---
title: COM クラスの例 - C# プログラミング ガイド
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- examples [C#], COM classes
- COM, exposing Visual C# objects to
ms.assetid: 6504dea9-ad1c-4993-a794-830fec5270af
ms.openlocfilehash: d4ea445339057bc65c3597d30a46f46d58b6e696
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64595531"
---
# <a name="example-com-class-c-programming-guide"></a>COM クラスの例 (C# プログラミング ガイド)
ここでは、COM オブジェクトとして公開されるクラスの例を紹介します。 このコードを .cs ファイルに保存して、プロジェクトに追加したあと、**[COM の相互運用機能に登録]** プロパティを **[True]** に設定します。 詳細については、「[方法 :コンポーネントを COM 相互運用機能に登録する](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/w29wacsy(v=vs.100))」をご覧ください。
  
 Visual C# オブジェクトを COM に公開するには、クラス インターフェイス、イベント インターフェイス (必要な場合)、クラス自体を宣言する必要があります。 クラスのメンバーを COM で参照するには、次の規則に従う必要があります。  
  
- クラスはパブリックであること。  
  
- プロパティ、メソッド、およびイベントがパブリックであること。  
  
- プロパティとメソッドがクラス インターフェイスで宣言されていること。  
  
- イベントがイベント インターフェイスで宣言されていること。  
  
 これらのインターフェイスで宣言されていない、クラス内の他のパブリック メンバーは、COM から参照されませんが、他の .NET Framework オブジェクトからは参照されます。  
  
 プロパティとメソッドを COM に公開するには、それらをクラス インターフェイスで宣言し、`DispId` 属性でマークを付けて、クラスに実装する必要があります。 メンバーをインターフェイスで宣言する順序は、COM vtable で使用される順序になります。  
  
 クラスのイベントを公開するには、それらをイベント インターフェイスで宣言し、`DispId` 属性でマークを付ける必要があります。 クラスでこのインターフェイスを実装しないでください。  
  
 クラスでは、クラス インターフェイスが実装されます。複数のインターフェイスを実装できますが、最初に実装されるのは、既定のクラス インターフェイスです。 ここで、COM に対して公開するプロパティとメソッドを実装します。 プロパティとメソッドは、パブリックとしてマークされており、クラス インターフェイスの宣言と一致する必要があります。 また、ここでクラスから発生するイベントを宣言します。 イベントは、パブリックとしてマークされており、イベント インターフェイスの宣言と一致する必要があります。  
  
## <a name="example"></a>例  
 [!code-csharp[csProgGuideInterop#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInterop/CS/ExampleCOM.cs#8)]  
  
## <a name="see-also"></a>関連項目

- [C# プログラミング ガイド](../../../csharp/programming-guide/index.md)
- [相互運用性](../../../csharp/programming-guide/interop/index.md)
- [[ビルド] ページ (プロジェクト デザイナー) (C#)](/visualstudio/ide/reference/build-page-project-designer-csharp)
