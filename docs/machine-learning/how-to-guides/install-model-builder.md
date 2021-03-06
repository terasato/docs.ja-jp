---
title: モデル ビルダーのインストール方法
description: ML.NET モデル ビルダー ツールのインストール方法について説明します
author: luisquintanilla
ms.author: luquinta
ms.date: 06/21/2019
ms.custom: mvc, how-to
ms.openlocfilehash: 54ab595c56f816517180aab48022c7df207fe84d
ms.sourcegitcommit: 52e588dc2ee74d484cd07ac60076be25cbf777ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2019
ms.locfileid: "67410570"
---
# <a name="how-to-install-mlnet-model-builder"></a>ML.NET モデル ビルダーのインストール方法

ML.NET モデル ビルダーをインストールして .NET アプリケーションに機械学習を追加する方法について説明します。

> [!NOTE]
> モデル ビルダーは現在のところ、プレビュー段階です。

## <a name="pre-requisites"></a>前提条件

- Visual Studio 2017 15.9.12 以降 / Visual Studio 2019
- .NET Core 2.1 以降の SDK

## <a name="limitations"></a>制限事項

- ML.NET モデル ビルダー拡張機能は現在のところ、Windows 上の Visual Studio でのみ動作します。
- トレーニング データセットの制限は 1 GB までの制限があります
- SQL Server のトレーニング用の行は 10 万行までの制限があります。
- Visual Studio 2017 用の Microsoft SQL Server Data Tools はサポートされていません

## <a name="install"></a>インストール

ML.NET モデル ビルダーは、Visual Studio Marketplace または Visual Studio からインストールできます。 

### <a name="visual-studio-marketplace"></a>Visual Studio Marketplace

1. [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=MLNET.07) からダウンロード
1. 指示に従って該当する Visual Studio バージョンにインストールします

### <a name="visual-studio-2017"></a>Visual Studio 2017

1. メニュー バーで、 **[ツール]**  >  **[拡張機能と更新プログラム]** の順に選択します
1. *[拡張機能と更新プログラム]* プロンプト内で、 *[オンライン]* ノードを選択します
1. 検索バーで「*ML.NET モデル ビルダー*」を検索し、結果から「ML.NET モデル ビルダー (Preview)」を選択します
1. プロンプトの指示に従って、インストールを行います

### <a name="visual-studio-2019"></a>Visual Studio 2019

1. メニュー バーで **[拡張機能]**  >  **[拡張機能の管理]** の順に選択します
1. *[拡張機能と更新プログラム]* プロンプト内で、 *[オンライン]* ノードを選択します
1. 検索バーに「*ML.NET モデル ビルダー*」と入力し、「ML.NET モデル ビルダー (Preview)」を選択します
1. プロンプトの指示に従って、インストールを行います

## <a name="uninstall"></a>[アンインストール]

### <a name="visual-studio-2017"></a>Visual Studio 2017

1. メニュー バーで、 **[ツール]**  >  **[拡張機能と更新プログラム]** の順に選択します
1. *[拡張機能と更新プログラム]* プロンプト内で、 *[インストール済み]* ノードを展開し、 *[ツール]* を選択します
1. ツールの一覧から「ML.NET モデル ビルダー (Preview)」を選択し、 *[アンインストール]* を選択します
1. プロンプトの指示に従って、アンインストールを行います

### <a name="visual-studio-2019"></a>Visual Studio 2019

1. メニュー バーで **[拡張機能]**  >  **[拡張機能の管理]** の順に選択します
1. *[拡張機能と更新プログラム]* プロンプト内で、 *[インストール済み]* ノードを展開し、 *[ツール]* を選択します
1. ツールの一覧から「ML.NET モデル ビルダー (Preview)」を選択し、 *[アンインストール]* を選択します
1. プロンプトの指示に従って、アンインストールを行います

## <a name="upgrade"></a>Upgrade

アップグレード プロセスは、インストール プロセスに似ています。 Visual Studio Marketplace から最新バージョンをダウンロードするか、または Visual Studio で拡張機能マネージャーを使用します。
