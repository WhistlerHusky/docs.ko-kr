---
title: '방법: GruopBox 템플릿 정의'
ms.date: 03/30/2017
helpviewer_keywords:
- controls [WPF], GroupBox
- GroupBox control [WPF], creating templates
ms.assetid: 85a4d1a7-4753-4f4a-b26d-14fa10c1ddb5
ms.openlocfilehash: 6b4ad4a588aab93f5445cda962af890bfcd41c14
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57377666"
---
# <a name="how-to-define-a-groupbox-template"></a>방법: GruopBox 템플릿 정의
에 대 한 템플릿을 만드는 방법을 보여 주는이 예제는 <xref:System.Windows.Controls.GroupBox> 제어 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 정의 <xref:System.Windows.Controls.GroupBox> 컨트롤 템플릿을 사용 하 여를 <xref:System.Windows.Controls.Grid> 레이아웃에 대 한 제어 합니다. 템플릿을 사용 하는 <xref:System.Windows.Controls.BorderGapMaskConverter> 경계를 정의 하는 <xref:System.Windows.Controls.GroupBox> 테두리를 가리지 않습니다 있도록는 <xref:System.Windows.Controls.HeaderedContentControl.Header%2A> 콘텐츠.  
  
 [!code-xaml[GroupBoxSnippet#GroupBoxTemplate](~/samples/snippets/csharp/VS_Snippets_Wpf/GroupBoxSnippet/CS/Window1.xaml#groupboxtemplate)]  
  
## <a name="see-also"></a>참고자료
- <xref:System.Windows.Controls.GroupBox>
- [방법: GroupBox 만들기](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms748321(v=vs.90))
