---
title: Timer 구성 요소 개요(Windows Forms)
ms.date: 03/30/2017
f1_keywords:
- Timer
helpviewer_keywords:
- Timer component [Windows Forms], about Timer components
- timers [Windows Forms], about timers
ms.assetid: e672c05b-a8b6-4b26-9e4d-9223aa9e3873
ms.openlocfilehash: a13afba026f1f9eed095817c65637bb6a091c7f0
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/09/2019
ms.locfileid: "57725287"
---
# <a name="timer-component-overview-windows-forms"></a>Timer 구성 요소 개요(Windows Forms)
Windows Forms <xref:System.Windows.Forms.Timer>는 일정한 간격마다 이벤트를 발생시키는 구성 요소입니다. 이 구성 요소는 Windows Forms 환경에 맞게 설계되었습니다. 서버 환경에 적합한 타이머가 필요한 경우 [서버 기반 타이머 소개](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/tb9yt5e6(v=vs.90))를 참조하세요.  
  
## <a name="key-properties-methods-and-events"></a>키 속성, 메서드 및 이벤트  
 간격의 길이 정의한는 <xref:System.Windows.Forms.Timer.Interval%2A> 속성을 해당 값은 밀리초에서입니다. 구성 요소를 사용 하는 경우는 <xref:System.Windows.Forms.Timer.Tick> 이벤트는 간격입니다. 코드 실행을 추가할 위치입니다. 자세한 내용은 [방법: Windows Forms Timer 구성 요소를 사용 하 여 설정 된 간격 프로시저를 실행](run-procedures-at-set-intervals-with-wf-timer-component.md)합니다. 주요 메서드는 <xref:System.Windows.Forms.Timer> 구성 요소는 <xref:System.Windows.Forms.Timer.Start%2A> 및 <xref:System.Windows.Forms.Timer.Stop%2A>, 타이머를 설정 하는 및 해제 합니다. 타이머 꺼진 재설정; 일시 중지 하려면 없기는 <xref:System.Windows.Forms.Timer> 구성 요소입니다.  
  
## <a name="see-also"></a>참고자료
- <xref:System.Windows.Forms.Timer>
- [Timer 구성 요소](timer-component-windows-forms.md)
- [Windows Forms Timer 구성 요소의 Interval 속성에 대한 제한 사항](limitations-of-the-timer-component-interval-property.md)
