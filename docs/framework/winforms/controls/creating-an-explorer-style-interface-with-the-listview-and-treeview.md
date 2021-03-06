---
title: '연습: ListView 및 TreeView 컨트롤이 디자이너를 사용 하 여 된 탐색기 스타일 인터페이스 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Explorer-style applications [Windows Forms], walkthroughs
- TreeView control [Windows Forms], ListView controls used with
- ListView control [Windows Forms], TreeView controls used with
- Explorer-style applications
- TreeView control [Windows Forms], using for explorer-style interface
- ListView control [Windows Forms], explorer style interface
- ListView control [Windows Forms], explorer-style interface
ms.assetid: 9e5e7721-19e2-4890-b273-a43589fe99ff
ms.openlocfilehash: a849eae086c3507bbaf7050afd2e0496ab5a970e
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/09/2019
ms.locfileid: "57716987"
---
# <a name="walkthrough-creating-an-explorer-style-interface-with-the-listview-and-treeview-controls-using-the-designer"></a>연습: ListView 및 TreeView 컨트롤이 디자이너를 사용 하 여 된 탐색기 스타일 인터페이스 만들기
Visual Studio의 이점 중 하나는 짧은 시간 안에 전문적으로 보이는 Windows Forms 응용 프로그램을 만들 수 있습니다. 일반적인 시나리오를 사용 하 여 사용자 인터페이스 (UI)를 만드는 것 <xref:System.Windows.Forms.ListView> 및 <xref:System.Windows.Forms.TreeView> 와 비슷한 Windows 운영 체제의 Windows 탐색기 기능을 제어 합니다. Windows 탐색기는 사용자의 컴퓨터에서 파일 및 폴더의 계층 구조를 표시합니다.  
  
> [!NOTE]
>  표시되는 대화 상자와 메뉴 명령은 활성 설정이나 버전에 따라 도움말에서 설명하는 것과 다를 수 있습니다. 설정을 변경하려면 **도구** 메뉴에서 **설정 가져오기 및 내보내기** 를 선택합니다. 자세한 내용은 [Visual Studio IDE 개인 설정](/visualstudio/ide/personalizing-the-visual-studio-ide)을 참조하세요.  
  
### <a name="to-create-the-form-containing-a-listview-and-treeview-control"></a>ListView 및 TreeView 컨트롤이 포함 된 폼을 만들려면  
  
1.  **파일** 메뉴에서 **새로 만들기**를 가리킨 다음 **프로젝트**를 클릭합니다.  
  
2.  에 **새 프로젝트** 대화 상자에서 다음을 수행 합니다.  
  
    1.  범주를 선택 하거나 **Visual Basic** 하거나 **Visual C#** 합니다.  
  
    2.  템플릿 목록에서 선택 **Windows Forms 응용 프로그램**합니다.  
  
3.  **확인**을 클릭합니다. 새 Windows Forms 프로젝트가 생성 됩니다.  
  
4.  추가 된 <xref:System.Windows.Forms.SplitContainer> 컨트롤을 폼 및 설정 해당 <xref:System.Windows.Forms.SplitContainer.Dock%2A> 속성을 <xref:System.Windows.Forms.DockStyle.Fill>입니다.  
  
5.  추가 <xref:System.Windows.Forms.ImageList> 라는 `imageList1` 폼을 사용 하 여 두 개의 이미지를 추가 하려면 속성 창: 폴더 이미지 및 문서 이미지를 지정 된 순서로 합니다.  
  
6.  추가 <xref:System.Windows.Forms.TreeView> 라는 컨트롤 `treeview1` 폼에 왼쪽에 배치 하 고는 <xref:System.Windows.Forms.SplitContainer> 컨트롤입니다. 에 대 한 속성 창의 `treeView1` 다음을 수행 합니다.  
  
    1.  <xref:System.Windows.Forms.Control.Dock%2A> 속성을 <xref:System.Windows.Forms.DockStyle.Fill>으로 설정합니다.  
  
    2.  <xref:System.Windows.Forms.TreeView.ImageList%2A> 속성을 `imagelist1.`로 설정합니다.  
  
7.  추가 <xref:System.Windows.Forms.ListView> 라는 컨트롤 `listView1` 폼에 오른쪽에 놓습니다는 <xref:System.Windows.Forms.SplitContainer> 제어 합니다. 에 대 한 속성 창의 `listview1` 다음을 수행 합니다.  
  
    1.  <xref:System.Windows.Forms.Control.Dock%2A> 속성을 <xref:System.Windows.Forms.DockStyle.Fill>으로 설정합니다.  
  
    2.  <xref:System.Windows.Forms.ListView.View%2A> 속성을 <xref:System.Windows.Forms.View.Details>으로 설정합니다.  
  
    3.  줄임표를 클릭 하 여 ColumnHeader 컬렉션 편집기를 엽니다 (![VisualStudioEllipsesButton 스크린 샷](../media/vbellipsesbutton.png "vbEllipsesButton"))에 <xref:System.Windows.Forms.ListView.Columns%2A> 속성**합니다.** 세 개의 열을 추가 하 고 설정 자신의 <xref:System.Windows.Forms.ColumnHeader.Text%2A> 속성을 `Name`를 `Type`, 및 `Last Modified`, 각각. **확인** 을 클릭하여 대화 상자를 닫습니다.  
  
    4.  <xref:System.Windows.Forms.ListView.SmallImageList%2A> 속성을 `imageList1.`로 설정합니다.  
  
