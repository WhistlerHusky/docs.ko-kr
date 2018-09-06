---
title: 드라이브, 디렉터리 및 파일 처리(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- drives
- drives, processing
- Visual Basic code, file access
- files [Visual Basic], processing
- files [Visual Basic], accessing
- directories [Visual Studio], processing
ms.assetid: f1db14c8-a4fd-4d0b-8323-c7cb29d688c2
ms.openlocfilehash: 0c9c1c787138595f725316a580acda9c5d4d43a9
ms.sourcegitcommit: 3c1c3ba79895335ff3737934e39372555ca7d6d0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/05/2018
ms.locfileid: "43777566"
---
# <a name="processing-drives-directories-and-files-visual-basic"></a><span data-ttu-id="cc005-102">드라이브, 디렉터리 및 파일 처리(Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="cc005-102">Processing Drives, Directories, and Files (Visual Basic)</span></span>
<span data-ttu-id="cc005-103">Visual Basic을 사용하여 `My.Computer.FileSystem` 개체로 드라이브, 폴더 및 파일을 처리할 수 있습니다. `FileOpen` 및 `Write` 함수(여전히 사용할 수 있음)와 같은 기존 메서드보다 사용하기 쉬우며 더 나은 성능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cc005-103">You can use Visual Basic to process drives, folders, and files with the `My.Computer.FileSystem` object, which provides better performance and is easier to use than traditional methods such as the `FileOpen` and `Write` functions (although they are still available).</span></span> <span data-ttu-id="cc005-104">다음 섹션에서는 이러한 메서드에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="cc005-104">The following sections discuss these methods in detail.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="cc005-105">섹션 내용</span><span class="sxs-lookup"><span data-stu-id="cc005-105">In This Section</span></span>  
 [<span data-ttu-id="cc005-106">Visual Basic을 사용한 파일 액세스</span><span class="sxs-lookup"><span data-stu-id="cc005-106">File Access with Visual Basic</span></span>](../../../../visual-basic/developing-apps/programming/drives-directories-files/file-access.md)  
 <span data-ttu-id="cc005-107">`My.Computer.FileSystem` 개체를 파일, 드라이브 및 폴더 작업에 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="cc005-107">Discusses how to use the `My.Computer.FileSystem` object to work with files, drives, and folders.</span></span>  
  
 [<span data-ttu-id="cc005-108">.NET Framework 파일 I/O 및 파일 시스템의 기본 사항(Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="cc005-108">Basics of .NET Framework File I/O and the File System (Visual Basic)</span></span>](../../../../visual-basic/developing-apps/programming/drives-directories-files/basics-of-net-framework-file-io-and-the-file-system.md)  
 <span data-ttu-id="cc005-109">스트림, 격리된 저장소, 파일 이벤트, 파일 특성, 파일 액세스 등 .NET Framework의 파일 I/O 개념에 대해 개략적으로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="cc005-109">Provides an overview of file I/O concepts in the .NET Framework, including streams, isolated storage, file events, file attributes, and file access.</span></span>  
  
 [<span data-ttu-id="cc005-110">연습: .NET Framework 메서드를 사용하여 파일 조작</span><span class="sxs-lookup"><span data-stu-id="cc005-110">Walkthrough: Manipulating Files by Using .NET Framework Methods</span></span>](../../../../visual-basic/developing-apps/programming/drives-directories-files/walkthrough-manipulating-files-by-using-net-framework-methods.md)  
 <span data-ttu-id="cc005-111">[!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)]를 사용하여 파일 및 폴더를 조작하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="cc005-111">Demonstrates how to use the [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] to manipulate files and folders.</span></span>  
  
 [<span data-ttu-id="cc005-112">연습: Visual Basic에서 파일과 디렉터리 조작</span><span class="sxs-lookup"><span data-stu-id="cc005-112">Walkthrough: Manipulating Files and Directories in Visual Basic</span></span>](../../../../visual-basic/developing-apps/programming/drives-directories-files/walkthrough-manipulating-files-and-directories.md)  
 <span data-ttu-id="cc005-113">`My.Computer.FileSystem` 개체를 사용하여 파일 및 폴더를 조작하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="cc005-113">Demonstrates how to use the `My.Computer.FileSystem` object to manipulate files and folders.</span></span>  
  
## <a name="related-sections"></a><span data-ttu-id="cc005-114">관련 단원</span><span class="sxs-lookup"><span data-stu-id="cc005-114">Related Sections</span></span>  
 [<span data-ttu-id="cc005-115">프로그램 구조 및 코드 규칙</span><span class="sxs-lookup"><span data-stu-id="cc005-115">Program Structure and Code Conventions</span></span>](../../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)  
 <span data-ttu-id="cc005-116">프로그램의 물리적 구조와 모양에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cc005-116">Provides guidelines for the physical structure and appearance of programs.</span></span>  
  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem>  
 <span data-ttu-id="cc005-117">`My.Computer.FileSystem` 개체와 해당 멤버에 대한 참조 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="cc005-117">Reference documentation for the `My.Computer.FileSystem` object and its members.</span></span>