---
title: 인스턴싱 초기화
ms.date: 03/30/2017
ms.assetid: 154d049f-2140-4696-b494-c7e53f6775ef
ms.openlocfilehash: ec44276d56b0a914c742a5a709f2207f8111e57b
ms.sourcegitcommit: bce0586f0cccaae6d6cbd625d5a7b824d1d3de4b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/02/2019
ms.locfileid: "58827915"
---
# <a name="instancing-initialization"></a>인스턴싱 초기화
이 샘플을 확장 합니다 [풀링](../../../../docs/framework/wcf/samples/pooling.md) 인터페이스를 정의 하 여 샘플 `IObjectControl`, 활성화 및 비활성화 하 여 개체의 초기화를 사용자 지정 하는 합니다. 클라이언트에서는 개체를 풀로 반환하는 메서드와 개체를 풀로 반환하지 않는 메서드를 호출합니다.  
  
> [!NOTE]
>  이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.  
  
## <a name="extensibility-points"></a>확장 지점  
 Windows Communication Foundation (WCF) 확장을 만드는 첫 번째 단계는 사용할 확장명 지점을 결정 하는 것입니다. Wcf에서 용어 *EndpointDispatcher* 사용자 서비스의 메서드 호출으로 들어오는 메시지를 변환 하 고 보내는 메시지를 해당 메서드에서 반환 값을 변환 하는 것에 대 한 런타임 구성 요소를 나타냅니다 . WCF 서비스에는 각 끝점에 대해 EndpointDispatcher를 만듭니다.  
  
 EndpointDispatcher는 <xref:System.ServiceModel.Dispatcher.EndpointDispatcher> 클래스를 사용하여 서비스에서 보내거나 받는 모든 메시지에 대해 엔드포인트 범위 확장성을 제공합니다. 이 클래스를 사용하면 EndpointDispatcher의 동작을 제어하는 다양한 속성을 사용자 지정할 수 있습니다. 이 샘플에서는 서비스 클래스의 인스턴스를 제공하는 개체를 가리키는 <xref:System.ServiceModel.Dispatcher.DispatchRuntime.InstanceProvider%2A> 속성을 중점적으로 다룹니다.  
  
## <a name="iinstanceprovider"></a>IInstanceProvider  
 Wcf에서 EndpointDispatcher를 구현 하는 인스턴스 공급자를 사용 하 여 서비스 클래스의 인스턴스를 만듭니다는 <xref:System.ServiceModel.Dispatcher.IInstanceProvider> 인터페이스입니다. 이 인터페이스에는 다음과 같은 두 개의 메서드만 있습니다.  
  
-   <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%2A>: 메시지가 도착할 때 하십시오 디스패처에서 호출을 <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%2A> 메시지를 처리할 서비스 클래스의 인스턴스를 만드는 메서드. 이 메서드의 호출 빈도는 <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A> 속성에 의해 결정됩니다. 예를 들어 <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A> 속성이 <xref:System.ServiceModel.InstanceContextMode.PerCall?displayProperty=nameWithType>로 설정된 경우 도착하는 각 메시지를 처리하기 위해 서비스 클래스의 새 인스턴스가 만들어지므로, 메시지가 도착할 때마다 <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%2A>가 호출됩니다.  
  
-   <xref:System.ServiceModel.Dispatcher.IInstanceProvider.ReleaseInstance%2A>: EndpointDispatcher를 호출 하는 서비스 인스턴스가 메시지를 처리 완료 되 면를 <xref:System.ServiceModel.Dispatcher.IInstanceProvider.ReleaseInstance%2A> 메서드. <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%2A> 메서드에서와 마찬가지로 이 메서드의 호출 빈도는 <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A> 속성에 의해 결정됩니다.  
  
## <a name="the-object-pool"></a>개체 풀  
 `ObjectPoolInstanceProvider` 클래스에는 개체 풀이 구현되어 있습니다. 이 클래스는 <xref:System.ServiceModel.Dispatcher.IInstanceProvider> 인터페이스를 구현하여 서비스 모델 계층과 상호 작용합니다. EndpointDispatcher가 새 인스턴스를 만드는 대신 <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%2A> 메서드를 호출하면 사용자 지정 구현에서 메모리 내의 풀에 있는 기존 개체를 찾습니다. 사용할 수 있는 개체가 있으면 반환되고, 그렇지 않으면 `ObjectPoolInstanceProvider`는 `ActiveObjectsCount` 속성(풀에서 반환된 개체의 개수)이 최대 풀 크기에 도달했는지 확인합니다. 이 크기에 도달하지 않았으면 새 인스턴스가 만들어지고 호출자에게 반환하며 이어서 `ActiveObjectsCount`가 증가합니다. 도달했으면 구성된 시간 동안 개체 만들기 요청이 큐에 대기합니다. `GetObjectFromThePool`의 구현은 다음 샘플 코드에 표시되어 있습니다.  
  
