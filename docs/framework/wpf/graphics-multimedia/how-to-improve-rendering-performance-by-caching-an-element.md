---
title: '방법: 요소를 캐시 하 여 렌더링 성능 향상'
ms.date: 03/30/2017
helpviewer_keywords:
- rendering performance [WPF], caching an element
- BitmapCache [WPF], improving rendering performance
- CacheMode [WPF], improving rendering performance
- performance [WPF], caching an element
- UIElement [WPF], caching
ms.assetid: 4739c1fc-60ba-4c46-aba6-f6c1a2688f19
ms.openlocfilehash: b5e39541fdf031b19e9e74483c0de94295e788d7
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57375227"
---
# <a name="how-to-improve-rendering-performance-by-caching-an-element"></a>방법: 요소를 캐시 하 여 렌더링 성능 향상
사용 된 <xref:System.Windows.Media.BitmapCache> 복잡 한의 렌더링 성능을 개선 하기 위해 클래스 <xref:System.Windows.UIElement>합니다. 새 인스턴스를 만들고 요소를 캐시 하려면 합니다 <xref:System.Windows.Media.BitmapCache> 클래스 및 요소에 할당할 <xref:System.Windows.UIElement.CacheMode%2A> 속성입니다. 다시 사용할 수 있습니다는 <xref:System.Windows.Media.BitmapCache> 효과적으로 <xref:System.Windows.Media.BitmapCacheBrush>합니다.  
  
## <a name="example"></a>예제  
 다음 코드 예제는 복잡 한 요소를 만들고 요소에 애니메이션이 적용 되어 때 성능을 향상 시킵니다 비트맵으로 캐시 하는 방법을 보여 줍니다. 꼭 짓 점 수를 사용 하 여 기 하 도형을 포함 하는 캔버스입니다. <xref:System.Windows.Media.BitmapCache> 이며 기본값은 값을 할당할는 <xref:System.Windows.UIElement.CacheMode%2A> 캔버스의 애니메이션 캐시 된 비트맵의 부드러운 크기 조정을 보여 줍니다.  
  
 [!code-xaml[System.Windows.Media.BitmapCache#_BitmapCacheXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/system.windows.media.bitmapcache/cs/window1.xaml#_bitmapcachexaml)]  
  
## <a name="see-also"></a>참고자료
- <xref:System.Windows.Media.BitmapCache>
- <xref:System.Windows.Media.BitmapCacheBrush>
- <xref:System.Windows.UIElement.CacheMode%2A>
- [방법: 캐시 된 요소를 브러시로 사용](how-to-use-a-cached-element-as-a-brush.md)
