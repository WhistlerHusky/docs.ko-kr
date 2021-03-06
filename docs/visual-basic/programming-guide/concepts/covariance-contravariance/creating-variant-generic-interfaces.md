---
title: Variant 제네릭 인터페이스 만들기 (Visual Basic)
ms.date: 07/20/2015
ms.assetid: d4037dd2-dfe9-4811-9150-93d4e8b20113
ms.openlocfilehash: 45454f12cf49994f3d476a9ee27f72442266db65
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2019
ms.locfileid: "57673290"
---
# <a name="creating-variant-generic-interfaces-visual-basic"></a>Variant 제네릭 인터페이스 만들기 (Visual Basic)

인터페이스에서 제네릭 형식 매개 변수를 공변(covariant) 또는 반공변(contravariant)으로 선언할 수 있습니다. *공변성(covariance)* 은 인터페이스 메서드가 제네릭 형식 매개 변수에 정의된 것보다 더 많은 수의 파생된 반환 형식을 갖도록 허용합니다. *반공변성(contravariance)* 은 인터페이스 메서드가 제네릭 매개 변수에 지정된 것보다 더 적은 수의 파생된 형식의 인수 형식을 갖도록 허용합니다. 공변(covariant) 또는 반공변(contravariant) 제네릭 형식 매개 변수가 포함된 제네릭 인터페이스를 *variant*라고 합니다.

> [!NOTE]
> .NET Framework 4에서는 기존의 몇몇 제네릭 인터페이스에 대한 가변성 지원이 추가되었습니다. .NET Framework의 variant 인터페이스 목록은 참조 하세요 [(Visual Basic) 제네릭 인터페이스의 가변성](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-generic-interfaces.md)합니다.

## <a name="declaring-variant-generic-interfaces"></a>Variant 제네릭 인터페이스 선언

제네릭 형식 매개 변수에 `in` 및 `out` 키워드를 사용하여 Variant 제네릭 인터페이스를 선언할 수 있습니다.

> [!IMPORTANT]
> `ByRef` Visual Basic의 매개 변수는 variant 일 수 없습니다. 또한 값 형식은 가변성을 지원하지 않습니다.

`out` 키워드를 사용하여 제네릭 형식 매개 변수를 공변(covariant)으로 선언할 수 있습니다. 공변(covariant) 형식은 다음 조건을 충족해야 합니다.

- 형식은 인터페이스 메서드의 반환 형식으로만 사용되고 메서드 인수의 형식으로 사용되지 않습니다. 이 내용은 `R` 형식이 공변(covariant)으로 선언된 다음 예제에서 설명합니다.

    ```vb
    Interface ICovariant(Of Out R)
        Function GetSomething() As R
        ' The following statement generates a compiler error.
        ' Sub SetSomething(ByVal sampleArg As R)
    End Interface
    ```

    그러나 이 규칙에는 한 가지 예외가 있습니다. 반공변(contravariant) 제네릭 대리자가 메서드 매개 변수로 있는 경우 형식을 이 대리자에 대한 제네릭 형식 매개 변수로 사용할 수 있습니다. 다음 예제에서 `R` 형식을 통해 이를 확인할 수 있습니다. 자세한 내용은 [대리자의 가변성 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md) 하 고 [Func 및 Action 제네릭 대리자 (Visual Basic)를 사용 하 여 분산](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/using-variance-for-func-and-action-generic-delegates.md)합니다.

    ```vb
    Interface ICovariant(Of Out R)
        Sub DoSomething(ByVal callback As Action(Of R))
    End Interface
    ```

- 형식은 인터페이스 메서드에 대한 제네릭 제약 조건으로 사용되지 않습니다. 이는 다음 코드에 설명되어 있습니다.

    ```vb
    Interface ICovariant(Of Out R)
        ' The following statement generates a compiler error
        ' because you can use only contravariant or invariant types
        ' in generic constraints.
        ' Sub DoSomething(Of T As R)()
    End Interface
    ```