```  
private object GetObjectFromThePool()  
{  
    bool didNotTimeout =   
       availableCount.WaitOne(creationTimeout, true);  
    if(didNotTimeout)  
    {  
         object obj = null;  
         lock (poolLock)  
        {  
             if (pool.Count != 0)  
             {  
                   obj = pool.Pop();  
                   activeObjectsCount++;  
             }  
             else if (pool.Count == 0)  
             {  
                   if (activeObjectsCount < maxPoolSize)  
                   {  
                        obj = CreateNewPoolObject();  
                        activeObjectsCount++;  
  
                        #if (DEBUG)  
                        WritePoolMessage(  
                             ResourceHelper.GetString("MsgNewObject"));  
                       #endif  
                   }                          
            }  
           idleTimer.Stop();  
      }  
     // Call the Activate method if possible.  
    if (obj is IObjectControl)  
   {  
         ((IObjectControl)obj).Activate();  
   }  
   return obj;  
}  
throw new TimeoutException(  
ResourceHelper.GetString("ExObjectCreationTimeout"));  
}  
```  
  
 사용자 지정 `ReleaseInstance` 구현에서는 해제된 인스턴스를 다시 풀에 추가하고 `ActiveObjectsCount` 값을 감소시킵니다. EndpointDispatcher는 서로 다른 스레드에서 이러한 메서드를 호출할 수 있기 때문에 `ObjectPoolInstanceProvider` 클래스의 클래스 수준 멤버에 대한 액세스를 동기화해야 합니다.  
  
```  
public void ReleaseInstance(InstanceContext instanceContext, object instance)  
{  
    lock (poolLock)  
    {  
        // Check whether the object can be pooled.   
        // Call the Deactivate method if possible.  
        if (instance is IObjectControl)  
        {  
            IObjectControl objectControl = (IObjectControl)instance;  
            objectControl.Deactivate();  
  
            if (objectControl.CanBePooled)  
            {  
                pool.Push(instance);  
  
                #if(DEBUG)  
                WritePoolMessage(  
                    ResourceHelper.GetString("MsgObjectPooled"));  
                #endif                          
            }  
            else  
            {  
                #if(DEBUG)  
                WritePoolMessage(  
                    ResourceHelper.GetString("MsgObjectWasNotPooled"));  
                #endif  
            }  
        }  
        else  
        {  
            pool.Push(instance);  
  
            #if(DEBUG)  
            WritePoolMessage(  
                ResourceHelper.GetString("MsgObjectPooled"));  
            #endif   
        }  
  
        activeObjectsCount--;  
  
        if (activeObjectsCount == 0)  
        {  
            idleTimer.Start();                       
        }  
    }  
  
    availableCount.Release(1);  
}  
```  
  
 `ReleaseInstance` 메서드는 제공 된 *정리 초기화* 기능. 일반적으로 풀은 풀의 수명 동안 최소한의 개체 수를 유지합니다. 하지만 사용량이 지나치게 많은 경우에는 구성에 지정된 최대 한도를 사용하기 위해 풀에 추가 개체를 만들어야 할 수도 있습니다. 결국 풀의 사용이 줄어들면 여분의 해당 개체는 추가 오버헤드가 될 수 있습니다. 따라서 `activeObjectsCount`가 0에 도달하면 정리 주기를 트리거하고 수행하는 유휴 타이머가 시작됩니다.  
  
```  
if (activeObjectsCount == 0)  
{  
    idleTimer.Start();   
}  
```  
  
 ServiceModel 계층 확장은 다음 동작을 사용하여 후크됩니다.  
  
-   서비스 동작: 전체 서비스 런타임을 사용자 지정할 수 있습니다.  
  
-   끝점 동작: EndpointDispatcher를 포함 하 여 특정 서비스 끝점을 사용자 지정할 수 있습니다.  
  
-   계약 동작: 사용자 지정할 수 <xref:System.ServiceModel.Dispatcher.ClientRuntime> 또는 <xref:System.ServiceModel.Dispatcher.DispatchRuntime> 클라이언트 또는 서비스에서 각각 클래스입니다.  
  
-   작업 동작: 사용자 지정할 수 <xref:System.ServiceModel.Dispatcher.ClientOperation> 또는 <xref:System.ServiceModel.Dispatcher.DispatchOperation> 클라이언트 또는 서비스에서 각각 클래스입니다.  
  
 개체 풀링 확장을 위해 엔드포인트 동작 또는 서비스 동작을 만들 수 있습니다. 이 예제에서는 서비스의 모든 엔드포인트에 개체 풀링 기능을 적용하는 서비스 동작을 사용합니다. 서비스 동작은 <xref:System.ServiceModel.Description.IServiceBehavior> 인터페이스를 구현하여 만듭니다. ServiceModel에 사용자 지정 동작을 인식시키는 방법에는 다음 여러 가지가 있습니다.  
  
