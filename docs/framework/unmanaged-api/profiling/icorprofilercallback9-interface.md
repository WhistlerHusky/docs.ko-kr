---
title: ICorProfilerCallback9 인터페이스
ms.date: 04/10/2018
api_name:
- ICorProfilerCallback9
api_location:
- mscorwks.dll
- corprof.idl
api_type:
- COM
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a6c480af921fb0259ef85beec8d8f65bdd430522
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54689313"
---
# <a name="icorprofilercallback9-interface"></a>ICorProfilerCallback9 인터페이스
[.NET Framework 4.7.2 이상 버전에서 지원 됨]  

 서브 클래스 [ICorProfilerCallback8](icorprofilercallback8-interface.md) 동적 메서드 가비지 수집 되 고 이후에 언로드 되었음을 프로파일러에 알리기 위해 공용 언어 런타임에서 사용 되는 콜백 메서드를 제공 하는 합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[DynamicMethodUnloaded 메서드](ICorProfilerCallback9-dynamicmethodunloaded-method.md)|동적 메서드 가비지 수집 되 고 이후에 언로드 되었음을 프로파일러에 알립니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
**.NET Framework 버전:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  

## <a name="see-also"></a>참고자료
- [프로파일링 인터페이스](profiling-interfaces.md)
- [ICorProfilerCallback8 인터페이스](icorprofilercallback9-interface.md)
- [ICorProfilerCallback8.DynamicMethodJITCompilationStarted 메서드](icorprofilercallback8-dynamicmethodjitcompilationstarted-method.md)
- [ICorProfilerCallback8.DynamicMethodJITCompilationFinished 메서드](icorprofilercallback8-dynamicmethodjitcompilationfinished-method.md)
