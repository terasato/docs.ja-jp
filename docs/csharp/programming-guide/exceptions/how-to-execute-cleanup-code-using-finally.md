---
title: '方法: finally を使用してクリーンアップ コードを実行する - C# プログラミング ガイド'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- try/finally blocks [C#]
- exceptions [C#], try/finally block
- exception handling [C#], try/finally block
ms.assetid: 1b1e5aef-3f32-4a88-9d39-b5fffb33bdaf
ms.openlocfilehash: 0ec661e5fb0e13eaf8c3c8e4a7b274ab58853f58
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/28/2019
ms.locfileid: "56978086"
---
# <a name="how-to-execute-cleanup-code-using-finally-c-programming-guide"></a>方法: finally を使用してクリーンアップ コードを実行する (C# プログラミング ガイド)
`finally` ステートメントの目的は、例外がスローされた場合でも、オブジェクト (一般に外部リソースを保持しているオブジェクト) に対して必要なクリーンアップをすぐに実行できるようにすることです。 次のように、共通言語ランタイムによってオブジェクトがガベージ コレクションされるまで待機するのではなく、オブジェクトを使用した後すぐに <xref:System.IO.FileStream> で <xref:System.IO.Stream.Close%2A> を呼び出すというのも、このようなクリーンアップの一例です。  
  
 [!code-csharp[csProgGuideExceptions#16](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideExceptions/CS/Exceptions.cs#16)]  
  
## <a name="example"></a>例  
 上のコードを `try-catch-finally` ステートメントに変えるには、次のようにクリーンアップ コードを作業コードから切り離します。  
  
 [!code-csharp[csProgGuideExceptions#17](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideExceptions/CS/Exceptions.cs#17)]  
  
 `try` ブロック内では `OpenWrite()` 呼び出しの前のどの時点でも例外が発生する可能性があります。また、`OpenWrite()` 呼び出し自体が失敗する可能性もあります。そのため、ファイルを閉じようとしたときに、そのファイルが開いているという保証はありません。 `finally` ブロックでは、<xref:System.IO.Stream.Close%2A> メソッドを呼び出す前に、<xref:System.IO.FileStream> オブジェクトが `null` でないことを確認するチェックが追加されます。 この `null` チェックがないと、`finally` ブロックからその <xref:System.NullReferenceException> がスローされる可能性がありますが、`finally` ブロックにおける例外のスローはできるだけ回避する必要があります。  
  
 データベース接続も、`finally` ブロックで閉じられる対象になります。 データベース サーバーで許可される接続数は限られていることがあるため、データベース接続はできるだけ早く閉じる必要があります。 接続を閉じる前に例外がスローされる場合も、ガベージ コレクションを待機するより、`finally` ブロックを使用することをお勧めします。  
  
## <a name="see-also"></a>関連項目

- [C# プログラミング ガイド](../../../csharp/programming-guide/index.md)
- [例外と例外処理](../../../csharp/programming-guide/exceptions/index.md)
- [例外処理](../../../csharp/programming-guide/exceptions/exception-handling.md)
- [using ステートメント](../../../csharp/language-reference/keywords/using-statement.md)
- [try-catch](../../../csharp/language-reference/keywords/try-catch.md)
- [try-finally](../../../csharp/language-reference/keywords/try-finally.md)
- [try-catch-finally](../../../csharp/language-reference/keywords/try-catch-finally.md)
