---
title: 測定単位
description: どの浮動小数点をについて説明しますと F# の符号付き整数値には、測定単位を長さ、ボリューム、および大容量を示すために使用される通常を関連付けることができます。
ms.date: 05/16/2016
ms.openlocfilehash: f97eac9984f934c55aff8cf9f287afbc3aa098f3
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630161"
---
# <a name="units-of-measure"></a>測定単位

の浮動小数点と符号付きF#整数値には、長さ、ボリューム、質量などを示すために通常使用される測定単位を関連付けることができます。 単位付きの数量を使用することにより、コンパイラは、算術リレーションシップの単位が正しいことを確認できます。これにより、プログラミングエラーを防ぐことができます。

## <a name="syntax"></a>構文

```fsharp
[<Measure>] type unit-name [ = measure ]
```

## <a name="remarks"></a>Remarks

前の構文では、*単位名*を測定単位として定義しています。 省略可能な部分は、以前に定義した単位に基づいて新しいメジャーを定義するために使用されます。 たとえば、次の行では、メジャー `cm` (センチメートル) を定義しています。

```fsharp
[<Measure>] type cm
```

次の行では、 `ml`メジャー (milliliter) を3次 (`cm^3`) として定義しています。

```fsharp
[<Measure>] type ml = cm^3
```

前の構文では、 *measure*は単位を含む数式です。 単位が関係する数式では、整数の累乗がサポートされています (正と負)。単位間の`*`スペースは、2つの単位の`/`積、つまり単位の積を示すと同時に、単位の商を示します。 逆数単位の場合は、負の整数の累乗を使用するか`/` 、または単位の数式の分子と分母を区別するを使用できます。 分母に複数の単位を指定する場合は、かっこで囲む必要があります。 の`/`後のスペースで区切られた単位は、分母の一部として解釈され`*`ますが、の後に続く単位は、分子の一部として解釈されます。

1つの単位式で1を使用すると、dimensionless の数量を示すことも、分子などの他の単位と組み合わせて使用することもできます。 たとえば、レートの単位はとして`1/s`書き込まれます。ここ`s`で、は秒を示します。 かっこは、単位の数式では使用されません。 単位の数式で数値変換定数を指定することはできません。ただし、単位を個別に指定して変換定数を定義し、単位チェックされた計算で使用できます。

同じことを意味する単位の数式は、さまざまな方法で記述できます。 したがって、コンパイラは、単位の数式を一貫性のある形式に変換します。これにより、負の値が reciprocals に変換され、単位が1つの分子と分母にグループ化され、分子と分母の単位が alphabetizes されます。

たとえば、単位の数式`kg m s^-2`とは両方と`m /s s * kg`もに`kg m/s^2`変換されます。

浮動小数点式では測定単位を使用します。 浮動小数点数を関連する測定単位と共に使用すると、タイプセーフの別のレベルが追加され、弱く型指定された浮動小数点数を使用するときに、式で発生する可能性がある単位不一致エラーを回避するのに役立ちます。 単位を使用する浮動小数点式を記述する場合は、式の単位が一致している必要があります。

次の例に示すように、山かっこで囲まれた単位の数式でリテラルに注釈を付けることができます。

```fsharp
1.0<cm>
55.0<miles/hour>
```

数字と山かっこの間にスペースを入れないでください。ただし、次の例に示すように、 `f`などのリテラルサフィックスを含めることができます。

```fsharp
// The f indicates single-precision floating point.
55.0f<miles/hour>
```

このような注釈は、リテラルの型をプリミティブ型 (など`float`) から次元型`float<cm>` (この場合`float<miles/hour>`はなど) に変更します。 の`<1>`単位注釈は dimensionless quantity を示し、その型は、unit パラメーターを持たないプリミティブ型に相当します。

測定単位の型は、浮動小数点型または符号付き整数型であり、追加の単位注釈が角かっこで示されます。 したがって、変換の種類を (グラム) から`g` (キログラム) `kg`に記述する場合は、次のように型を記述します。

