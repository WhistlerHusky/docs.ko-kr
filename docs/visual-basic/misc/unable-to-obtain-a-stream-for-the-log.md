---
title: 로그에 대한 스트림을 가져올 수 없습니다.
ms.date: 07/20/2015
f1_keywords:
- vbrApplicationLog_ExhaustedPossibleStreamNames
ms.assetid: 33994f52-8efb-4790-a459-033e5c1db632
ms.openlocfilehash: 45b7a16608bea4879e84fa7004097a8c38312284
ms.sourcegitcommit: 5c1abeec15fbddcc7dbaa729fabc1f1f29f12045
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2019
ms.locfileid: "58031704"
---
# <a name="unable-to-obtain-a-stream-for-the-log"></a>로그에 대한 스트림을 가져올 수 없습니다.
로그에 대한 스트림을 가져올 수 없습니다. 에 기반한 파일 이름이 \<이름 >에서 이미 사용 중인 합니다.  
  
 합니다 <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener> 모든 잠재적 로그 파일 이름을 기반으로 하므로 클래스 새 로그 파일을 만들지 못했습니다 \<이름 >에서 이미 사용 중인 합니다.  
  
 로그 파일이 너무 많으면 애플리케이션의 아키텍처 문제를 나타낼 수도 있습니다. 자세한 내용은 <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener> 클래스에 대한 설명서를 참조하세요.  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
1.  <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener.LogFileCreationSchedule%2A> 속성을 <xref:Microsoft.VisualBasic.Logging.LogFileCreationScheduleOption.Daily> 또는 <xref:Microsoft.VisualBasic.Logging.LogFileCreationScheduleOption.Weekly> 로 설정하여 로그 파일 이름에 날짜 스탬프를 포함합니다.  
  
2.  <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener> 개체가 새 로그를 만들 수 있도록 기존 로그를 보관하고 컴퓨터에서 제거합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener>
- <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener.LogFileCreationSchedule%2A>
- [My.Application.Log](xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.Log)
- [My.Application.Info.DirectoryPath](xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.Log)
