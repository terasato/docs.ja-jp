---
title: TCP アクティベーション
ms.date: 03/30/2017
ms.assetid: bf8c215c-0228-4f4f-85c2-e33794ec09a7
ms.openlocfilehash: e3bfbe9d7e7a6efafc8bf1e281e1f7a99c9c5fbe
ms.sourcegitcommit: 2d42b7ae4252cfe1232777f501ea9ac97df31b63
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2019
ms.locfileid: "67487525"
---
# <a name="tcp-activation"></a>TCP アクティベーション

このサンプルでは、net.tcp プロトコルで通信するサービスをアクティブ化するために、Windows プロセス アクティブ化サービス (WAS) を使用してサービスをホストする方法について示します。 このサンプルがに基づいて、 [Getting Started](../../../../docs/framework/wcf/samples/getting-started-sample.md)します。

> [!NOTE]
> このサンプルのセットアップ手順とビルド手順については、このトピックの最後を参照してください。

> [!IMPORTANT]
> サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> このディレクトリが存在しない場合に移動[Windows Communication Foundation (WCF) と .NET Framework 4 向けの Windows Workflow Foundation (WF) サンプル](https://go.microsoft.com/fwlink/?LinkId=150780)すべて Windows Communication Foundation (WCF) をダウンロードして[!INCLUDE[wf1](../../../../includes/wf1-md.md)]サンプル。 このサンプルは、次のディレクトリに格納されます。
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Hosting\WASHost\TCPActivation`

このサンプルは、クライアント コンソール プログラム (.exe) と、WAS によってアクティブ化されるワーカー プロセス内でホストされるサービス ライブラリ (.dll) で構成されています。 クライアント アクティビティは、コンソール ウィンドウに表示されます。

サービスは、要求/応答通信パターンを定義するコントラクトを実装します。 コントラクトは `ICalculator` インターフェイスによって定義されており、算術演算 (Add、Subtract、Multiply、および Divide) を公開しています。次のサンプル コードを参照してください。

```csharp
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]
public interface ICalculator
{
    [OperationContract]
    double Add(double n1, double n2);
    [OperationContract]
    double Subtract(double n1, double n2);
    [OperationContract]
    double Multiply(double n1, double n2);
    [OperationContract]
    double Divide(double n1, double n2);
}
```

このサービス実装は、計算を行い、結果を返します。

```csharp
// Service class that implements the service contract.
public class CalculatorService : ICalculator
{
    public double Add(double n1, double n2)
    {
        return n1 + n2;
    }
    public double Subtract(double n1, double n2)
    {
        return n1 - n2;
    }
    public double Multiply(double n1, double n2)
    {
        return n1 * n2;
    }
    public double Divide(double n1, double n2)
    {
        return n1 / n2;
    }
}
```

このサンプルでは、TCP ポート共有が有効でセキュリティが無効になっている net.tcp バインディングの変化形を使用します。 セキュリティ保護された TCP バインディングを使用する場合は、サーバーのセキュリティ モードを必要な設定に変更し、クライアントで Svcutil.exe を再実行して更新クライアントの構成ファイルを生成します。

サービスの構成を次のサンプルに示します。

```xml
<system.serviceModel>

    <services>
      <service name="Microsoft.ServiceModel.Samples.CalculatorService"
               behaviorConfiguration="CalculatorServiceBehavior">
        <!-- This endpoint is exposed at the base address provided by host: net.tcp://localhost/servicemodelsamples/service.svc  -->
        <endpoint binding="netTcpBinding" bindingConfiguration="PortSharingBinding"
          contract="Microsoft.ServiceModel.Samples.ICalculator" />
        <!-- the mex endpoint is exposed at net.tcp://localhost/servicemodelsamples/service.svc/mex -->
        <endpoint address="mex"
                  binding="mexTcpBinding"
                  contract="IMetadataExchange" />
      </service>
    </services>
    <bindings>
      <netTcpBinding>
        <binding name="PortSharingBinding" portSharingEnabled="true">
          <security mode="None" />
        </binding>
      </netTcpBinding>
    </bindings>

    <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->
    <behaviors>
      <serviceBehaviors>
        <behavior name="CalculatorServiceBehavior">
          <serviceMetadata />
          <serviceDebug includeExceptionDetailInFaults="False" />
        </behavior>
      </serviceBehaviors>
    </behaviors>

  </system.serviceModel>
```

クライアントのエンドポイントが構成されます。次のサンプル コードを参照してください。

```xml
<system.serviceModel>
    <bindings>
        <netTcpBinding>
          <binding name="NetTcpBinding_ICalculator">
            <security mode="None"/>
          </binding>
        </netTcpBinding>
    </bindings>
    <client>
        <endpoint address="net.tcp://localhost/servicemodelsamples/service.svc"
            binding="netTcpBinding" bindingConfiguration="NetTcpBinding_ICalculator"
            contract="Microsoft.ServiceModel.Samples.ICalculator" name="NetTcpBinding_ICalculator" />
    </client>
