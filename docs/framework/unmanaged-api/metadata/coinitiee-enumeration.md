---
title: COINITIEE 열거형
ms.date: 03/30/2017
api_name:
- COINITIEE
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- COINITIEE
helpviewer_keywords:
- COINITIEE enumeration [.NET Framework metadata]
ms.assetid: 64264238-3b68-4bac-a887-36b552426a6c
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 48f15cc08167baaadc61787b8b1f7167304f0cae
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54569481"
---
# <a name="coinitiee-enumeration"></a>COINITIEE 열거형
사용 하는 상수를 지정 [CoInitializeEE](../../../../docs/framework/unmanaged-api/hosting/coinitializeee-function.md) 공용 언어 런타임을 초기화할 때.  
  
## <a name="syntax"></a>구문  
  
```  
typedef enum tagCOINITEE {  
   COINITEE_DEFAULT = 0x0,  
   COINITEE_DLL     = 0x1,  
   COINITEE_MAIN    = 0x2  
} COINITIEE;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|설명|  
|------------|-----------------|  
|`COINITEE_DEFAULT`|기본 초기화 모드입니다. 이 런타임을 초기화 하 고 기본 만듭니다 <xref:System.AppDomain>합니다.|  
|`COINITEE_DLL`|관리 되는 DLL을 실행 하도록 초기화 합니다.|  
|`COINITEE_MAIN`|관리 되는 EXE를 실행 하도록 초기화 합니다. 이 런타임을 초기화 하지만 기본 만들어지지는지 않습니다 <xref:System.AppDomain>, exe 파일의 기본 루틴을 입력 한 후 생성 됩니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MsCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료
- [메타데이터 열거형](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)