8.  채우는 코드를 구현 합니다 <xref:System.Windows.Forms.TreeView> 노드 및 하위 노드를 사용 하 여 합니다. 이 코드를 추가 하 여 `Form1` 클래스입니다.  
  
     [!code-csharp[System.Windows.Forms.ExplorerStyleInterface#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/CS/Form1.cs#1)]
     [!code-vb[System.Windows.Forms.ExplorerStyleInterface#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/VB/Form1.vb#1)]  
  
9. System.IO 네임 스페이스를 사용 하는 이전 코드를 적절 한 사용 하 여 추가 되거나 폼의 맨 위에 있는 문을 가져옵니다.  
  
     [!code-csharp[System.Windows.Forms.ExplorerStyleInterface#4](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/CS/Form1.cs#4)]
     [!code-vb[System.Windows.Forms.ExplorerStyleInterface#4](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/VB/Form1.vb#4)]  
  
10. 폼의 생성자에서 이전 단계에서 설정 메서드를 호출 하거나 <xref:System.Windows.Forms.Form.Load> 이벤트 처리 메서드. 폼 생성자에이 코드를 추가 합니다.  
  
     [!code-csharp[System.Windows.Forms.ExplorerStyleInterface#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.ExplorerStyleInterface#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/VB/Form1.vb#2)]  
  
11. 처리를 <xref:System.Windows.Forms.TreeView.NodeMouseClick> 이벤트에 대 한 `treeview1` **를** 채우는 코드를 구현 하 고 `listview1` 노드를 클릭할 때 노드 콘텐츠를 사용 하 여 합니다. 이 코드를 추가 하 여 `Form1` 클래스입니다.  
  
     [!code-csharp[System.Windows.Forms.ExplorerStyleInterface#3](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.ExplorerStyleInterface#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/VB/Form1.vb#3)]  
  
     C#을 사용 하는 경우 했는지 확인 합니다 <xref:System.Windows.Forms.TreeView.NodeMouseClick> 해당 이벤트 처리 메서드를 사용 하 여 연결 된 이벤트입니다. 폼 생성자에이 코드를 추가 합니다.  
  
     [!code-csharp[System.Windows.Forms.ExplorerStyleInterface#5](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/CS/Form1.cs#5)]  
  
## <a name="testing-the-application"></a>애플리케이션 테스트  
 이제 예상 대로 작동 되도록 폼을 테스트할 수 있습니다.  
  
#### <a name="to-test-the-form"></a>폼을 테스트 하려면  
  
-   F5 키를 눌러 애플리케이션을 실행합니다.  
  
     포함 된 분할 폼 표시 됩니다는 <xref:System.Windows.Forms.TreeView> 왼쪽에 프로젝트 디렉터리를 표시 하는 컨트롤 및 <xref:System.Windows.Forms.ListView> 오른쪽에 있는 세 개의 열을 사용 하 여 제어 합니다. 이동할 수는 <xref:System.Windows.Forms.TreeView> directory 노드를 선택 하 여 및 <xref:System.Windows.Forms.ListView> 선택한 디렉터리의 내용으로 채워집니다.  
  
## <a name="next-steps"></a>다음 단계  
 이 응용 프로그램 사용할 수 있습니다 하는 방법의 예를 제공 <xref:System.Windows.Forms.TreeView> 고 <xref:System.Windows.Forms.ListView> 함께 제어 합니다. 이러한 컨트롤에 대 한 자세한 내용은 다음 항목을 참조 하세요.  
  
-   [방법: TreeView 또는 ListView 컨트롤 (Windows Forms)에 사용자 지정 정보 추가](add-custom-information-to-a-treeview-or-listview-control-wf.md)  
  
-   [방법: ListView 컨트롤에 검색 기능 추가](how-to-add-search-capabilities-to-a-listview-control.md)  
  
-   [방법: TreeView 노드에 바로 가기 메뉴 연결](how-to-attach-a-shortcut-menu-to-a-treeview-node.md)  
  
## <a name="see-also"></a>참고자료
- <xref:System.Windows.Forms.ListView>
- <xref:System.Windows.Forms.TreeView>
- [ListView 컨트롤](listview-control-windows-forms.md)
- [방법: 추가 하 고 Windows Forms TreeView 컨트롤을 사용 하 여 노드를 제거 합니다.](how-to-add-and-remove-nodes-with-the-windows-forms-treeview-control.md)
- [방법: Windows Forms ListView 컨트롤을 사용 하 여 항목 추가 및 제거](how-to-add-and-remove-items-with-the-windows-forms-listview-control.md)
- [방법: Windows Forms ListView 컨트롤에 열 추가](how-to-add-columns-to-the-windows-forms-listview-control.md)
