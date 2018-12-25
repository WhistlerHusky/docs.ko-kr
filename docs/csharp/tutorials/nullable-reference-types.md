---
title: nullable 참조 형식을 사용하여 디자인
description: 이 고급 자습서에서는 nullable 참조 형식을 소개합니다. 참조 값이 null일 수 있는 경우에 대한 디자인 의도를 표현하고 컴파일러가 null일 수 없는 경우를 적용하게 하는 방법을 알아봅니다.
ms.date: 12/03/2018
ms.custom: mvc
ms.openlocfilehash: 7e4cb423658287e5260770a680f189c227b9cd01
ms.sourcegitcommit: ccd8c36b0d74d99291d41aceb14cf98d74dc9d2b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/10/2018
ms.locfileid: "53156691"
---
# <a name="tutorial-express-your-design-intent-more-clearly-with-nullable-and-non-nullable-reference-types"></a><span data-ttu-id="72200-104">자습서: nullable 참조 형식 및 nullable이 아닌 참조 형식을 사용하여 디자인 의도를 보다 명확하게 표현</span><span class="sxs-lookup"><span data-stu-id="72200-104">Tutorial: Express your design intent more clearly with nullable and non-nullable reference types</span></span>

<span data-ttu-id="72200-105">C# 8에서는 nullable 값 형식이 값 형식을 보완하는 것과 동일한 방식으로 참조 형식을 보완하는 **nullable 참조 형식**이 도입되었습니다.</span><span class="sxs-lookup"><span data-stu-id="72200-105">C# 8 introduces **nullable reference types**, which complement reference types the same way nullable value types complement value types.</span></span> <span data-ttu-id="72200-106">형식에 `?`를 추가하여 변수를 **nullable 참조 형식**으로 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-106">You declare a variable to be a **nullable reference type** by appending a `?` to the type.</span></span> <span data-ttu-id="72200-107">예를 들어 `string?`는 nullable `string`을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="72200-107">For example, `string?` represents a nullable `string`.</span></span> <span data-ttu-id="72200-108">이러한 새 형식을 사용하여 디자인 의도를 보다 명확하게 표현할 수 있습니다. ‘항상 값이 있어야 하는’ 변수도 있고, ‘값이 누락될 수 있는’ 변수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72200-108">You can use these new types to more clearly express your design intent: some variables *must always have a value*, others *may be missing a value*.</span></span>

<span data-ttu-id="72200-109">이 자습서에서는 다음과 같은 작업을 수행하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="72200-109">In this tutorial, you'll learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="72200-110">디자인에 nullable 참조 형식 및 nullable이 아닌 참조 형식 통합</span><span class="sxs-lookup"><span data-stu-id="72200-110">Incorporate nullable and non-nullable reference types into your designs</span></span>
> * <span data-ttu-id="72200-111">코드 전체에서 nullable 참조 형식 확인을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-111">Enable nullable reference type checks throughout your code.</span></span>
> * <span data-ttu-id="72200-112">컴파일러가 이러한 디자인 결정을 적용하는 코드를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-112">Write code where the compiler enforces those design decisions.</span></span>
> * <span data-ttu-id="72200-113">고유한 디자인에 nullable 참조 기능 사용</span><span class="sxs-lookup"><span data-stu-id="72200-113">Use the nullable reference feature in your own designs</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72200-114">전제 조건</span><span class="sxs-lookup"><span data-stu-id="72200-114">Prerequisites</span></span>

<span data-ttu-id="72200-115">C# 8.0 베타 컴파일러를 포함하여 .NET Core를 실행하도록 머신을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-115">You’ll need to set up your machine to run .NET Core, including the C# 8.0 beta compiler.</span></span> <span data-ttu-id="72200-116">C# 8 베타 컴파일러는 [Visual Studio 2019 Preview 1](https://visualstudio.microsoft.com/vs/preview/) 또는 [.NET Core 3.0 Preview 1](https://dotnet.microsoft.com/download/dotnet-core/3.0)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72200-116">The C# 8 beta compiler is available with [Visual Studio 2019 preview 1](https://visualstudio.microsoft.com/vs/preview/), or [.NET Core 3.0 preview 1](https://dotnet.microsoft.com/download/dotnet-core/3.0).</span></span>