-   사용자 지정 특성 사용  
  
-   사용자 지정 동작을 서비스 설명의 동작 컬렉션에 명령적으로 추가  
  
-   구성 파일 확장  
  
 이 샘플에서는 사용자 지정 특성을 사용합니다. <xref:System.ServiceModel.ServiceHost>가 생성되면 이는 서비스의 형식 정의에 사용된 특성을 확인하고 사용 가능한 동작을 서비스 설명의 동작 컬렉션에 추가합니다.  
  
 합니다 <xref:System.ServiceModel.Description.IServiceBehavior> 인터페이스에는: <xref:System.ServiceModel.Description.IServiceBehavior.Validate%2A> `,` <xref:System.ServiceModel.Description.IServiceBehavior.AddBindingParameters%2A> `,` 고 <xref:System.ServiceModel.Description.IServiceBehavior.ApplyDispatchBehavior%2A>입니다. WCF에서 이러한 메서드를 호출 하는 경우는 <xref:System.ServiceModel.ServiceHost> 초기화 하는 중입니다. <xref:System.ServiceModel.Description.IServiceBehavior.Validate%2A?displayProperty=nameWithType>가 먼저 호출되어 서비스에 일관성을 검사할 수 있게 해 줍니다. <xref:System.ServiceModel.Description.IServiceBehavior.AddBindingParameters%2A?displayProperty=nameWithType>이 다음으로 호출됩니다. 이 메서드는 고급 시나리오에서만 필요합니다. <xref:System.ServiceModel.Description.IServiceBehavior.ApplyDispatchBehavior%2A?displayProperty=nameWithType>가 마지막으로 호출되며 런타임 구성을 담당합니다. 다음 매개 변수가 <xref:System.ServiceModel.Description.IServiceBehavior.ApplyDispatchBehavior%2A?displayProperty=nameWithType>에 전달됩니다.  
  
-   `Description`: 이 매개 변수는 전체 서비스에 대 한 서비스 설명을 제공합니다. 이 매개 변수를 사용하여 서비스의 엔드포인트, 계약, 바인딩 및 그 외 서비스와 관련된 데이터에 대한 설명 데이터를 검사할 수 있습니다.  
  
-   `ServiceHostBase`: 이 매개 변수를 제공 합니다 <xref:System.ServiceModel.ServiceHostBase> 현재 초기화 되는 합니다.  
  
 사용자 지정 <xref:System.ServiceModel.Description.IServiceBehavior> 구현에서는 `ObjectPoolInstanceProvider`의 새 인스턴스가 인스턴스화되어 <xref:System.ServiceModel.Dispatcher.DispatchRuntime.InstanceProvider%2A>에 첨부된 각 <xref:System.ServiceModel.Dispatcher.EndpointDispatcher>의 <xref:System.ServiceModel.ServiceHostBase> 속성에 할당됩니다.  
  
```  
public void ApplyDispatchBehavior(ServiceDescription description, ServiceHostBase serviceHostBase)  
{  
    if (enabled)  
    {  
        // Create an instance of the ObjectPoolInstanceProvider.  
        instanceProvider = new ObjectPoolInstanceProvider(description.ServiceType,  
        maxPoolSize, minPoolSize, creationTimeout);  
  
        // Assign our instance provider to Dispatch behavior in each   
        // endpoint.  
        foreach (ChannelDispatcherBase cdb in serviceHostBase.ChannelDispatchers)  
        {  
             ChannelDispatcher cd = cdb as ChannelDispatcher;  
             if (cd != null)  
             {  
                 foreach (EndpointDispatcher ed in cd.Endpoints)  
                 {  
                        ed.DispatchRuntime.InstanceProvider = instanceProvider;  
                 }  
             }  
         }  
     }  
}   
```  
  
 <xref:System.ServiceModel.Description.IServiceBehavior> 구현 외에 `ObjectPoolingAttribute` 클래스에도 특성 인수를 사용하여 개체 풀을 사용자 지정하는 멤버가 몇 개 있습니다. 이러한 멤버에는 .NET Enterprise Services에서 제공하는 개체 풀링 기능 집합과 일치하는 `MaxSize`, `MinSize`, `Enabled` 및 `CreationTimeout`이 포함됩니다.  
  
 개체 풀링 동작 수를 새로 만든 사용자 지정 서비스 구현을 주석으로 이제 WCF 서비스에 추가 하는 수 `ObjectPooling` 특성입니다.  
  
