---
title: ISymUnmanagedVariable 인터페이스
ms.date: 03/30/2017
api_name:
- ISymUnmanagedVariable
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedVariable
helpviewer_keywords:
- ISymUnmanagedVariable interface [.NET Framework debugging]
ms.assetid: 704c69ba-77bc-40d7-8c0c-400061686321
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 50c38c5a9e1799a460c5be1f7234b36968dc3da2
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54706893"
---
# <a name="isymunmanagedvariable-interface"></a>ISymUnmanagedVariable 인터페이스
매개 변수, 지역 변수 또는 필드 등의 변수를 나타냅니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[GetAddressField1 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedvariable-getaddressfield1-method.md)|이 변수에 대 한 첫 번째 주소 필드를 가져옵니다. 해당 의미는 주소에 따라 달라 집니다.|  
|[GetAddressField2 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedvariable-getaddressfield2-method.md)|이 변수에 대 한 두 번째 주소 필드를 가져옵니다. 해당 의미는 주소에 따라 달라 집니다.|  
|[GetAddressField3 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedvariable-getaddressfield3-method.md)|이 변수에 대 한 세 번째 주소 필드를 가져옵니다. 해당 의미는 주소에 따라 달라 집니다.|  
|[GetAddressKind 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedvariable-getaddresskind-method.md)|이 변수의 주소가의 종류를 가져옵니다.|  
|[GetAttributes 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedvariable-getattributes-method.md)|이 변수에 대 한 특성 플래그를 가져옵니다.|  
|[GetEndOffset 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedvariable-getendoffset-method.md)|부모 내에서이 변수의 끝 오프셋을 가져옵니다.|  
|[GetName 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedvariable-getname-method.md)|이 변수의 이름을 가져옵니다.|  
|[GetSignature 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedvariable-getsignature-method.md)|이 변수 시그니처를 가져옵니다.|  
|[GetStartOffset 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedvariable-getstartoffset-method.md)|부모 내에서이 변수의 시작 오프셋을 가져옵니다.|  
  
## <a name="requirements"></a>요구 사항  
 **헤더:** CorSym.idl, CorSym.h  
  
## <a name="see-also"></a>참고자료
- [진단 기호 저장소 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/diagnostics-symbol-store-interfaces.md)
