---
title: 오류 없이 계속됩니다.
ms.date: 07/20/2015
f1_keywords:
- vbrID20
ms.assetid: f9631804-fd36-4443-b36c-30db827e6176
ms.openlocfilehash: 8cb58064e7249273051ead87cbc6841d13cdf5ad
ms.sourcegitcommit: bce0586f0cccaae6d6cbd625d5a7b824d1d3de4b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/02/2019
ms.locfileid: "58840447"
---
# <a name="resume-without-error"></a>오류 없이 계속됩니다.
`Resume` 문을 오류 처리 코드 외부에 있거나 오류가 없는 경우에 코드 오류 처리기로 점프 합니다.  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
1.  이동 된 `Resume` 오류 처리기로 문 또는 삭제 합니다.  
  
2.  오류 처리기를 식별 하는 레이블에 대 한 프로시저를 검색 프로시저에서 레이블로 점프 발생할 수 없습니다. 대상으로 지정 하는 레이블과 중복 하는 경우는 `GoTo` 문이 아닌는 `On Error GoTo` 문에서 원하는 대상와 일치 하도록 줄 레이블을 변경 합니다.  
  
## <a name="see-also"></a>참고자료

- [Resume 문](../../../visual-basic/language-reference/statements/resume-statement.md)
- [On Error 문](../../../visual-basic/language-reference/statements/on-error-statement.md)
