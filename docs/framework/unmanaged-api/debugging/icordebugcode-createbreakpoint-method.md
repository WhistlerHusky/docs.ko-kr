---
title: ICorDebugCode::CreateBreakpoint 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugCode.CreateBreakpoint
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugCode::CreateBreakpoint
helpviewer_keywords:
- ICorDebugCode::CreateBreakpoint method [.NET Framework debugging]
- CreateBreakpoint method, ICorDebugCode interface [.NET Framework debugging]
ms.assetid: 46842618-0fe4-480b-871c-82fba82d23d9
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: df27d2ab609551bb7a7f6f4b0ff8c7118c9f93f8
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2019
ms.locfileid: "57478676"
---
# <a name="icordebugcodecreatebreakpoint-method"></a>ICorDebugCode::CreateBreakpoint 메서드
이 코드 세그먼트의 지정 된 오프셋 위치에서 중단점을 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```  
HRESULT CreateBreakpoint (  
    [in] ULONG32     offset,  
    [out] ICorDebugFunctionBreakpoint **ppBreakpoint  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `offset`  
 [in] 중단점을 만들려는 오프셋입니다.  
  
 `ppBreakpoint`  
 [out] 중단점을 나타내는 "ICorDebugFunctionBreakpoint" 개체의 주소에 대 한 포인터입니다.  
  
## <a name="remarks"></a>설명  
 중단점 활성화 되려면 프로세스 개체에 추가 되어야 합니다.  
  
 이 코드는 Microsoft intermediate language (MSIL) 코드 했으며 경우는-just-in-time (JIT)-네이티브 컴파일된 버전의 코드에서 중단점 JIT 컴파일 코드 에서도 적용 됩니다. (마찬가지 코드가 있는 경우 JIT 컴파일된 나중.)  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