`in` 키워드를 사용하여 제네릭 형식 매개 변수를 반공변(contravariant)으로 선언할 수 있습니다. 반공변(contravariant) 형식은 메서드 인수의 형식으로서만 사용할 수 있으며 인터페이스 메서드의 반환 형식으로는 사용할 수 없습니다. 반공변(contravariant) 형식은 제네릭 제약 조건에 사용될 수도 있습니다. 다음 코드에서는 반공변(contravariant) 인터페이스를 선언하고 해당 메서드 중 하나에 제네릭 제약 조건을 사용하는 방법을 보여 줍니다.

```vb
Interface IContravariant(Of In A)
    Sub SetSomething(ByVal sampleArg As A)
    Sub DoSomething(Of T As A)()
    ' The following statement generates a compiler error.
    ' Function GetSomething() As A
End Interface
```

같은 인터페이스에서 그러나 서로 다른 형식 매개 변수에 대해 공변성(covariance) 및 반공변성(contravariance)을 모두 지원하는 것도 가능합니다.

```vb
Interface IVariant(Of Out R, In A)
    Function GetSomething() As R
    Sub SetSomething(ByVal sampleArg As A)
    Function GetSetSomething(ByVal sampleArg As A) As R
End Interface
```

Visual basic에서 대리자 형식을 지정 하지 않고 변형 인터페이스의 이벤트를 선언할 수 없습니다. 또한 variant 인터페이스를 클래스, 열거형 또는 구조를 중첩 있을 수 없습니다. 하지만 인터페이스 중첩 있을 수 있습니다. 이는 다음 코드에 설명되어 있습니다.

```vb
Interface ICovariant(Of Out R)
    ' The following statement generates a compiler error.
    ' Event SampleEvent()
    ' The following statement specifies the delegate type and
    ' does not generate an error.
    Event AnotherEvent As EventHandler

    ' The following statements generate compiler errors,
    ' because a variant interface cannot have
    ' nested enums, classes, or structures.

    'Enum SampleEnum : test : End Enum
    'Class SampleClass : End Class
    'Structure SampleStructure : Dim value As Integer : End Structure

    ' Variant interfaces can have nested interfaces.
    Interface INested : End Interface
End Interface
```

## <a name="implementing-variant-generic-interfaces"></a>Variant 제네릭 인터페이스 구현

고정(invariant) 인터페이스에 사용되는 같은 구문을 사용하여 클래스에서 Variant 제네릭 인터페이스를 구현합니다. 다음 코드 예제에서는 제네릭 클래스에서 공변(covariant) 인터페이스를 구현하는 방법을 보여 줍니다.

```vb
Interface ICovariant(Of Out R)
    Function GetSomething() As R
End Interface

Class SampleImplementation(Of R)
    Implements ICovariant(Of R)
    Public Function GetSomething() As R _
    Implements ICovariant(Of R).GetSomething
        ' Some code.
    End Function
End Class
```

Variant 인터페이스를 구현하는 클래스는 고정입니다. 예를 들어, 다음과 같은 코드를 생각해 볼 수 있습니다.

```vb
 The interface is covariant.
Dim ibutton As ICovariant(Of Button) =
    New SampleImplementation(Of Button)
Dim iobj As ICovariant(Of Object) = ibutton

' The class is invariant.
Dim button As SampleImplementation(Of Button) =
    New SampleImplementation(Of Button)
' The following statement generates a compiler error
' because classes are invariant.
' Dim obj As SampleImplementation(Of Object) = button
```

## <a name="extending-variant-generic-interfaces"></a>Variant 제네릭 인터페이스 확장

Variant 제네릭 인터페이스를 확장할 경우 `in` 및 `out` 키워드를 사용하여 파생 인터페이스가 가변성을 지원하는지 명시적으로 지정해야 합니다. 컴파일러에서는 확장되고 있는 인터페이스에서 가변성을 유추하지 않습니다. 예를 들어 다음 인터페이스를 살펴봅니다.

```vb
Interface ICovariant(Of Out T)
End Interface

Interface IInvariant(Of T)
    Inherits ICovariant(Of T)
End Interface

Interface IExtCovariant(Of Out T)
    Inherits ICovariant(Of T)
End Interface
```

