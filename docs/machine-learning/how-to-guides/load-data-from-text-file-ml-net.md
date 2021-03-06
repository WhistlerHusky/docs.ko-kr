---
title: 기계 학습 처리를 위해 텍스트 파일에서 데이터 로드 - ML.NET
description: ML.NET를 통해 기계 학습 모델을 빌드하고, 학습시키고, 점수 매기는 데 사용할 데이터를 텍스트 파일에서 로드하는 방법 알아보기
ms.date: 03/05/2019
ms.custom: mvc,how-to
ms.openlocfilehash: 14b1f8c99da6f1b8da436d9afef5b2ac8d36ecae
ms.sourcegitcommit: 16aefeb2d265e69c0d80967580365fabf0c5d39a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/18/2019
ms.locfileid: "57843371"
---
# <a name="load-data-from-a-text-file-for-machine-learning-processing---mlnet"></a>기계 학습 처리를 위해 텍스트 파일에서 데이터 로드 - ML.NET

> [!NOTE]
> 이 항목은 현재 미리 보기로 제공되는 ML.NET을 참조하며, 자료는 변경될 수 있습니다. 자세한 내용은 [ML.NET 소개](https://www.microsoft.com/net/learn/apps/machine-learning-and-ai/ml-dotnet)를 참조하세요.

이 방법과 관련 샘플에서는 현재 **ML.NET 버전 0.10**을 사용하고 있습니다. 자세한 내용은 [dotnet/machinelearning GitHub 리포지토리](https://github.com/dotnet/machinelearning/tree/master/docs/release-notes)에서 릴리스 정보를 참조하세요.

`TextLoader`는 텍스트 파일에서 데이터를 로드하는 데 사용됩니다. 데이터 열, 열 형식 및 텍스트 파일에서 해당 위치를 지정해야 합니다.

파일의 일부 열을 읽거나 동일한 열을 여러 번 읽어도 됩니다.

[예제 파일](https://github.com/dotnet/machinelearning/blob/master/test/data/adult.tiny.with-schema.txt):

<!-- markdownlint-disable MD010 -->
```console
Label   Workclass   education   marital-status
0   Private 11th    Never-married
0   Private HS-grad Married-civ-spouse
1   Local-gov   Assoc-acdm  Married-civ-spouse
1   Private Some-college    Married-civ-spouse
```
<!-- markdownlint-enable MD010 -->

텍스트 파일에서 데이터를 로드하려면

```csharp
// Create a new context for ML.NET operations. It can be used for exception tracking and logging,
// as a catalog of available operations and as the source of randomness.
var mlContext = new MLContext();

// Create the reader: define the data columns and where to find them in the text file.
var reader = mlContext.Data.CreateTextLoader(
    columns: new TextLoader.Column[]
    {
        // A boolean column depicting the 'target label'.
        new TextLoader.Column("IsOver50k",DataKind.BL,0),
        // Three text columns.
        new TextLoader.Column("WorkClass",DataKind.TX,1),
        new TextLoader.Column("Education",DataKind.TX,2),
        new TextLoader.Column("MaritalStatus",DataKind.TX,3)
    },
    hasHeader: true
);

// Now read the file (remember though, readers are lazy, so the actual reading will happen when the data is accessed).
var data = reader.Read(dataPath);
```
