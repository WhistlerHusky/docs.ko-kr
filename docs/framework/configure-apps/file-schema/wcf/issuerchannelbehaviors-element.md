---
title: <issuerChannelBehaviors> 요소
ms.date: 03/30/2017
ms.assetid: f7378673-8e9b-45b2-98d1-cf5dccdd8c40
ms.openlocfilehash: 7cbd50daa82b0ca937a1bba93786545898b03c8b
ms.sourcegitcommit: 5c2176883dc3107445702724a7caa7ac2f6cb0d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/03/2019
ms.locfileid: "58890477"
---
# <a name="issuerchannelbehaviors-element"></a>\<issuerChannelBehaviors > 요소

지정한 서비스 토큰 서비스와 통신할 때 사용 되는 Windows Communication Foundation (WCF) 클라이언트 끝점 동작 (구성에 정의 됨)의 컬렉션을 포함 합니다. 정의 된 동작을 포함할 수 없습니다 [\<clientCredentials>](../../../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md) 요소입니다.

```xml
<system.ServiceModel>
  <behaviors>
    <endpointBehaviors>
      <behavior>
        <clientCredentials>
          <issuedToken>
            <issuerChannelBehaviors>
```

## <a name="syntax"></a>구문

```xml
<issuerChannelBehaviors>
  <add behaviorConfiguration="string"
       issuerAddress="string" />
</issuerChannelBehaviors>
```

## <a name="attributes-and-elements"></a>특성 및 요소

다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.

### <a name="attributes"></a>특성

없음

### <a name="child-elements"></a>자식 요소

|요소|설명|
|-------------|-----------------|
|[\<add>](../../../../../docs/framework/configure-apps/file-schema/wcf/add-of-issuerchannelbehaviors.md)|동작을 컬렉션에 추가합니다.|

### <a name="parent-elements"></a>부모 요소

|요소|설명|
|-------------|-----------------|
|[\<issuedToken>](../../../../../docs/framework/configure-apps/file-schema/wcf/issuedtoken.md)|서비스에 대해 클라이언트를 인증할 때 사용되는 사용자 지정 토큰을 지정합니다.|

## <a name="remarks"></a>설명

`<clientCredentials>` 요소를 포함하는 동작을 제외한 동작을 서비스와 통신하는 데 사용하는 경우 이 요소를 사용합니다. 예를 들어 경우는 [\<dataContractSerializer >](../../../../../docs/framework/configure-apps/file-schema/wcf/datacontractserializer-element.md) 동작 요소가 포함 되어야 합니다.

## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Configuration.IssuedTokenClientElement.IssuerChannelBehaviors%2A>
- <xref:System.ServiceModel.Configuration.IssuedTokenClientBehaviorsElement>
- <xref:System.ServiceModel.Configuration.IssuedTokenClientBehaviorsElementCollection>
- <xref:System.ServiceModel.Security.IssuedTokenClientCredential.IssuerChannelBehaviors%2A>
- [서비스 ID 및 인증](../../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)
- [보안 동작](../../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)
- [페더레이션 및 발급된 토큰](../../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)
- [서비스 및 클라이언트에 보안 설정](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)
- [클라이언트에 보안 설정](../../../../../docs/framework/wcf/securing-clients.md)
- [방법: 페더레이션 클라이언트 만들기](../../../../../docs/framework/wcf/feature-details/how-to-create-a-federated-client.md)
- [방법: 로컬 발급자 구성](../../../../../docs/framework/wcf/feature-details/how-to-configure-a-local-issuer.md)
- [페더레이션 및 발급된 토큰](../../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)