</system.serviceModel>
```

このサンプルを実行すると、操作要求および応答がクライアントのコンソール ウィンドウに表示されます。 クライアントをシャットダウンするには、クライアント ウィンドウで Enter キーを押します。

```console
Add(100,15.99) = 115.99
Subtract(145,76.54) = 68.46
Multiply(9,81.25) = 731.25
Divide(22,7) = 3.14285714285714

Press <ENTER> to terminate client.
```

### <a name="to-set-up-build-and-run-the-sample"></a>サンプルをセットアップ、ビルド、および実行するには

1. IIS 7.0 がインストールされていることを確認します。 IIS 7.0 では、WAS アクティブ化に必要です。

2. 実行済みであるかどうかを必ず、 [Windows Communication Foundation サンプルの 1 回限りのセットアップ手順](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)します。

    さらに、WCF 非 HTTP アクティブ化コンポーネントをインストールする必要があります。

    1. **[スタート]** メニューの **[コントロール パネル]** をクリックします。

    2. 選択**プログラムと機能**します。

    3. クリックして**Windows コンポーネントをオンまたはオフ**します。

    4. 展開、 **Microsoft .NET Framework 3.0**ノードとチェック、 **Windows Communication Foundation NON-HTTP Activation**機能します。

3. TCP アクティベーションをサポートするよう WAS を構成します。

    便宜上次の 2 つの手順が、サンプル ディレクトリにある AddNetTcpSiteBinding.cmd というバッチ ファイルに実装されています。

    1. net.tcp アクティベーションをサポートするには、既定の Web サイトをあらかじめ net.tcp ポートにバインドしておく必要があります。 これは、インターネット インフォメーション サービス 7.0 (IIS) 管理ツール セットと共にインストールされる Appcmd.exe を使用して行います。 管理者レベルのコマンド プロンプトから、次のコマンドを実行します。

        ```console
        %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site" -+bindings.[protocol='net.tcp',bindingInformation='808:*']
        ```

        > [!TIP]
        > このコマンドはテキスト 1 行です。 このコマンドは、net.tcp サイト バインディングを、TCP ポート 808 で任意のホスト名をリッスンする既定の Web サイトに追加します。

    2. サイト内のすべてのアプリケーションが同じ net.tcp バインディングを共有しますが、net.tcp サポートの有効化はアプリケーションごとに指定できます。 /servicemodelsamples アプリケーションで net.tcp を有効にするには、管理者レベルのコマンド プロンプトから、次のコマンドを実行します。

        ```console
        %windir%\system32\inetsrv\appcmd.exe set app
        "Default Web Site/servicemodelsamples" /enabledProtocols:http,net.tcp
        ```

        > [!NOTE]
        > このコマンドはテキスト 1 行です。 このコマンドにより、/servicemodelsamples アプリケーションに両方を使用してアクセスできる`http://localhost/servicemodelsamples`と`net.tcp://localhost/servicemodelsamples`します。

4. ソリューションの C# 版または Visual Basic .NET 版をビルドするには、「 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)」の手順に従います。

5. 1 つまたは複数コンピューター構成では、サンプルを実行する手順については、 [Windows Communication Foundation サンプルの実行](../../../../docs/framework/wcf/samples/running-the-samples.md)します。

    このサンプル用に追加した net.tcp サイト バインディングを削除します。

    便宜上次の 2 つの手順が、サンプル ディレクトリにある RemoveNetTcpSiteBinding.cmd というバッチ ファイルに実装されています。

    1. 管理者レベルのコマンド プロンプトから次のコマンドを実行して、有効なプロトコルの一覧から net.tcp を削除します。

        ```console
        %windir%\system32\inetsrv\appcmd.exe set app
        "Default Web Site/servicemodelsamples" /enabledProtocols:http
        ```

        > [!NOTE]
        > このコマンドは、全体で 1 行のテキストになるように入力する必要があります。

    2. 管理者レベルのコマンド プロンプトから次のコマンドを実行して、net.tcp サイト バインディングを削除します。

        ```console
        %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site"
        --bindings.[protocol='net.tcp',bindingInformation='808:*']
        ```

        > [!NOTE]
        > このコマンドは、全体で 1 行のテキストになるように入力する必要があります。

## <a name="see-also"></a>関連項目

- [AppFabric のホストおよび永続化のサンプル](https://go.microsoft.com/fwlink/?LinkId=193961)
