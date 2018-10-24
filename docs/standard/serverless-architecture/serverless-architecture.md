---
title: サーバーレス アーキテクチャのサーバーレス アプリ
description: さまざまなアーキテクチャと web アプリ、モバイル、IoT などのサーバーレス アーキテクチャでサポートされているアプリの探索。
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 06/26/2018
ms.openlocfilehash: ea944a172154a1cff2b8f830cb8fc3fa24a15028
ms.sourcegitcommit: 4c158beee818c408d45a9609bfc06f209a523e22
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2018
ms.locfileid: "49370202"
---
# <a name="serverless-architecture"></a>サーバーレス アーキテクチャ

サーバーレス アーキテクチャを使用する多くの方法はあります。 この章では、サーバーレスを統合する一般的なアーキテクチャの例について説明します。 追加の課題をもたらす可能性があります、またはサーバーレスを実装する場合は、追加の考慮事項を必要とする考慮事項についても説明します。 最後に、デザイン例をいくつかは、さまざまなサーバーレスのユース ケースを説明する指定されます。

サーバーレスのホストでは、サーバーレスのインスタンスを管理するのに既存のコンテナー ベースまたは PaaS レイヤーを多くの場合、使用します。 たとえば、Azure Functions に基づきます。 [Azure App Service](https://docs.microsoft.com/azure/app-service/)します。 App Service は、スケール アウト インスタンスと Azure Functions のコードを実行するランタイムの管理に使用されます。 PaaS とスケールの役割として実行するホストを Windows ベースの関数では、.NET ランタイムをチェック アウトします。 Linux ベースの関数では、ホストは、コンテナーを活用します。

![Azure Functions のアーキテクチャ](./media/azure-functions-architecture.png)

WebJobs Core では、関数の実行コンテキストを提供します。 言語ランタイムは、スクリプトを実行、ライブラリを実行し、対象言語のフレームワークをホストします。 たとえば、Node.js は JavaScript 関数を実行するために使用し、c# 関数の実行に .NET Framework を使用します。 この章の言語とプラットフォームのオプションについて説明します。

サーバーレスにする「オールインワン」アプローチを取るいくつかのプロジェクトが挙げられます。 マイクロ サービスに大きく依存するアプリケーションは、サーバーレス テクノロジを使用してすべてのマイクロ サービスを実装することができます。 ほとんどのアプリがハイブリッド、次の N 層デザインをおよび使用してサーバーレス コンポーネントが高まり、個別に拡張可能であるために、意味のあるコンポーネントの。 これらのシナリオを理解するには、このセクションはサーバーレスを使用する一般的なアーキテクチャ例を説明します。

## <a name="full-serverless-back-end"></a>完全サーバーレスのバック エンド

完全サーバーレスのバック エンドは、新しいビルド時に特にのシナリオでは、いくつかの種類に最適ですか「グリーン フィールド」アプリケーションです。 サーバーレスの関数としては、各 API を実装する Api の大規模なサーフェス領域を持つアプリケーションが挙げられます。 マイクロ サービス アーキテクチャに基づくアプリは、完全なサーバーレス バックエンドとして実装できる別の例です。 マイクロ サービスは、互いのさまざまなプロトコル経由で通信します。 特定のシナリオは次のとおりです。

* API ベースの SaaS 製品 (例: 財務支払プロセッサ)。
* メッセージ駆動型アプリケーション (例: デバイスの監視ソリューション)。
* アプリは、サービス間の統合に重点を置いて (例: 航空券の予約アプリケーション)。
* 定期的に実行されているプロセス (例: タイマー ベースのデータベースのクリーンアップ)。
* データ変換に重点を置いてアプリ (例: インポート ファイルのアップロードによってトリガーされます)。
* 変換および読み込み (ETL) プロセスを抽出します。

このドキュメントで後で説明する他、特定のユース ケースがあります。

## <a name="monoliths-and-starving-the-beast"></a>モノリスを「猛獣を逼迫させて」

一般的な課題には、既存のモノリシック アプリケーションをクラウドには、移行中です。 危険度の低いアプローチの仮想マシンを完全に「リフト アンド シフト」することです。 多くの店舗の機会として、コード ベースを現代化する、移行を使用したいです。 移行の実践的なアプローチは「悪の不足」と呼ばれる 「現状有姿に移行するモノリスでは、このシナリオでは、最初にします。 次に、選択したサービスが最新化します。 場合によっては、サービスの署名は、元と同じです。 関数としてホストだけです。 クライアントは、モノリス エンドポイントではなく、新しいサービスを使用して更新されます。 それまでの間、データベースのレプリケーションなどの手順には、トランザクションは、モノリスによって引き続き処理される場合でも、独自の記憶域をホストするマイクロ サービスが有効にします。 最終的には、すべてのクライアントは、新しいサービスに移行されます。 モノリスは「不足」(そのサービスが呼び出されない) までのすべての機能が置き換えられました。 サーバーレスの組み合わせと、プロキシは、この移行の多くを促進できます。

![サーバーレスのモノリスの移行](./media/serverless-monolith-migration.png)

この方法について詳しくは、ビデオを見る:[サーバーレス Azure Functions を使用してクラウドにアプリをもたらす](https://channel9.msdn.com/Events/Connect/2017/E102)します。

## <a name="web-apps"></a>Web アプリ

Web アプリは、サーバーレス アプリケーションの候補として最適です。 Web アプリへの 2 つの一般的なアプローチが今ある: サーバー ドリブン、およびクライアント主導の (Single Page Application SPA など)。 サーバー主導の web アプリは、通常、web UI を表示するために API 呼び出しを発行するのにミドルウェア レイヤーを使用します。 SPA アプリケーションでは、ブラウザーから直接 REST API 呼び出しを行います。 サーバーレス両方のシナリオで必要なビジネス ロジックを提供することにより、ミドルウェアまたは REST API 要求に対応できます。 一般的なアーキテクチャを使って、静的で軽量な web サーバーを設定します。 シングル ページ アプリケーション (SPA) は、HTML、CSS、JavaScript、およびその他のブラウザーの資産は機能します。 Web アプリは、マイクロ サービスのバック エンドに接続します。

## <a name="mobile-back-ends"></a>モバイル バックエンド

イベント ドリブンのサーバーレス アプリのパラダイムでは、モバイル バック エンドとして最適になります。 モバイル デバイスが、イベントをトリガーし、要求を満たすために、サーバーレス コードを実行します。 サーバーレスのモデルの活用によって、開発者は、完全なアプリケーションの更新プログラムを展開することがなくビジネス ロジックを強化できます。 サーバーレス アプローチでは、エンドポイントを共有し、並列で作業するチームもできます。

モバイル開発者は、サーバー側でのエキスパートになることがなく、ビジネス ロジックを構築できます。 これまでは、モバイル アプリでは、オンプレミス サービスに接続されています。 サービス層を構築するには、サーバー プラットフォームを理解し、パラダイムのプログラミングが必要です。 開発者は、サーバーをプロビジョニングし、適切に構成する操作と協力しています。 場合によっては数日または数週間が配置パイプラインの構築に費やされていました。 すべてのこれらの課題は、サーバーレスで対処できます。

サーバーなしのサーバー側の依存関係を抽象化され、開発者はビジネス ロジックに専念できます。 たとえば、モバイル開発者は JavaScript フレームワークを使用してアプリの構築には、JavaScript でサーバーレス関数もを構築できます。 サーバーレスのホストでは、オペレーティング システム、コード、パッケージの依存関係をホストする Node.js のインスタンスを管理します。 開発者は、出力の単純な一連の入力と標準テンプレートに提供されます。 これらはし、ビルドとテストのビジネス ロジックに専念できます。 されているので、既存のスキルを使用して、新しいプラットフォームを説明します。 または、「サーバー側開発者」になることがなく、モバイル アプリのバックエンド ロジックを構築するため

![サーバーレス モバイル バックエンドの終了します。](./media/serverless-mobile-backend.png)

ほとんどのクラウド プロバイダーでは、全体のモバイル開発ライフ サイクルを簡略化する mobile ベースのサーバーレスな製品を提供します。 製品には、データを永続化、DevOps の問題を処理、クラウド ベースのビルドし、テスト フレームワークと、開発者を使用してスクリプトのビジネス プロセスの機能の優先言語を提供するデータベースのプロビジョニングを自動化可能性があります。 モバイル中心のサーバーレス アプローチに従うと、プロセスを合理化することができます。 サーバーレスは、プロビジョニング、構成、およびモバイルのバックエンド サーバーの保守の膨大なオーバーヘッドを削除します。

## <a name="internet-of-things-iot"></a>モノのインターネット (IoT)

IoT は、ネットワークでつながっている物理オブジェクトを参照します。 「接続されているデバイス」または「スマート デバイス」として指すしている場合があります。 自動車や自動販売機のすべては、接続することがあり、温度と湿度などのセンサー データをインベントリからさまざまな情報を送信します。 企業内では、IoT は、automation の監視とビジネス プロセスの改善を提供します。 IoT データは、大規模なウェアハウスの気候の規定またはサプライ チェーン全体の在庫追跡を使用できます。 IoT は、化学物質の流出を検出し、煙が検出された場合に、消防署を呼び出します。

デバイスと情報を多くの場合、膨大な量は、メッセージ ルートを処理するイベント ドリブン アーキテクチャを決定します。 サーバーレスは、いくつかの理由で理想的なソリューションのことです。

* デバイスとデータの増加量としてのスケールを実現します。
* 新しいデバイスとセンサーをサポートする新しいエンドポイントの追加に対応します。
* 開発者は、システム全体をデプロイすることがなく、特定のデバイスのビジネス ロジックを更新できるように、独立したバージョン管理を容易になります。
* 回復性とダウンタイムの短縮。

IoT の良しの結果、いくつかのサーバーレス製品具体的には、IoT の問題に的を絞ったなど[Azure IoT Hub](https://docs.microsoft.com/azure/iot-hub)します。 デバイスの登録、ポリシーの適用、追跡、およびコードでのデバイスにも配置などのタスクを自動化するサーバーレス*エッジ*します。 エッジは、センサーとアクチュエータに接続されている一部ではない、アクティブなインターネットのようなデバイスを指します。

>[!div class="step-by-step"]
[前へ](architecture-approaches.md)
[次へ](serverless-architecture-considerations.md)