<span data-ttu-id="72200-117">이 자습서에서는 Visual Studio 또는 .NET Core CLI를 포함하여 C# 및 .NET에 익숙하다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-117">This tutorial assumes you're familiar with C# and .NET, including either Visual Studio or the .NET Core CLI.</span></span>

## <a name="incorporate-nullable-reference-types-into-your-designs"></a><span data-ttu-id="72200-118">디자인에 nullable 참조 형식 통합</span><span class="sxs-lookup"><span data-stu-id="72200-118">Incorporate nullable reference types into your designs</span></span>

<span data-ttu-id="72200-119">이 자습서에서는 설문 조사 실행을 모델링하는 라이브러리를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-119">In this tutorial, you'll build a library that models running a survey.</span></span> <span data-ttu-id="72200-120">코드는 nullable 참조 형식 및 nullable이 아닌 참조 형식을 둘 다 사용하여 실제 세계의 개념을 표현합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-120">The code uses both nullable reference types and non-nullable reference types to represent the real-world concepts.</span></span> <span data-ttu-id="72200-121">설문 조사 질문은 null일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="72200-121">The survey questions can never be null.</span></span> <span data-ttu-id="72200-122">응답자는 질문에 응답하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72200-122">A respondent might prefer not to answer a question.</span></span> <span data-ttu-id="72200-123">이 경우 응답이 null일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72200-123">The responses might be null in this case.</span></span>

<span data-ttu-id="72200-124">이 샘플에 대해 작성하는 코드는 해당 의도를 표현하고 컴파일러가 의도를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-124">The code you'll write for this sample expresses that intent, and the compiler enforces that intent.</span></span>

## <a name="create-the-application-and-enable-nullable-reference-types"></a><span data-ttu-id="72200-125">애플리케이션을 만들고 nullable 참조 형식을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="72200-125">Create the application and enable nullable reference types</span></span>

<span data-ttu-id="72200-126">Visual Studio 또는 `dotnet new console`을 사용하여 명령줄에서 새로운 콘솔 애플리케이션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72200-126">Create a new console application either in Visual Studio or from the command line using `dotnet new console`.</span></span> <span data-ttu-id="72200-127">응용 프로그램 이름을 `NullableIntroduction`으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-127">Name the application `NullableIntroduction`.</span></span> <span data-ttu-id="72200-128">애플리케이션을 만든 후에는 C# 8 베타 기능을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-128">Once you've created the application, you'll need to enable C# 8 beta features.</span></span> <span data-ttu-id="72200-129">`csproj` 파일을 열고 `PropertyGroup` 요소에 `LangVersion` 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-129">Open the `csproj` file, and add a `LangVersion` element to the `PropertyGroup` element:</span></span>

```xml
<LangVersion>8.0</LangVersion>
```

<span data-ttu-id="72200-130">또는 Visual Studio 프로젝트 속성을 통해 C# 8을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72200-130">Alternatively, you can use the Visual Studio project properties to enable C# 8.</span></span> <span data-ttu-id="72200-131">솔루션 탐색기에서 프로젝트 노드를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-131">In Solution Explorer, right click on the project node, select **Properties**.</span></span> <span data-ttu-id="72200-132">**빌드** 탭을 선택하고 **고급...** 을 클릭합니다. 언어 버전 드롭다운에서 **C# 8.0(베타)** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-132">Then, select the **build** tab, and click **Advanced...**. In the dropdown for language version, select **C# 8.0 (beta)**.</span></span>

