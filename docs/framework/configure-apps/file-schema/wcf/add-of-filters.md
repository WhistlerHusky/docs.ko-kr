---
title: <add>의 <filters>
ms.date: 03/30/2017
ms.assetid: e3bf437c-dd99-49f3-9792-9a8721e6eaad
ms.openlocfilehash: 1340b70cf4656b764370a14955a2f4d6f6209fe4
ms.sourcegitcommit: 7156c0b9e4ce4ce5ecf48ce3d925403b638b680c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2019
ms.locfileid: "58466025"
---
# <a name="add-of-filters"></a>\<추가 >의 \<필터 >
로깅할 메시지 종류를 지정하는 XPath 필터입니다.  
  
 \<system.ServiceModel>  
\<diagnostic>  
\<messageLogging>  
\<filters>  
\<add>  
  
## <a name="syntax"></a>구문  
  
```xml  
<filters>
  <add filter="String" />
</filters>
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|필터|XPath 1.0 식에서 정의하는 XML 문서에 대한 쿼리를 지정하는 문자열입니다. 자세한 내용은 <xref:System.ServiceModel.Dispatcher.XPathMessageFilter>을 참조하세요.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<필터>](../../../../../docs/framework/configure-apps/file-schema/wcf/filters.md)|로깅할 메시지 종류를 제어하는 데 사용되는 XPath 필터 컬렉션을 포함합니다.|  
  
## <a name="remarks"></a>설명  
 필터는 전송 계층에서만 적용됩니다(`logMessagesAtTransportLevel` = `true`). 서비스 수준 및 잘못된 형식의 메시지 로깅은 필터의 영향을 받지 않습니다.  
  
 컬렉션에 필터를 추가하려면 `add` 키워드를 사용하세요. 하나 이상의 필터가 정의되면 그 중 최소한 하나의 필터와 일치하는 메시지만 로깅됩니다. 정의된 필터가 없으면 모든 메시지가 통과합니다.  
  
 필터는 모든 XPath 구문을 지원하며, 구성 파일에 표시되는 순서대로 적용됩니다. 필터 구문에 오류가 있으면 구성 예외가 발생합니다.  
  
 다음은 SOAP 헤더 섹션이 있는 메시지만 기록하는 필터 구성 방법에 대한 예제입니다.  
  
## <a name="example"></a>예제  
 다음은 SOAP 헤더 섹션이 있는 메시지만 기록하는 필터 구성 방법에 대한 예제입니다.  
  
```xml  
<messageLogging logEntireMessage="true"
                logMalformedMessages="true"
                logMessagesAtServiceLevel="true"
                logMessagesAtTransportLevel="true"
                maxMessagesToLog="420">
  <filters>
    <add xmlns:soap="http://www.w3.org/2003/05/soap-envelope">
      /soap:Envelope/soap:Headers
    </add>
  </filters>
</messageLogging>
```  
  
## <a name="see-also"></a>참고자료
- <xref:System.ServiceModel.Configuration.DiagnosticSection>
- <xref:System.ServiceModel.Diagnostics>
- <xref:System.ServiceModel.Configuration.DiagnosticSection.MessageLogging%2A>
- <xref:System.ServiceModel.Configuration.MessageLoggingElement>
- <xref:System.ServiceModel.Configuration.MessageLoggingElement.Filters%2A>
- <xref:System.ServiceModel.Configuration.XPathMessageFilterElement>
- <xref:System.ServiceModel.Dispatcher.XPathMessageFilter>
- [메시지 로깅 구성](../../../../../docs/framework/wcf/diagnostics/configuring-message-logging.md)
- [\<messageLogging>](../../../../../docs/framework/configure-apps/file-schema/wcf/messagelogging.md)
