---
title: Windows Forms 컨트롤에서 속성 정의
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- properties [Windows Forms], defining in code
- custom controls [Windows Forms], defining properties in code
ms.assetid: c2eb8277-a842-4d99-89a9-647b901a0434
ms.openlocfilehash: 84273d2fab36df287eaca70f5f32fd8024a9204d
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/09/2019
ms.locfileid: "57712203"
---
# <a name="defining-a-property-in-windows-forms-controls"></a>Windows Forms 컨트롤에서 속성 정의
속성의 개요는 [속성 개요](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/65zdfbdt(v=vs.120))를 참조하세요. 속성을 정의할 때 다음과 같은 몇 가지 주요 고려 사항이 있습니다.  
  
-   정의한 속성에 특성을 적용해야 합니다. 특성은 디자이너가 속성을 표시하는 방법을 지정합니다. 자세한 내용은 [구성 요소의 디자인 타임 특성](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/tk67c2t8(v=vs.120))을 참조하세요.  
  
-   컨트롤의 시각적 표시에 영향을 주는 속성을 변경 하는 경우 호출 된 <xref:System.Windows.Forms.Control.Invalidate%2A> 메서드 (컨트롤에서 상속 되는 <xref:System.Windows.Forms.Control>)에서 `set` 접근자입니다. <xref:System.Windows.Forms.Control.Invalidate%2A> 호출 된 <xref:System.Windows.Forms.Control.OnPaint%2A> 메서드는 컨트롤을 다시 그립니다. 여러 번 호출 <xref:System.Windows.Forms.Control.Invalidate%2A> 에 대 한 단일 호출에서 결과 <xref:System.Windows.Forms.Control.OnPaint%2A> 효율성에 대 한 합니다.  
  
-   .NET Framework 클래스 라이브러리는 정수, 10진수 숫자, 부울 값 등과 같은 일반적인 데이터 형식에 대해 형식 변환기를 제공합니다. 형식 변환기의 목적은 일반적으로 문자열을 값으로 변환하도록 제공합니다(문자열 데이터에서 다른 데이터 형식으로). 일반적인 데이터 형식은 값을 문자열로 변환하고 문자열을 적절한 데이터 형식으로 변환하는 기본 형식 변환기와 연결됩니다. 사용자 지정(즉, 비표준) 데이터 형식인 속성을 정의하는 경우 형식 변환기를 지정하는 특성을 적용하여 해당 속성과 연결해야 합니다. 특성을 사용하여 사용자 지정 UI 형식 편집기를 속성과 연결할 수 있습니다. UI 형식 편집기는 속성이나 데이터 형식을 편집하는 사용자 인터페이스를 제공합니다. 색 선택은 UI 형식 편집기의 예입니다. 이 항목의 끝에 특성의 예가 제공됩니다.  
  
    > [!NOTE]
    >  사용자 지정 속성에 형식 변환기 또는 UI 형식 편집기를 사용할 수 없는 경우 [디자인 타임 지원 확장](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/37899azc(v=vs.120))에 설명된 대로 구현할 수 있습니다.  
  
 다음 코드 조각은 사용자 지정 컨트롤 `FlashTrackBar`에 대해 `EndColor`이라는 사용자 지정 속성을 정의합니다.  
  
```vb  
Public Class FlashTrackBar  
   Inherits Control  
   ...  
   ' Private data member that backs the EndColor property.  
   Private _endColor As Color = Color.LimeGreen  
  
   ' The Category attribute tells the designer to display  
   ' it in the Flash grouping.   
   ' The Description attribute provides a description of  
   ' the property.   
   <Category("Flash"), _  
   Description("The ending color of the bar.")>  _  
   Public Property EndColor() As Color  
      ' The public property EndColor accesses _endColor.  
      Get  
         Return _endColor  
      End Get  
      Set  
         _endColor = value  
         If Not (baseBackground Is Nothing) And showGradient Then  
            baseBackground.Dispose()  
            baseBackground = Nothing  
         End If  
         ' The Invalidate method calls the OnPaint method, which redraws    
         ' the control.  
         Invalidate()  
      End Set  
   End Property  
   ...  
End Class  
```  
  
```csharp  
public class FlashTrackBar : Control {  
   ...  
   // Private data member that backs the EndColor property.  
   private Color endColor = Color.LimeGreen;  
   // The Category attribute tells the designer to display  
   // it in the Flash grouping.   
   // The Description attribute provides a description of  
   // the property.   
   [  
   Category("Flash"),  
   Description("The ending color of the bar.")  
   ]  
   // The public property EndColor accesses endColor.  
   public Color EndColor {  
      get {  
         return endColor;  
      }  
      set {  
         endColor = value;  
         if (baseBackground != null && showGradient) {  
            baseBackground.Dispose();  
            baseBackground = null;  
         }  
         // The Invalidate method calls the OnPaint method, which redraws   
         // the control.  
         Invalidate();  
      }  
   }  
   ...  
}  
```  
  
 다음 코드 조각은 형식 변환기 및 UI 형식 편집기를 속성 `Value`과 연결합니다. 이 예제의 `Value` 는 정수 이며 기본 형식 변환기가 있지만 <xref:System.ComponentModel.TypeConverterAttribute> 사용자 지정 형식 변환기를 적용 하는 특성 (`FlashTrackBarValueConverter`) 디자이너가 백분율로 표시할 수 있도록 하는. UI 형식 편집기인 `FlashTrackBarValueEditor`은 백분율을 시각적으로 표시할 수 있습니다. 또한 보여 주는이 예제는 형식 변환기 또는 편집기에서 지정한 합니다 <xref:System.ComponentModel.TypeConverterAttribute> 또는 <xref:System.ComponentModel.EditorAttribute> 특성 기본 변환기를 재정의 합니다.  
  
```vb  
<Category("Flash"), _  
TypeConverter(GetType(FlashTrackBarValueConverter)), _  
Editor(GetType(FlashTrackBarValueEditor), _  
GetType(UITypeEditor)), _  
Description("The current value of the track bar.  You can enter an actual value or a percentage.")>  _  
Public ReadOnly Property Value() As Integer  
...  
End Property  
```  
  
```csharp  
[  
Category("Flash"),   
TypeConverter(typeof(FlashTrackBarValueConverter)),  
Editor(typeof(FlashTrackBarValueEditor), typeof(UITypeEditor)),  
Description("The current value of the track bar.  You can enter an actual value or a percentage.")  
]  
public int Value {  
...  
}  
```  
  
## <a name="see-also"></a>참고자료
- [Windows Forms 컨트롤의 속성](properties-in-windows-forms-controls.md)
- [ShouldSerialize 및 Reset 메서드를 사용하여 기본값 정의](defining-default-values-with-the-shouldserialize-and-reset-methods.md)
- [속성 변경 이벤트](property-changed-events.md)
- [Windows Forms 컨트롤의 특성](attributes-in-windows-forms-controls.md)
