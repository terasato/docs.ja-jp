---
title: '方法 : ScrollViewer のコンテンツ スクロール メソッドを使用する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- IScrollInfo interface [WPF]
- scrolling methods [WPF]
- ScrollViewer control [WPF], scrolling methods
ms.assetid: 4708cc65-6510-45f8-82e6-30b0d3e30045
ms.openlocfilehash: b4da666934be7dd182838d870e54e496b2646901
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
ms.locfileid: "33552767"
---
# <a name="how-to-use-the-content-scrolling-methods-of-scrollviewer"></a>方法 : ScrollViewer のコンテンツ スクロール メソッドを使用する
この例は、<xref:System.Windows.Controls.ScrollViewer>のスクロール メソッドを使用する方法を示しています。これらのメソッドにより、<xref:System.Windows.Controls.ScrollViewer>内のコンテンツを、行毎あるいはページ毎に、段階的にスクロールできます。  
  
## <a name="example"></a>例  
 次の例では、`sv1`という名前の<xref:System.Windows.Controls.ScrollViewer>を作成し、<xref:System.Windows.Controls.TextBlock>要素をホストさせています。<xref:System.Windows.Controls.TextBlock>は親である<xref:System.Windows.Controls.ScrollViewer>よりも大きいので、スクロールを有効にするためにスクロール バーが表示されます。様々なスクロール方法を表す<xref:System.Windows.Controls.Button>要素が，独立した<xref:System.Windows.Controls.StackPanel>に格納されて左側にドッキングされています。[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]内の各<xref:System.Windows.Controls.Button>は、<xref:System.Windows.Controls.ScrollViewer>内のスクロールの挙動をコントロールする，関連したカスタムメソッドを呼び出します。
  
 [!code-xaml[ScrollViewerMethods#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ScrollViewerMethods/CSharp/Window1.xaml#1)]  
  
 次の例では、<xref:System.Windows.Controls.ScrollViewer.LineUp%2A>と<xref:System.Windows.Controls.ScrollViewer.LineDown%2A>メソッドを使用します。
 
 [!code-csharp[ScrollViewerMethods#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ScrollViewerMethods/CSharp/Window1.xaml.cs#2)]
 [!code-vb[ScrollViewerMethods#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ScrollViewerMethods/VisualBasic/Window1.xaml.vb#2)]  
  
## <a name="see-also"></a>関連項目  
 <xref:System.Windows.Controls.ScrollViewer>  
 <xref:System.Windows.Controls.StackPanel>
