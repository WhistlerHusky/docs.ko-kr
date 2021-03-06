---
title: IDebugAutoAttach::AutoAttach 메서드
ms.date: 03/30/2017
api_name:
- IDebugAutoAttach.AutoAttach
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- IDebugAutoAttach::AutoAttach
helpviewer_keywords:
- AutoAttach method [.NET Framework debugging]
- IDebugAutoAttach::AutoAttach method [.NET Framework debugging]
ms.assetid: 3cf3bd9c-7d88-4afa-a476-94cdc7609aa6
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 16ccc56579a1ebe45ada61a9565cc8ade335333d
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2019
ms.locfileid: "57469680"
---
# <a name="idebugautoattachautoattach-method"></a>IDebugAutoAttach::AutoAttach 메서드
서버에서 호출한 디버거 자동 수행 연결 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
HRESULT AutoAttach  
(  
    [in]  REFGUID   guidPort,  
    [in]  DWORD     dwPid,  
    [in]  AUTOATTACH_PROGRAM_TYPE dwProgramType,  
    [in]  DWORD     dwProgramId,  
    [in]  LPCWSTR   pszSessionId  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `guidPort`  
 [in] 항상로 `GUID_NULL`합니다.  
  
 `dwPid`  
 [in] 프로세스 ID, 일반적으로 사용 하 여 검색 된 `GetCurrentProcessId` 함수입니다.  
  
 `dwProgramType`  
 [in] 프로그램 형식: `AUTOATTACH_PROGRAM_WIN32`하십시오 `AUTOATTACH_PROGRAM_COMPLUS`, 또는 `AUTOATTACH_PROGRAM_UNKNOWN`합니다.  
  
 `dwProgramId`  
 [in] 프로그램 id입니다.  
  
 `pszSessionId`  
 [in] Debug 동사를 전달한 문자열입니다.  
  
## <a name="return-value"></a>반환 값  
 메서드가 성공 하면 S_OK입니다.  
  
## <a name="requirements"></a>요구 사항  
 **헤더:** DbgAutoAttach.h  
  
## <a name="see-also"></a>참고자료
- [IDebugAutoAttach 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/idebugautoattach-interface.md)