<span data-ttu-id="72200-133">C# 8 프로젝트에서도 **nullable 참조 형식** 기능을 옵트인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-133">You must opt into the **nullable reference types** feature, even in C# 8 projects.</span></span> <span data-ttu-id="72200-134">기능이 켜지고 나면 기존 참조 변수 선언이 **nullable이 아닌 참조 형식**으로 바뀌기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="72200-134">That's because once the feature is turned on, existing reference variable declarations become **non-nullable reference types**.</span></span> <span data-ttu-id="72200-135">이러한 의사 결정은 기존 코드에 적절한 null 확인이 없는 문제를 찾는 데 도움이 되지만 원래 디자인 의도를 정확하게 반영하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72200-135">While that decision will help find issues where existing code may not have proper null-checks, it may not accurately reflect your original design intent.</span></span> <span data-ttu-id="72200-136">새 pragma를 사용하여 기능을 켭니다.</span><span class="sxs-lookup"><span data-stu-id="72200-136">You turn on the feature with a new pragma:</span></span>

```csharp
#nullable enable
```

<span data-ttu-id="72200-137">소스 파일의 어디에나 앞의 pragma를 추가할 수 있으며, 해당 지점부터 nullable 참조 형식 기능이 켜집니다.</span><span class="sxs-lookup"><span data-stu-id="72200-137">You can add the preceding pragma anywhere in a source file, and the nullable reference type feature is turned on from that point.</span></span> <span data-ttu-id="72200-138">pragma는 기능을 끄는 `disable` 인수도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-138">The pragma also supports the `disable` argument to turn off the feature.</span></span>

<span data-ttu-id="72200-139">.csproj 파일에 다음 요소를 추가하여 전체 프로젝트에 대해 **nullable 참조 형식**을 켤 수도 있습니다. 예를 들어 C# 8.0을 사용하도록 설정한 `LangVersion` 요소 바로 다음에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-139">You can also turn on **nullable reference types** for an entire project by adding the following element to your .csproj file, for example, immediately following the `LangVersion` element that enabled C# 8.0:</span></span>

```xml
<NullableReferenceTypes>true</NullableReferenceTypes>
```

### <a name="design-the-types-for-the-application"></a><span data-ttu-id="72200-140">애플리케이션의 형식 디자인</span><span class="sxs-lookup"><span data-stu-id="72200-140">Design the types for the application</span></span>

<span data-ttu-id="72200-141">이 설문 조사 애플리케이션에서는 다음과 같은 많은 클래스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-141">This survey application requires creating a number of classes:</span></span>

- <span data-ttu-id="72200-142">질문 목록을 모델링하는 클래스</span><span class="sxs-lookup"><span data-stu-id="72200-142">A class that models the list of questions.</span></span>
- <span data-ttu-id="72200-143">설문 조사를 위해 연락한 사람 목록을 모델링하는 클래스</span><span class="sxs-lookup"><span data-stu-id="72200-143">A class that models a list of people contacted for the survey.</span></span>
- <span data-ttu-id="72200-144">설문 조사를 수행한 사람의 응답을 모델링하는 클래스</span><span class="sxs-lookup"><span data-stu-id="72200-144">A class that models the answers from a person that took the survey.</span></span>

<span data-ttu-id="72200-145">이러한 형식은 nullable 참조 형식 및 nullable이 아닌 참조 형식을 둘 다 사용하여 필수 멤버가 선택적 멤버를 표현합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-145">These types will make use of both nullable and non-nullable reference types to express which members are required and which members are optional.</span></span> <span data-ttu-id="72200-146">nullable 참조 형식은 해당 디자인 의도를 명확하게 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-146">Nullable reference types communicate that design intent clearly:</span></span>

- <span data-ttu-id="72200-147">설문 조사의 일부인 질문은 null일 수 없습니다. 빈 질문을 하는 것은 타당하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="72200-147">The questions that are part of the survey can never be null: It makes no sense to ask an empty question.</span></span>
- <span data-ttu-id="72200-148">응답자는 null일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="72200-148">The respondents can never be null.</span></span> <span data-ttu-id="72200-149">참여를 거부한 응답자를 포함하여 연락한 사람을 추적하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="72200-149">You'll want to track people you contacted, even respondents that declined to participate.</span></span>
- <span data-ttu-id="72200-150">질문에 대한 응답은 null일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72200-150">Any response to a question may be null.</span></span> <span data-ttu-id="72200-151">응답자는 일부 또는 모든 질문에 대한 응답을 거부할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72200-151">Respondents can decline to answer some or all questions.</span></span>

