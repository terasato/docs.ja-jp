---
title: '方法: コントロールの名前空間プレフィックス (Visual Basic) (LINQ to XML)'
ms.date: 07/20/2015
ms.assetid: 2fcf28a5-31b6-409d-84ea-27c22f71fc9f
ms.openlocfilehash: 2b89b49aa76df526c08143cad49685386ffd5e7c
ms.sourcegitcommit: eb9ff6f364cde6f11322e03800d8f5ce302f3c73
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/01/2019
ms.locfileid: "68709818"
---
# <a name="how-to-control-namespace-prefixes-visual-basic-linq-to-xml"></a>方法: コントロールの名前空間プレフィックス (Visual Basic) (LINQ to XML)
このトピックでは、名前空間プレフィックスを制御する方法について説明します。  
  
## <a name="example"></a>例  
  
### <a name="description"></a>説明  
 この例では、2 つの名前空間を宣言します。 `http://www.adventure-works.com`名前空間に`aw`プレフィックス`fc`があり、名前空間のプレフィックスがであることを指定します。 `www.fourthcoffee.com`  
  
### <a name="code"></a>コード  
  
```vb  
Imports <xmlns:aw="http://www.adventure-works.com">  
Imports <xmlns:fc="www.fourthcoffee.com">  
  
Module Module1  
  
    Sub Main()  
        Dim root As XElement = _  
            <aw:Root>  
                <fc:Child>  
                    <aw:DifferentChild>other content</aw:DifferentChild>  
                </fc:Child>  
                <aw:Child2>c2 content</aw:Child2>  
                <fc:Child3>c3 content</fc:Child3>  
            </aw:Root>  
        Console.WriteLine(root)  
    End Sub  
  
End Module  
```  
  
### <a name="comments"></a>コメント  
 この例を実行すると、次の出力が生成されます。  
  
```xml  
<aw:Root xmlns:fc="www.fourthcoffee.com" xmlns:aw="http://www.adventure-works.com">  
  <fc:Child>  
    <aw:DifferentChild>other content</aw:DifferentChild>  
  </fc:Child>  
  <aw:Child2>c2 content</aw:Child2>  
  <fc:Child3>c3 content</fc:Child3>  
</aw:Root>  
```  
  
## <a name="see-also"></a>関連項目

- [名前空間の概要 (LINQ to XML) (Visual Basic)](namespaces-overview-linq-to-xml.md)