에 `Invariant(Of T)` 인터페이스를 제네릭 형식 매개 변수 `T` 변형의 경우 아닙니다 반면에서 `IExtCovariant (Of Out T)`두 인터페이스 모두 동일한 인터페이스를 확장 하지만 형식 매개 변수는 공변 (covariant), 합니다. 반공변(contravariant) 제네릭 형식 매개 변수에는 같은 규칙이 적용됩니다.

제네릭 형식 매개 변수 `T`가 공변(covariant)인 인터페이스 및 확장 인터페이스에서 제네릭 형식 매개 변수 `T`가 고정인 경우 반공변(contravariant)인 인터페이스를 둘 다 확장하는 인터페이스를 만들 수 있습니다. 다음 코드 예제에서 이 내용을 보여 줍니다.

```vb
Interface ICovariant(Of Out T)
End Interface

Interface IContravariant(Of In T)
End Interface

Interface IInvariant(Of T)
    Inherits ICovariant(Of T), IContravariant(Of T)
End Interface
```

그러나 한 인터페이스에서 제네릭 형식 매개 변수 `T`가 공변(covariant)으로 선언되면 확장 인터페이스에서는 이 매개 변수를 반공변(contravariant)으로 선언할 수 없고, 반대의 경우도 마찬가지입니다. 다음 코드 예제에서 이 내용을 보여 줍니다.

```vb
Interface ICovariant(Of Out T)
End Interface

' The following statements generate a compiler error.
' Interface ICoContraVariant(Of In T)
'     Inherits ICovariant(Of T)
' End Interface
```

### <a name="avoiding-ambiguity"></a>모호성 방지

Variant 제네릭 인터페이스를 구현할 경우 가변성으로 인해 모호성이 나타나는 경우가 있습니다. 이러한 경우가 발생해서는 안 됩니다.

예를 들어 서로 다른 제네릭 형식 매개 변수가 포함된 같은 Variant 제네릭 인터페이스를 한 클래스에서 명시적으로 구현하면 모호성이 발생할 수 있습니다. 컴파일러에서는 이 경우 오류를 생성하지 않지만 런타임에 선택될 인터페이스 구현이 지정되지 않습니다. 이로 인해 코드에서 미묘한 버그가 발생할 수 있습니다. 다음 코드 예제를 살펴봅니다.

> [!NOTE]
> 사용 하 여 `Option Strict Off`, Visual Basic 모호한 인터페이스 구현을 때 컴파일러 경고를 생성 합니다. 사용 하 여 `Option Strict On`, Visual Basic 컴파일러 오류를 생성 합니다.

```vb
' Simple class hierarchy.
Class Animal
End Class

Class Cat
    Inherits Animal
End Class

Class Dog
    Inherits Animal
End Class

' This class introduces ambiguity
' because IEnumerable(Of Out T) is covariant.
Class Pets
    Implements IEnumerable(Of Cat), IEnumerable(Of Dog)

    Public Function GetEnumerator() As IEnumerator(Of Cat) _
        Implements IEnumerable(Of Cat).GetEnumerator
        Console.WriteLine("Cat")
        ' Some code.
    End Function

    Public Function GetEnumerator1() As IEnumerator(Of Dog) _
        Implements IEnumerable(Of Dog).GetEnumerator
        Console.WriteLine("Dog")
        ' Some code.
    End Function

    Public Function GetEnumerator2() As IEnumerator _
        Implements IEnumerable.GetEnumerator
        ' Some code.
    End Function
End Class

Sub Main()
    Dim pets As IEnumerable(Of Animal) = New Pets()
    pets.GetEnumerator()
End Sub
```

이 예제에서는 `pets.GetEnumerator` 메서드가 `Cat` 및 `Dog` 중에 선택하는 방법이 지정되어 있지 않습니다. 이로 인해 코드에서 문제가 발생할 수 있습니다.

## <a name="see-also"></a>참고자료

- [제네릭 인터페이스의 가변성(Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-generic-interfaces.md)
- [Func 및 Action 제네릭 대리자에 가변성 사용(Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/using-variance-for-func-and-action-generic-delegates.md)