<span data-ttu-id="72200-152">C#으로 프로그래밍한 경우 null 값을 허용하는 참조 형식에 익숙해서 nullable이 아닌 인스턴스로 선언할 기회를 놓쳤을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72200-152">If you've programmed in C#, you may be so accustomed to reference types that allow null values that you may have missed other opportunities to declare non-nullable instances:</span></span>

- <span data-ttu-id="72200-153">질문 컬렉션은 nullable이 아니어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-153">The collection of questions should be non-nullable.</span></span>
- <span data-ttu-id="72200-154">응답자 컬렉션은 nullable이 아니어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-154">The collection of respondents should be non-nullable.</span></span>

<span data-ttu-id="72200-155">코드를 작성할 때 nullable이 아닌 참조 형식을 참조의 기본값으로 사용하면 null 참조 예외를 발생시킬 수 있는 일반적인 실수를 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72200-155">As you write the code, you'll see that a non-nullable reference type as the default for references avoids common mistakes that could lead to null reference exceptions.</span></span> <span data-ttu-id="72200-156">이 자습서에서 배운 한 가지 교훈은 null일 수 있는 변수와 null일 수 없는 변수를 결정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="72200-156">One lesson from this tutorial is that you made decisions about which variables could or could not be null.</span></span> <span data-ttu-id="72200-157">이러한 결정을 표현하는 구문은 언어에서 제공하지 않았지만</span><span class="sxs-lookup"><span data-stu-id="72200-157">The language didn't provide syntax to express those decisions.</span></span> <span data-ttu-id="72200-158">이제 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-158">Now it does.</span></span>

<span data-ttu-id="72200-159">빌드하는 앱은 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-159">The app you'll build will do the following steps:</span></span>

1. <span data-ttu-id="72200-160">설문 조사를 만들고 질문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-160">Create a survey and add questions to it.</span></span>
1. <span data-ttu-id="72200-161">설문 조사 응답자의 의사 임의 세트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72200-161">Create a pseudo-random set of respondents for the survey.</span></span>
1. <span data-ttu-id="72200-162">완료된 설문 조사 크기가 목표 수치에 도달할 때까지 응답자에게 연락합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-162">Contact respondents until the completed survey size reaches the goal number.</span></span>
1. <span data-ttu-id="72200-163">설문 조사 응답에 대한 중요한 통계를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-163">Write out important statistics on the survey responses.</span></span>

## <a name="build-the-survey-with-nullable-and-non-nullable-types"></a><span data-ttu-id="72200-164">nullable 형식과 nullable이 아닌 형식을 사용하여 설문 조사 작성</span><span class="sxs-lookup"><span data-stu-id="72200-164">Build the survey with nullable and non-nullable types</span></span>

<span data-ttu-id="72200-165">작성하는 첫 번째 코드에서 설문 조사를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72200-165">The first code you'll write creates the survey.</span></span> <span data-ttu-id="72200-166">설문 조사 질문과 설문 조사 실행을 모델링하는 클래스를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-166">You'll write classes to model a survey question and a survey run.</span></span> <span data-ttu-id="72200-167">설문 조사에는 응답 형식(예/아니요 응답, 숫자 응답, 텍스트 응답)으로 구분되는 세 가지 질문 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72200-167">Your survey has three types of questions, distinguished by the format of the answer: Yes/No answers, number answers, and text answers.</span></span> <span data-ttu-id="72200-168">`public` `SurveyQuestion` 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72200-168">Create a `public` `SurveyQuestion` class.</span></span> <span data-ttu-id="72200-169">`using` 문 바로 뒤에 `#nullable enable` pragma를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-169">Include the `#nullable enable` pragma immediately after the `using` statements:</span></span>

```csharp
#nullable enable
namespace NullableIntroduction
{
    public class SurveyQuestion
    {
    }
}
```

<span data-ttu-id="72200-170">`#nullable enable` pragma를 추가하면 컴파일러가 모든 참조 형식 변수 선언을 **nullable이 아닌** 참조 형식으로 해석합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-170">Adding the `#nullable enable` pragma means the compiler interprets every reference type variable declaration as a **non-nullable** reference type.</span></span> <span data-ttu-id="72200-171">다음 코드에 표시된 대로 질문 텍스트 및 질문 유형의 속성을 추가하여 첫 번째 경고를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72200-171">You can see your first warning by adding properties for the question text and the type of question, as shown in the following code:</span></span>