```fsharp
let convertg2kg (x : float<g>) = x / 1000.0<g/kg>
```

測定単位は、コンパイル時の単位チェックに使用されますが、実行時環境には保存されません。 そのため、パフォーマンスには影響しません。

測定単位は、浮動小数点型だけでなく、任意の型に適用できます。ただし、浮動小数点型、符号付き整数型、および10進数型のみが次元の数量をサポートします。 したがって、プリミティブ型と、これらのプリミティブ型を含む集計では、測定単位を使用するのが理にかなっています。

次の例は、測定単位の使用方法を示しています。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6901.fs)]

次のコード例は、dimensionless 浮動小数点数から次元浮動小数点値に変換する方法を示しています。 1\.0 で乗算するだけで、1.0 にディメンションが適用されます。 これは、のような`degreesFahrenheit`関数に要約できます。

また、dimensionless 浮動小数点数を予期する関数に次元値を渡す場合は、 `float` `float`演算子を使用して、その単位をキャンセルするか、にキャストする必要があります。 この例では、が`1.0<degC>` `printf` dimensionless 数量を想定して`printf`いるため、の引数としてをで除算します。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6902.fs)]

次のセッション例は、からの出力とこのコードへの入力を示しています。

```
Enter a temperature in degrees Fahrenheit.
90
That temperature in degrees Celsius is    32.22.
```

## <a name="using-generic-units"></a>汎用単位の使用

関連する測定単位を持つデータを操作するジェネリック関数を作成できます。 これを行うには、次のコード例に示すように、型パラメーターとしてジェネリック単位を使用して型を指定します。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6903.fs)]

## <a name="creating-aggregate-types-with-generic-units"></a>汎用単位を使用した集計型の作成

次のコードは、ジェネリックである単位を持つ個々の浮動小数点値で構成される集計型を作成する方法を示しています。 これにより、さまざまな単位で動作する1つの型を作成できます。 また、1つの単位セットを持つジェネリック型が、異なる単位のセットを持つ同じジェネリック型とは異なる型であることを保証することで、ジェネリックユニットはタイプセーフを保持します。 この手法の基礎は、 `Measure`属性を型パラメーターに適用できることです。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6904.fs)]

## <a name="units-at-runtime"></a>実行時の単位数

静的な型チェックには、測定単位が使用されます。 浮動小数点値をコンパイルすると、測定単位が削除されるため、実行時に単位が失われます。 したがって、実行時の単位のチェックに依存する機能を実装しようとすることはできません。 たとえば、単位を出力`ToString`する関数を実装することはできません。

## <a name="conversions"></a>変換

単位を持つ型 (など`float<'u>`) を、単位のない型に変換するには、標準変換関数を使用します。 たとえば、次のコードに`float`示すように、 `float`を使用して、単位を持たない値に変換することができます。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6905.fs)]

単位を含む値に単位なしの値を変換するには、適切な単位で注釈が付けられた1または1.0 の値を乗算します。 ただし、相互運用性レイヤーを記述する場合は、単位の値を単位の値に変換するために使用できる明示的な関数もいくつかあります。 これらは[fsharp.core](https://msdn.microsoft.com/library/69d08ac5-5d51-4c20-bf1e-850fd312ece3)モジュールに含まれています。 たとえば、単位なしから`float` `float<cm>`に変換するには、次のコードに示すように、 [FloatWithMeasure](https://msdn.microsoft.com/library/69520bc7-d67b-46b8-9004-7cac9646b8d9)を使用します。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6906.fs)]

## <a name="units-of-measure-in-the-f-core-library"></a>F#コアライブラリの測定単位

`FSharp.Data.UnitSystems.SI`名前空間では、ユニットライブラリを使用できます。 この`m`例では、 `UnitSymbols`副名前空間のシンボル形式 (メーターの場合) と、 `UnitNames`サブ名前空間のフルネーム (メーター `meter`のような) の両方に SI 単位が含まれています。

## <a name="see-also"></a>関連項目

- [F# 言語リファレンス](index.md)
