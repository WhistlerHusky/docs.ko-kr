---
title: ICorDebugController::EnumerateThreads 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugController.EnumerateThreads
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugController::EnumerateThreads
helpviewer_keywords:
- ICorDebugController::EnumerateThreads method [.NET Framework debugging]
- EnumerateThreads method [.NET Framework debugging]
ms.assetid: 73f536f6-4668-4a4a-b3e4-ac7df862d5be
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6a4bb4072c574edeac1c531978fac75595c252e0
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2019
ms.locfileid: "57481601"
---
# <a name="icordebugcontrollerenumeratethreads-method"></a>ICorDebugController::EnumerateThreads 메서드
프로세스에서 현재 관리 되는 스레드에 대 한 열거자를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
HRESULT EnumerateThreads (  
    [out] ICorDebugThreadEnum **ppThreads  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `ppThreads`  
 [out] 프로세스에서 활성화 된 모든 관리 되는 스레드에 대 한 열거자를 나타내는 "ICorDebugThreadEnum" 개체의 주소에 대 한 포인터입니다.  
  
## <a name="remarks"></a>설명  
 스레드 후 활성 차트로 간주 됩니다는 [icordebugmanagedcallback:: Createthread](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-createthread-method.md) 콜백 디스패치 된 전과 합니다 [icordebugmanagedcallback:: Exitthread](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-exitthread-method.md) 디스패치 된 콜백 . 관리 되는 스레드 없을 수 있습니다 반드시 모든 관리 되는 프레임 스택에 해당 합니다. 스레드 이전에 열거할 수는 [icordebugmanagedcallback:: Createprocess](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-createprocess-method.md) 콜백 합니다. 열거형은 자연스럽 게 비어 있게 됩니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

