---
title: 注釈の概要
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- highlights [WPF]
- documents [WPF], annotations
- sticky notes [WPF]
ms.assetid: 716bf474-29bd-4c74-84a4-8e0744bdad62
ms.openlocfilehash: 861a757effee8d68d1e41682dd91ffadba20c536
ms.sourcegitcommit: 30a83efb57c468da74e9e218de26cf88d3254597
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/20/2019
ms.locfileid: "68364380"
---
# <a name="annotations-overview"></a>注釈の概要
用紙にメモやコメントを書くことは普通の行為であり、人はそれを当たり前のことと思っています。 そのようなメモやコメントが "注釈" です。注釈をドキュメントに追加することで情報に目印を付け、興味のある内容を強調表示し、後で参照します。 印刷したドキュメントにメモを書くことは簡単で一般的な行為ですが、電子ドキュメントに個人的なコメントを追加する機能は利用できるとしても一般的に非常に限定されています。  
  
 このトピックでは、いくつかの一般的な種類の注釈 (特に付箋と強調表示) について説明します。また、Microsoft Annotations フレームワークが Windows Presentation Foundation を通じてアプリケーションでこれらの種類の注釈を容易にする方法を示します (WPF) ドキュメントの表示コントロール。  [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]注釈をサポートするドキュメント表示コントロール<xref:System.Windows.Controls.FlowDocumentReader>に<xref:System.Windows.Controls.FlowDocumentScrollViewer>は、および、 <xref:System.Windows.Controls.DocumentViewer>および<xref:System.Windows.Controls.FlowDocumentPageViewer>などの<xref:System.Windows.Controls.Primitives.DocumentViewerBase>から派生したコントロールが含まれます。  

<a name="caf1_type_stickynotes"></a>   
## <a name="sticky-notes"></a>付箋  
 典型的な付箋とは、色の付いた小さな紙切れに情報を記入し、書類に "貼り付ける" というものです。 デジタル付箋は電子ドキュメントのために同様の機能を提供しますが、さまざまなコンテンツを追加できるという柔軟性があります。タイプしたテキスト、手書きのメモ ([!INCLUDE[TLA#tla_tpc](../../../../includes/tlasharptla-tpc-md.md)] の "インク" ストロークなど)、Web リンクなどです。  
  
 次の図では、蛍光ペン、テキスト付箋、インク付箋で注釈を付けていることを確認できます。  
  
 ![蛍光ペン、テキスト付箋、インク付箋による注釈](./media/caf-stickynote.jpg "CAF_StickyNote")  
  
 次は、アプリケーションで注釈サポートを有効にするためのメソッドのサンプルです。  
  
 [!code-csharp[DocViewerAnnotationsXml#DocViewXmlStartAnnotations](~/samples/snippets/csharp/VS_Snippets_Wpf/DocViewerAnnotationsXml/CSharp/Window1.xaml.cs#docviewxmlstartannotations)]
 [!code-vb[DocViewerAnnotationsXml#DocViewXmlStartAnnotations](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DocViewerAnnotationsXml/visualbasic/window1.xaml.vb#docviewxmlstartannotations)]  
  
<a name="caf1_type_callouts"></a>   
## <a name="highlights"></a>強調表示  
 書面であれば、下線を引いたり、蛍光ペンでなぞったり、ドキュメント内の単語を囲んだり、余白に目印や注釈を付けたりするなど、さまざまな方法で書き込みを行い、興味のある項目を目立たせることができます。  Microsoft annotations Framework の注釈を強調表示すると、ドキュメント表示コントロールに[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]表示される情報をマークするための同様の機能が提供されます。  
  
 次の図は、注釈の強調表示のサンプルです。  
  
 ![注釈の強調表示](./media/caf-callouts.png "CAF_Callouts")  
  
 通常、ユーザーは、最初にテキストまたは目的の項目を選択し、右クリックして注釈の<xref:System.Windows.Controls.ContextMenu>オプションのを表示することで、注釈を作成します。  次の例は、 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]ユーザーが注釈を作成および<xref:System.Windows.Controls.ContextMenu>管理するためにアクセスできるルーティングコマンドを使用してを宣言するために使用できるを示しています。  
  
 [!code-xaml[DocViewerAnnotationsXps#CreateDeleteAnnotations](~/samples/snippets/csharp/VS_Snippets_Wpf/DocViewerAnnotationsXps/CSharp/Window1.xaml#createdeleteannotations)]  
  
<a name="caf1_framework_data_anchoring"></a>   
## <a name="data-anchoring"></a>データの固定  
 注釈フレームワークは、表示ビュー上の位置だけではなく、ユーザーが選択したデータに注釈をバインドします。 そのため、スクロールしたり、表示ウィンドウのサイズを変更したりするなど、ドキュメントの表示が変わっても、注釈はそれが固定されているデータにとどまります。 たとえば、次の図をご覧ください。選択したテキストが蛍光ペンでなぞられています。 ドキュメントの表示が変わると (スクロール、サイズ変更、拡大/縮小、その他の移動)、蛍光ペンは元のデータ選択と一緒に移動します。  
  
 ![注釈データ固定](./media/caf-dataanchoring.png "CAF_DataAnchoring")  
  
<a name="matching_annotations_with_annotated_objects"></a>   
## <a name="matching-annotations-with-annotated-objects"></a>注釈と注釈付きオブジェクトを照合する  
 注釈とそれに対応する注釈付きオブジェクトを照合できます。 たとえば、コメント ウィンドウが付いている単純なドキュメント リーダー アプリケーションを想像してください。 そのコメント ウィンドウにはリスト ボックスがあり、そのリスト ボックスに、ドキュメントに固定されている注釈の一覧からのテキストが表示されます。 リスト ボックスの項目を選択すると、それに対応する注釈オブジェクトが固定されている段落がドキュメントに表示されます。  
  
 次の例を見ると、コメント ウィンドウとして機能するそのようなリスト ボックスのイベント ハンドラーの実装方法がわかります。  
  
 [!code-csharp[FlowDocumentAnnotatedViewer#Handler](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentAnnotatedViewer/CSharp/Window1.xaml.cs#handler)]
 [!code-vb[FlowDocumentAnnotatedViewer#Handler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDocumentAnnotatedViewer/visualbasic/window1.xaml.vb#handler)]  
  
 もう1つのシナリオ例では、電子メールを使用してドキュメントリーダー間で注釈と付箋を交換できるアプリケーションが含まれています。 そのような機能を利用すると、交換された注釈を含むページにドキュメント リーダーで移動できます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.Primitives.DocumentViewerBase>
- <xref:System.Windows.Controls.DocumentViewer>
- <xref:System.Windows.Controls.FlowDocumentPageViewer>
- <xref:System.Windows.Controls.FlowDocumentScrollViewer>
- <xref:System.Windows.Controls.FlowDocumentReader>
- <xref:System.Windows.Annotations.IAnchorInfo>
- [注釈スキーマ](annotations-schema.md)
- [ContextMenu の概要](../controls/contextmenu-overview.md)
- [コマンド実行の概要](commanding-overview.md)
- [フロー ドキュメントの概要](flow-document-overview.md)
- [方法: MenuItem にコマンドを追加する](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms741839(v=vs.90))
