---
title: '방법: 설치 된 글꼴 열거'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- fonts [Windows Forms], enumerating installed
- examples [Windows Forms], fonts
ms.assetid: 26d74ef5-0f39-4eeb-8d20-00e66e014abe
ms.openlocfilehash: e56f06d6f7a762a1ef1ff85fa30751ea64f9f14b
ms.sourcegitcommit: 15ab532fd5e1f8073a4b678922d93b68b521bfa0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2019
ms.locfileid: "58653745"
---
# <a name="how-to-enumerate-installed-fonts"></a>방법: 설치 된 글꼴 열거
합니다 <xref:System.Drawing.Text.InstalledFontCollection> 클래스에서 상속 된 <xref:System.Drawing.Text.FontCollection> 추상 기본 클래스입니다. 사용할 수는 <xref:System.Drawing.Text.InstalledFontCollection> 컴퓨터에 설치 된 글꼴을 열거 하는 개체입니다. 합니다 <xref:System.Drawing.Text.FontCollection.Families%2A> 의 속성을 <xref:System.Drawing.Text.InstalledFontCollection> 개체의 배열이 <xref:System.Drawing.FontFamily> 개체입니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 컴퓨터에 설치 하는 모든 글꼴 패밀리 이름을 나열 합니다. 코드를 검색 합니다 <xref:System.Drawing.FontFamily.Name%2A> 의 각 속성 <xref:System.Drawing.FontFamily> 반환한 배열의 개체에에서는 <xref:System.Drawing.Text.FontCollection.Families%2A> 속성. 제품군 이름 검색은 쉼표로 구분 된 형식 목록에 연결 합니다. 그런 다음 <xref:System.Drawing.Graphics.DrawString%2A> 메서드는 <xref:System.Drawing.Graphics> 클래스 쉼표로 구분 된 목록 사각형을 그립니다.  
  
 예제 코드를 실행 하는 경우 다음 그림에 나와 있는 것과 비슷한 출력이 됩니다.  
  
 ![설치 된 글꼴 패밀리를 보여주는 스크린샷.](./media/how-to-enumerate-installed-fonts/list-installed-font-families.png)  
  
 [!code-csharp[System.Drawing.FontsAndText#11](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.FontsAndText/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.FontsAndText#11](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.FontsAndText/VB/Class1.vb#11)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 앞의 예제는 Windows Forms에서 사용 하도록 설계 되었으며 필요 <xref:System.Windows.Forms.PaintEventArgs> `e`의 매개 변수인 <xref:System.Windows.Forms.PaintEventHandler>합니다. 또한 가져와야는 <xref:System.Drawing.Text> 네임 스페이스입니다.  
  
## <a name="see-also"></a>참고자료
- [글꼴 및 텍스트 사용](using-fonts-and-text.md)