```  
[ObjectPooling(MaxSize=1024, MinSize=10, CreationTimeout=30000]      
public class PoolService : IPoolService  
{  
  // …  
}  
```  
  
## <a name="hooking-activation-and-deactivation"></a>활성화 및 비활성화 후크  
 개체 풀링의 주요 목적은 만들고 초기화하는 데 비교적 자원이 많이 사용되는 수명이 짧은 개체를 최적화하는 데 있습니다. 따라서 개체 풀링을 제대로 사용하면 응용 프로그램의 성능을 현저히 향상시킬 수 있습니다. 풀에서 개체가 반환되기 때문에 생성자는 한 번만 호출됩니다. 반면 일부 응용 프로그램의 경우는 단일 컨텍스트 동안 사용된 리소스를 초기화하고 정리할 수 있도록 일정 수준의 제어가 필요합니다. 예를 들어 일련의 계산에 사용되는 개체는 다음 계산을 처리하기 전에 private 필드를 재설정할 수 있습니다. 엔터프라이즈 서비스에서는 개체 개발자가 `Activate` 기본 클래스의 `Deactivate` 및 <xref:System.EnterpriseServices.ServicedComponent> 메서드를 재정의할 수 있도록 하여 이러한 종류의 컨텍스트별 초기화를 사용하도록 설정합니다.  
  
 개체 풀은 풀에서 개체를 반환하기 바로 전에 `Activate` 메서드를 호출합니다. 개체가 풀로 다시 돌아갈 때 `Deactivate`가 호출됩니다. <xref:System.EnterpriseServices.ServicedComponent> 기본 클래스에는 또한 개체를 계속 풀링할 수 있는지 여부를 풀에 알리는 데 사용되는 `boolean`라는 `CanBePooled` 속성이 있습니다.  
  
 이 기능을 모방하기 위해 이 샘플에서는 이전에 언급된 멤버가 있는 공용 인터페이스(`IObjectControl`)를 선언합니다. 그런 다음 이 인터페이스는 컨텍스트별 초기화를 제공하는 데 사용되는 서비스 클래스에 의해 구현됩니다. 이러한 요구 사항에 맞게 <xref:System.ServiceModel.Dispatcher.IInstanceProvider> 구현을 수정해야 합니다. 이제 가져올 때마다 개체를 호출 하 여 합니다 `GetInstance` 메서드를 확인 해야 합니다는 개체가 구현 하는지 `IObjectControl.` 그렇지 않으면 호출 해야 합니다는 `Activate` 메서드 적절 하 게 합니다.  
  
```  
if (obj is IObjectControl)  
{  
    ((IObjectControl)obj).Activate();  
}  
```  
  
 개체를 풀에 반환할 때는 개체를 다시 풀에 추가하기 전에 `CanBePooled` 속성을 확인해야 합니다.  
  
```  
if (instance is IObjectControl)  
{  
    IObjectControl objectControl = (IObjectControl)instance;  
    objectControl.Deactivate();  
    if (objectControl.CanBePooled)  
    {  
       pool.Push(instance);  
    }  
}  
```  
  
 서비스 개발자는 개체를 풀링할 수 있는지 여부를 결정할 수 있으므로 지정된 시간에 풀에 있는 개체 수가 최소 크기 아래로 내려갈 수 있습니다. 따라서 개체 수가 최소 수준 아래로 내려갔는지 확인하고 정리 절차에서 필요한 시작 작업을 수행해야 합니다.  
  
```  
// Remove the surplus objects.  
if (pool.Count > minPoolSize)  
{  
  // Clean the surplus objects.  
}                      
else if (pool.Count < minPoolSize)  
{  
  // Reinitialize the missing objects.  
  while(pool.Count != minPoolSize)  
  {  
    pool.Push(CreateNewPoolObject());  
  }  
}  
```  
  
 샘플을 실행하면 작업 요청 및 응답이 서비스와 클라이언트 콘솔 창 모두에 표시됩니다. 서비스와 클라이언트를 종료하려면 각 콘솔 창에서 Enter 키를 누릅니다.  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1.  수행 했는지 확인 합니다 [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)합니다.  
  
2.  지침에 따라 솔루션을 빌드하려면 [Building Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)합니다.  
  
3.  단일 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면의 지침을 따릅니다 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)합니다.  
  
> [!IMPORTANT]
>  컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  이 디렉터리가 없으면로 이동 [Windows Communication Foundation (WCF) 및.NET Framework 4 용 Windows WF (Workflow Foundation) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 모든 Windows Communication Foundation (WCF)를 다운로드 하 고 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플. 이 샘플은 다음 디렉터리에 있습니다.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Instancing\Initialization`  
  
