---
title: 파생 클래스는 기본 클래스 이벤트를 발생시킬 수 없습니다.
ms.date: 07/20/2015
f1_keywords:
- vbc30029
- bc30029
helpviewer_keywords:
- BC30029
ms.assetid: 63afa1c6-2f93-4512-a2f0-372455979771
ms.openlocfilehash: 0e9acf4b3e71295655c15ae9b1c80852c9aca8df
ms.sourcegitcommit: bce0586f0cccaae6d6cbd625d5a7b824d1d3de4b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/02/2019
ms.locfileid: "58835143"
---
# <a name="derived-classes-cannot-raise-base-class-events"></a>파생 클래스는 기본 클래스 이벤트를 발생시킬 수 없습니다.
이벤트 선언 되는 선언 공간 에서만에서 발생할 수 있습니다. 따라서 클래스 다른 클래스와 파생 된 하나에서 이벤트를 발생 시킬 수 없습니다.  
  
 **오류 ID:** BC30029  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
-   이동 합니다 `Event` 문 또는 `RaiseEvent` 문을 동일한 클래스에서.  
  
## <a name="see-also"></a>참고자료

- [Event 문](../../../visual-basic/language-reference/statements/event-statement.md)
- [RaiseEvent 문](../../../visual-basic/language-reference/statements/raiseevent-statement.md)
