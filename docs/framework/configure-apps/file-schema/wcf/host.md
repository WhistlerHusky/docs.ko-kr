---
title: <host>
ms.date: 03/30/2017
ms.assetid: be566d55-9d50-4b2e-985d-52a5cc26cbbb
ms.openlocfilehash: 8a8f9db96281d8d775ff5c2923018228b3a9c1e5
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2019
ms.locfileid: "55269031"
---
# <a name="host"></a>\<host>
서비스 호스트의 설정을 지정합니다.  
  
 \<system.ServiceModel>  
\<services>  
\<service>  
\<host>  
  
## <a name="syntax"></a>구문  
  
```xml  
<host>
  <baseAddresses>
    <add baseAddress="string" />
  </baseAddresses>
  <timeOuts closeTimeout="TimeSpan"
            openTimeout="TimeSpan" />
</host>
```  
  
## <a name="type"></a>형식  
 `Type`  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
 없음  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<baseAddresses>](../../../../../docs/framework/configure-apps/file-schema/wcf/baseaddresses.md)|서비스 호스트에서 사용하는 기본 주소를 지정하는 `baseAddress` 요소 컬렉션입니다.|  
|[\<timeOuts>](../../../../../docs/framework/configure-apps/file-schema/wcf/timeouts.md)|서비스 호스트가 열리거나 닫히는 데 허용되는 시간 간격을 지정하는 구성 요소입니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<service>](../../../../../docs/framework/configure-apps/file-schema/wcf/service.md)|Windows Communication Foundation (WCF) 서비스에 대 한 설정을 지정합니다.|  
  
## <a name="see-also"></a>참고자료
- <xref:System.ServiceModel.Configuration.HostElement>
- <xref:System.ServiceModel.ServiceHost>
- [호스팅](../../../../../docs/framework/wcf/feature-details/hosting.md)