```csharp
#nullable enable
namespace NullableIntroduction
{
    public enum QuestionType
    {
        YesNo,
        Number,
        Text
    }

    public class SurveyQuestion
    {
        public string QuestionText { get; }
        public QuestionType TypeOfQuestion { get; }
    }
}
```

<span data-ttu-id="72200-172">`QuestionText`를 초기화하지 않았기 때문에 컴파일러에서 nullable이 아닌 속성이 초기화되지 않았다는 경고를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-172">Because you haven't initialized `QuestionText`, the compiler issues a warning that a non-nullable property hasn't been initialized.</span></span> <span data-ttu-id="72200-173">디자인에 따라 질문 텍스트는 null이 아니어야 하므로 초기화할 생성자와 `QuestionType` 값도 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-173">Your design requires the question text to be non-null, so you add a constructor to initialize it and the `QuestionType` value as well.</span></span> <span data-ttu-id="72200-174">완성된 클래스 정의는 다음 코드와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="72200-174">The finished class definition looks like the following code:</span></span>

[!code-csharp[DefineQuestion](../../../samples/csharp/NullableIntroduction/NullableIntroduction/SurveyQuestion.cs)]

<span data-ttu-id="72200-175">생성자를 추가하면 경고가 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="72200-175">Adding the constructor removes the warning.</span></span> <span data-ttu-id="72200-176">생성자 인수도 nullable이 아닌 참조 형식이므로 컴파일러에서 경고를 실행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="72200-176">The constructor argument is also a non-nullable reference type, so the compiler doesn't issue any warnings.</span></span>

<span data-ttu-id="72200-177">`SurveyRun`이라는 `public` 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72200-177">Next, create a `public` class named `SurveyRun`.</span></span> <span data-ttu-id="72200-178">`using` 문 다음에 `#nullable enable` pragma를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-178">Include the `#nullable enable` pragma following the `using` statements.</span></span> <span data-ttu-id="72200-179">이 클래스에는 다음 코드에 표시된 것처럼 설문 조사에 질문을 추가하는 메서드 및 `SurveyQuestion` 개체 목록이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72200-179">This class contains a list of `SurveyQuestion` objects and methods to add questions to the survey, as shown in the following code:</span></span>

```csharp
using System.Collections.Generic;

#nullable enable
namespace NullableIntroduction
{
    public class SurveyRun
    {
        private List<SurveyQuestion> surveyQuestions = new List<SurveyQuestion>();

        public void AddQuestion(QuestionType type, string question) =>
            AddQuestion(new SurveyQuestion(type, question));
        public void AddQuestion(SurveyQuestion surveyQuestion) => surveyQuestions.Add(surveyQuestion);
    }
}
```

<span data-ttu-id="72200-180">이전과 마찬가지로, 목록 개체를 null이 아닌 값으로 초기화해야 합니다. 초기화하지 않으면 컴파일러에서 경고를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-180">As before, you must initialize the list object to a non-null value or the compiler issues a warning.</span></span> <span data-ttu-id="72200-181">`AddQuestion`의 두 번째 오버로드에는 null 확인이 없습니다. 해당 변수를 nullable이 아닌 것으로 선언하여 필요하지 않기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="72200-181">There are no null checks in the second overload of `AddQuestion` because they aren't needed: You've declared that variable to be non-nullable.</span></span> <span data-ttu-id="72200-182">해당 값은 `null`일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72200-182">Its value can't be `null`.</span></span>

<span data-ttu-id="72200-183">편집기에서 `Program.cs`로 전환하고 `Main`의 내용을 다음 코드 줄로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="72200-183">Switch to `Program.cs` in your editor and replace the contents of `Main` with the following lines of code:</span></span>

