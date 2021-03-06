---
title: '방법: Windows Forms ListView 컨트롤에 대 한 아이콘을 표시 합니다.'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ListView control [Windows Forms], displaying icons
- icons [Windows Forms], displaying for ListView controls
- lists [Windows Forms], displaying icons
- ImageList component [Windows Forms], with ListView control
- list views [Windows Forms], displaying icons
ms.assetid: 9d577542-8595-429b-99e5-078770ec9d35
ms.openlocfilehash: ab515da932a4c73410e6ef22bec5ba8af200f270
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/09/2019
ms.locfileid: "57704483"
---
# <a name="how-to-display-icons-for-the-windows-forms-listview-control"></a>방법: Windows Forms ListView 컨트롤에 대 한 아이콘을 표시 합니다.
Windows Forms <xref:System.Windows.Forms.ListView> 컨트롤 3 개 이미지 목록에서 아이콘을 표시할 수 있습니다. 목록, 세부 정보 및 SmallIcon 보기에 지정 된 이미지 목록의 이미지에 표시 된 <xref:System.Windows.Forms.ListView.SmallImageList%2A> 속성입니다. 큰 아이콘 보기에 지정 된 이미지 목록의 이미지를 표시 합니다 <xref:System.Windows.Forms.ListView.LargeImageList%2A> 속성입니다. 목록 보기에서 설정 아이콘의 추가 집합을 표시할 수도 있습니다는 <xref:System.Windows.Forms.ListView.StateImageList%2A> 크고 작은 아이콘과 옆에 있는 속성입니다. 이미지 목록에 대 한 자세한 내용은 참조 하세요. [ImageList 구성 요소](imagelist-component-windows-forms.md) 고 [방법: 제거 이미지는 Windows Forms ImageList 구성 요소 추가 또는](how-to-add-or-remove-images-with-the-windows-forms-imagelist-component.md)합니다.  
  
### <a name="to-display-images-in-a-list-view"></a>목록 보기에 이미지를 표시 하려면  
  
1.  적절 한 속성을 설정-<xref:System.Windows.Forms.ListView.SmallImageList%2A>, <xref:System.Windows.Forms.ListView.LargeImageList%2A>, 또는 <xref:System.Windows.Forms.ListView.StateImageList%2A>-기존 <xref:System.Windows.Forms.ImageList> 사용 하려는 구성 요소입니다.  
  
     속성 창 사용 하 여 디자이너에서 또는 코드에서 이러한 속성을 설정할 수 있습니다.  
  
     [!code-csharp[System.Windows.Forms.ListViewLegacyTopics#41](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/CS/Class1.cs#41)]
     [!code-vb[System.Windows.Forms.ListViewLegacyTopics#41](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/VB/Class1.vb#41)]  
  
2.  설정 된 <xref:System.Windows.Forms.ListViewItem.ImageIndex%2A> 또는 <xref:System.Windows.Forms.ListViewItem.StateImageIndex%2A> 연결된 아이콘이 포함 된 각 목록 항목의 속성입니다.  
  
     또는 코드에서 이러한 속성을 설정할 수는 **ListViewItem 컬렉션 편집기**합니다. 열려는 합니다 **ListViewItem 컬렉션 편집기**, 줄임표 단추를 클릭 (![VisualStudioEllipsesButton 스크린 샷](../media/vbellipsesbutton.png "vbEllipsesButton"))는 옆에있는<xref:System.Windows.Forms.ListView.Items%2A>속성을 **속성** 창입니다.  
  
     [!code-csharp[System.Windows.Forms.ListViewLegacyTopics#42](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/CS/Class1.cs#42)]
     [!code-vb[System.Windows.Forms.ListViewLegacyTopics#42](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/VB/Class1.vb#42)]  
  
## <a name="see-also"></a>참고자료
- [ListView 컨트롤 개요](listview-control-overview-windows-forms.md)
- [방법: Windows Forms ListView 컨트롤을 사용 하 여 항목 추가 및 제거](how-to-add-and-remove-items-with-the-windows-forms-listview-control.md)
- [방법: Windows Forms ListView 컨트롤에 열 추가](how-to-add-columns-to-the-windows-forms-listview-control.md)
- [방법: TreeView 또는 ListView 컨트롤 (Windows Forms)에 사용자 지정 정보 추가](add-custom-information-to-a-treeview-or-listview-control-wf.md)
- [ImageList 구성 요소](imagelist-component-windows-forms.md)
