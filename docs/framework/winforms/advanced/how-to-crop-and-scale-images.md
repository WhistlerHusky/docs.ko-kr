---
title: '방법: 자르기 및 배율 이미지'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- images [Windows Forms], cropping
- images [Windows Forms], scaling
ms.assetid: 053e3360-bca0-4b25-9afa-0e77a6f17b03
ms.openlocfilehash: ff0567dca0fd86736e02a9dd827ec15df8bf2df8
ms.sourcegitcommit: 15ab532fd5e1f8073a4b678922d93b68b521bfa0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2019
ms.locfileid: "58654499"
---
# <a name="how-to-crop-and-scale-images"></a>방법: 자르기 및 배율 이미지
합니다 <xref:System.Drawing.Graphics> 클래스에는 일부의 <xref:System.Drawing.Graphics.DrawImage%2A> 메서드 중 일부는 자르기 및 배율 이미지를 사용할 수 있는 원본 및 대상 사각형 매개 변수가 있습니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 <xref:System.Drawing.Image> 있는 Apple.gif 디스크 파일에서 개체입니다. 코드 전체 사과 이미지를 원래 크기로 그립니다. 코드를 호출 합니다 <xref:System.Drawing.Graphics.DrawImage%2A> 메서드를 <xref:System.Drawing.Graphics> 원래 apple 이미지 보다 큰 대상 사각형의 apple 이미지 부분을 그릴 개체.  
  
 <xref:System.Drawing.Graphics.DrawImage%2A> 메서드 다섯 번째 및 여섯 번째 인수는 세 번째, 네 번째, 지정 된 소스 사각형을 확인 하 여 그릴 apple의 부분을 결정 합니다. 이 경우 apple 너비의 75% 및 높이의 75%로 잘립니다.  
  
 <xref:System.Drawing.Graphics.DrawImage%2A> 메서드 자른된 apple를 그릴 위치와는 자른된 apple 대상 사각형을 보면 하도록 크기를 결정 두 번째 인수로 지정 합니다. 이 경우 대상 사각형은 30% 더 광범위 한 및 높이가 원본 이미지 보다 30%입니다.  
  
 다음 그림은 원래 apple 및 확장을 잘라 나타냅니다.  
  
 ![원래 이미지 및 이미지는 동일한 스크린샷.](./media/how-to-crop-and-scale-images/original-image-cropped-image.png)  
  
 [!code-csharp[System.Drawing.WorkingWithImages#11](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.WorkingWithImages#11](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/VB/Class1.vb#11)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 앞의 예제는 Windows forms에서 사용하도록 설계되었으며 <xref:System.Windows.Forms.Control.Paint> 이벤트 처리기의 매개 변수인 <xref:System.Windows.Forms.PaintEventArgs> `e`가 필요합니다. 바꿔야 `Apple.gif` 있는 이미지 파일 이름 및 경로 시스템에서 사용할 수 있는 합니다.  
  
## <a name="see-also"></a>참고자료
- [이미지, 비트맵 및 메타파일](images-bitmaps-and-metafiles.md)
- [이미지, 비트맵, 아이콘 및 메타파일 사용](working-with-images-bitmaps-icons-and-metafiles.md)
