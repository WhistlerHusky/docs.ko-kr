---
title: '방법: TextBox 컨트롤에서 탭 문자 사용'
ms.date: 03/30/2017
helpviewer_keywords:
- TextBox control [WPF], enabling tab characters
- tab characters [WPF], enabling
ms.assetid: 14b1b064-61f7-4958-be63-88d85b868d03
ms.openlocfilehash: 6d134757c3c08e92e608a7ff868b2f3d28a69b27
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57356548"
---
# <a name="how-to-enable-tab-characters-in-a-textbox-control"></a>방법: TextBox 컨트롤에서 탭 문자 사용
탭 문자에 대 한 동의가 일반 입력으로 사용 하도록 설정 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Controls.TextBox> 제어 합니다.  
  
## <a name="example"></a>예제  
 탭 문자에 대 한 동의가에서 입력으로 사용 하도록 설정 하려면을 <xref:System.Windows.Controls.TextBox> 컨트롤을 <xref:System.Windows.Controls.Primitives.TextBoxBase.AcceptsTab%2A> 특성을 **true**합니다.  
  
 [!code-xaml[TextBox_EnablingTab#_AcceptsTab](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBox_EnablingTab/CS/Window1.xaml#_acceptstab)]  
  
## <a name="see-also"></a>참고자료
- [TextBox 개요](textbox-overview.md)
- [RichTextBox 개요](richtextbox-overview.md)
