---
title: ICorDebugNativeFrame2::IsMatchingParentFrame 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugNativeFrame2.IsMatchingParentFrame Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugNativeFrame2::IsMatchingParentFrame
helpviewer_keywords:
- IsMatchingParentFrame method [.NET Framework debugging]
- ICorDebugNativeFrame2::IsMatchingParentFrame method [.NET Framework debugging]
ms.assetid: d2ca20db-df22-4528-a0dd-a09ea62c8998
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 56d2c28529d3f3ee87fe3fdedd91634133ebf864
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2019
ms.locfileid: "57492207"
---
# <a name="icordebugnativeframe2ismatchingparentframe-method"></a>ICorDebugNativeFrame2::IsMatchingParentFrame 메서드
지정된 된 프레임에 현재 프레임의 부모 인지 여부를 결정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
HRESULT IsMatchingParentFrame([in] ICorDebugNativeFrame2  
                                      *pPotentialParentFrame,  
                              [out] BOOL *pIsParent);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pPotentialParentFrame`  
 [in] 부모 상태에 대 한 평가 하려는 프레임 개체에 대 한 포인터입니다.  
  
 `pIsParent`  
 [out] `true` 하는 경우 `pPotentialParentFrame` 현재 프레임의 부모이 고, 그렇지 않으면 `false`합니다.  
  
## <a name="return-value"></a>반환 값  
 이 메서드는 다음과 같은 특정 HRESULT뿐만 아니라 메서드 오류를 나타내는 HRESULT 오류도 반환합니다.  
  
|HRESULT|설명|  
|-------------|-----------------|  
|S_OK|부모 상태가 반환 되었습니다.|  
|E_FAIL|부모 상태를 반환 하지 못했습니다.|  
|E_INVALIDARG|`pPotentialParentFrame` 또는 `pIsParent`이 null입니다.|  
  
## <a name="exceptions"></a>예외  
  
## <a name="remarks"></a>설명  
 `IsMatchingParentFrame` 반환 `true` 의 경우 프레임 개체를 메서드에 전달 하는 메서드가 호출 된 프레임 개체의 부모입니다. 지정된 된 프레임의 자식이 아닌 프레임에서 메서드를 호출 하는 경우는 오류를 반환 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참고자료
- [ICorDebugNativeFrame2 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebugnativeframe2-interface.md)
- [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
- [디버깅](../../../../docs/framework/unmanaged-api/debugging/index.md)