[!code-csharp[AddQuestions](../../../samples/csharp/NullableIntroduction/NullableIntroduction/Program.cs#AddQuestions)]

<span data-ttu-id="72200-184">파일 맨 위에 `#nullable enable` pragma가 없으면 `AddQuestion` 인수의 텍스트로 `null`을 전달할 때 컴파일러에서 경고를 실행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="72200-184">Without the `#nullable enable` pragma at the top of the file, the compiler doesn't issue a warning when you pass `null` as the text for the `AddQuestion` argument.</span></span> <span data-ttu-id="72200-185">`using` 문 다음에 `#nullable enable`을 추가하여 코드를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-185">Fix that by adding `#nullable enable` following the `using` statement.</span></span> <span data-ttu-id="72200-186">다음 줄을 `Main`에 추가하여 시도해 보세요.</span><span class="sxs-lookup"><span data-stu-id="72200-186">Try it by adding the following line to `Main`:</span></span>

```csharp
surveyRun.AddQuestion(QuestionType.Text, default);
```

## <a name="create-respondents-and-get-answers-to-the-survey"></a><span data-ttu-id="72200-187">응답자를 만들고 설문 조사에 대한 응답 받기</span><span class="sxs-lookup"><span data-stu-id="72200-187">Create respondents and get answers to the survey</span></span>

<span data-ttu-id="72200-188">다음으로, 설문 조사에 대한 응답을 생성하는 코드를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-188">Next, write the code that generates answers to the survey.</span></span> <span data-ttu-id="72200-189">여기에는 다음과 같은 몇 개의 작은 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="72200-189">This involves several small tasks:</span></span>

1. <span data-ttu-id="72200-190">응답자 개체를 생성하는 메서드를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-190">Build a method that generates respondent objects.</span></span> <span data-ttu-id="72200-191">이러한 개체는 설문 조사를 작성하도록 요청된 사람을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="72200-191">These represent people asked to fill out the survey.</span></span>
1. <span data-ttu-id="72200-192">응답자에게 질문하고 응답을 수집하거나 응답자가 응답하지 않았음을 확인하는 과정을 시뮬레이션하는 논리를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-192">Build logic to simulate asking the questions to a respondent and collecting answers or noting that a respondent didn't answer.</span></span>
1. <span data-ttu-id="72200-193">충분한 응답자가 설문 조사에 응답할 때까지 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-193">Repeat until enough respondents have answered the survey.</span></span>

<span data-ttu-id="72200-194">설문 조사 응답을 나타낼 클래스가 필요하므로 지금 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-194">You'll need a class to represent a survey response, so add that now.</span></span> <span data-ttu-id="72200-195">nullable 지원을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-195">Enable nullable support.</span></span> <span data-ttu-id="72200-196">다음 코드에 표시된 대로 `Id` 속성 및 이 속성을 초기화하는 생성자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-196">Add an `Id` property and a constructor that initializes it, as shown in the following code:</span></span>

```csharp
#nullable enable
namespace NullableIntroduction
{
    public class SurveyResponse
    {
        public int Id { get; }

        public SurveyResponse(int id) => Id = id;
    }
}
```

<span data-ttu-id="72200-197">다음으로, `static` 메서드를 추가해서 임의 ID를 생성하여 새 참가자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="72200-197">Next, add a `static` method to create new participants by generating a random ID:</span></span>

[!code-csharp[GenerateRespondents](../../../samples/csharp/NullableIntroduction/NullableIntroduction/SurveyResponse.cs#Random)]

<span data-ttu-id="72200-198">이 클래스의 주요 책임은 설문 조사의 질문에 대한 참가자의 응답을 생성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="72200-198">The main responsibility of this class is to generate the responses for a participant to the questions in the survey.</span></span> <span data-ttu-id="72200-199">이 책임에는 몇 가지 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72200-199">This responsibility has a few steps:</span></span>

1. <span data-ttu-id="72200-200">설문 조사에 참여하도록 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-200">Ask for participation in the survey.</span></span> <span data-ttu-id="72200-201">개인이 동의하지 않을 경우 missing(또는 null) 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-201">If the person doesn't consent, return a missing (or null) response.</span></span>
1. <span data-ttu-id="72200-202">각 질문을 하고 응답을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-202">Ask each question and record the answer.</span></span> <span data-ttu-id="72200-203">각 응답도 missing(또는 null)일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72200-203">Each answer may also be missing (or null).</span></span>

<span data-ttu-id="72200-204">`SurveyRespondent` 클래스에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-204">Add the following code to your `SurveyRespondent` class:</span></span>

[!code-csharp[AnswerSurvey](../../../samples/csharp/NullableIntroduction/NullableIntroduction/SurveyResponse.cs#AnswerSurvey)]

<span data-ttu-id="72200-205">설문 조사 응답의 스토리지는 `Dictionary<int, string>?`로, null일 수 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="72200-205">The storage for the survey answers is a `Dictionary<int, string>?`, indicating that it may be null.</span></span> <span data-ttu-id="72200-206">새 언어 기능을 사용하여 컴파일러 및 나중에 코드를 읽는 모든 사람에게 디자인 의도를 선언하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72200-206">You're using the new language feature to declare your design intent, both to the compiler and to anyone reading your code later.</span></span> <span data-ttu-id="72200-207">먼저 null 값을 확인하지 않고 `surveyResponses`를 역참조하는 경우 컴파일러 경고가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="72200-207">If you ever dereference `surveyResponses` without checking for the null value first, you'll get a compiler warning.</span></span> <span data-ttu-id="72200-208">위에서 `surveyResponses` 변수가 null이 아닌 값으로 설정되었음을 컴파일러가 판별할 수 있으므로 `AnswerSurvey` 메서드에 경고가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="72200-208">You don't get a warning in the `AnswerSurvey` method because the compiler can determine the `surveyResponses` variable was set to a non-null value above.</span></span>

<span data-ttu-id="72200-209">다음으로, `SurveyRun` 클래스에 `PerformSurvey` 메서드를 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-209">Next, you need to write the `PerformSurvey` method in the `SurveyRun` class.</span></span> <span data-ttu-id="72200-210">`SurveyRun` 클래스에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-210">Add the following code in the `SurveyRun` class:</span></span>

[!code-csharp[PerformSurvey](../../../samples/csharp/NullableIntroduction/NullableIntroduction/SurveyRun.cs#PerformSurvey)]

<span data-ttu-id="72200-211">여기서 다시, nullable `List<SurveyResponse>?` 선택은 응답이 null일 수 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="72200-211">Here again, your choice of a nullable `List<SurveyResponse>?` indicates the response may be null.</span></span> <span data-ttu-id="72200-212">이는 설문 조사가 아직 어떠한 응답자에게도 제공되지 않았음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="72200-212">That indicates the survey hasn't been given to any respondents yet.</span></span> <span data-ttu-id="72200-213">충분한 응답자가 동의할 때까지 응답자가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="72200-213">Notice that respondents are added until enough have consented.</span></span>

<span data-ttu-id="72200-214">설문 조사를 실행하는 마지막 단계는 `Main` 메서드의 끝에 설문 조사를 수행할 호출을 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="72200-214">The last step to run the survey is to add a call to perform the survey at the end of the `Main` method:</span></span>

[!code-csharp[RunSurvey](../../../samples/csharp/NullableIntroduction/NullableIntroduction/Program.cs#RunSurvey)]

## <a name="examine-survey-responses"></a><span data-ttu-id="72200-215">설문 조사 응답 조사</span><span class="sxs-lookup"><span data-stu-id="72200-215">Examine survey responses</span></span>

<span data-ttu-id="72200-216">마지막 단계는 설문 조사 결과를 표시하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="72200-216">The last step is to display survey results.</span></span> <span data-ttu-id="72200-217">작성한 여러 클래스에 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-217">You'll add code to many of the classes you've written.</span></span> <span data-ttu-id="72200-218">이 코드는 nullable 참조 형식과 nullable이 아닌 참조 형식 구분의 가치를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="72200-218">This code demonstrates the value of distinguishing nullable and non-nullable reference types.</span></span> <span data-ttu-id="72200-219">먼저 다음 두 개의 식 본문 멤버를 `SurveyResponse` 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-219">Start by adding the following two expression-bodied members to the `SurveyResponse` class:</span></span>

[!code-csharp[ReportResponses](../../../samples/csharp/NullableIntroduction/NullableIntroduction/SurveyResponse.cs#SurveyStatus)]

<span data-ttu-id="72200-220">`surveyResponses`는 nullable이 아닌 참조 형식이므로 역참조하기 전에 확인할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="72200-220">Because `surveyResponses` is a non-nullable reference, type no checks are necessary before de-referencing it.</span></span> <span data-ttu-id="72200-221">`Answer` 메서드는 nullable이 아닌 문자열을 반환하므로 기본값으로 두 번째 인수를 사용하는 `GetValueOrDefault` 오버로드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-221">The `Answer` method returns a non-nullable string, so choose the overload of `GetValueOrDefault` that takes a second argument for the default value.</span></span>

<span data-ttu-id="72200-222">다음 세 개의 식 본문 멤버를 `SurveyRun` 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-222">Next, add these three expression-bodied members to the `SurveyRun` class:</span></span>

[!code-csharp[ReportResults](../../../samples/csharp/NullableIntroduction/NullableIntroduction/SurveyRun.cs#RunReport)]

<span data-ttu-id="72200-223">`respondents` 변수는 null일 수 있지만 반환 값은 null일 수 없음을 `AllParticipants` 멤버가 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-223">The `AllParticipants` member must take into account that the `respondents` variable might be null, but the return value can't be null.</span></span> <span data-ttu-id="72200-224">`??` 및 뒤에 오는 빈 시퀀스를 제거하여 해당 식을 변경하면 컴파일러에서 메서드가 `null`을 반환할 수 있고 해당 반환 시그니처가 nullable이 아닌 형식을 반환한다고 경고합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-224">If you change that expression by removing the `??` and the empty sequence that follows, the compiler warns you the method might return `null` and its return signature returns a non-nullable type.</span></span>

<span data-ttu-id="72200-225">마지막으로, `Main` 메서드의 맨 아래에 다음 루프를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-225">Finally, add the following loop at the bottom of the `Main` method:</span></span>

[!code-csharp[DisplaySurveyResults](../../../samples/csharp/NullableIntroduction/NullableIntroduction/Program.cs#WriteAnswers)]

<span data-ttu-id="72200-226">모두 nullable이 아닌 참조 형식을 반환하도록 기본 인터페이스를 디자인했기 때문에 이 코드에는 `null` 확인이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="72200-226">You don't need any `null` checks in this code because you've designed the underlying interfaces so that they all return non-nullable reference types.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="72200-227">코드 가져오기</span><span class="sxs-lookup"><span data-stu-id="72200-227">Get the code</span></span>

<span data-ttu-id="72200-228">[samples](https://github.com/dotnet/samples) 리포지토리의 [csharp/IntroToNullables](https://github.com/dotnet/samples/tree/master/csharp/NullableIntroduction) 폴더에서 완료된 자습서의 코드를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72200-228">You can get the code for the finished tutorial from our [samples](https://github.com/dotnet/samples) repository in the [csharp/IntroToNullables](https://github.com/dotnet/samples/tree/master/csharp/NullableIntroduction) folder.</span></span>

<span data-ttu-id="72200-229">nullable 참조 형식과 nullable이 아닌 참조 형식 간에 형식 선언을 변경하여 실험합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-229">Experiment by changing the type declarations between nullable and non-nullable reference types.</span></span> <span data-ttu-id="72200-230">실수로 `null`을 역참조하지 않도록 어떻게 다양한 경고를 생성하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="72200-230">See how that generates different warnings to ensure you don't accidentally dereference a `null`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="72200-231">다음 단계</span><span class="sxs-lookup"><span data-stu-id="72200-231">Next steps</span></span>

<span data-ttu-id="72200-232">nullable 참조 형식에 대한 개요를 읽고 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="72200-232">Learn more by reading an overview of nullable reference types..</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="72200-233">nullable 참조 개요</span><span class="sxs-lookup"><span data-stu-id="72200-233">An overview of nullable references</span></span>](../nullable-references.md)