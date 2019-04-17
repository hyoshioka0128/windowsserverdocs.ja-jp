---
title: ユーザー用にリモート デスクトップ Web クライアントをセットアップする
description: リモート デスクトップ web クライアントを管理者を設定する方法について説明します。
ms.prod: windows-server-threshold
ms.technology: remote-desktop-services
ms.author: helohr
ms.date: 11/2/2018
ms.topic: article
author: Heidilohr
ms.localizationpriority: medium
ms.openlocfilehash: 2cb819a7f91646c61b84c3ee70550af6033ba340
ms.sourcegitcommit: 491c94b25501732c4a4abda533cc62b8bd278ed2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "9099185"
---
# ユーザー用にリモート デスクトップ Web クライアントをセットアップする

リモート デスクトップ web クライアントを使用して、互換性のある web ブラウザーから、組織のリモート デスクトップ インフラストラクチャにアクセスできます。 リモート アプリやユーザーがいる場所に関係なく、ローカル PC とは、それらのようにデスクトップを操作することができます。 リモート デスクトップ web クライアントを設定すると、ユーザーを開始する必要があるすべては、URL、自分の資格情報およびサポートされている web ブラウザーをクライアントにアクセスできます。

>[!IMPORTANT]
>Web クライアントでは、サポートされていません。 Azure アプリケーション プロキシを使用して、Web アプリケーション プロキシがまったくサポートされません。 詳細については、[アプリケーションのプロキシ サービスを使用して RDS](../rds-supported-config.md#using-remote-desktop-services-with-application-proxy-services)を参照してください。

## Web クライアントをセットアップする必要があります内容

始める前に、次の点に注意してください。

* [リモート デスクトップの展開](../rds-deploy-infrastructure.md)にサーバーが、RD ゲートウェイ、RD 接続ブローカーおよび RD Web アクセスの Windows Server 2016 または 2019 で実行されていることを確認します。
* デバイスごと、それ以外のすべてのライセンスが消費されるのではなく[ユーザーごとのクライアント アクセス ライセンス](../rds-client-access-license.md)(Cal) の展開が構成されていることを確認します。
* RD ゲートウェイには、 [Windows 10 KB4025334 の更新](https://support.microsoft.com/en-us/help/4025334/windows-10-update-kb4025334)をインストールします。 後で累積的な更新プログラムには、この KB 既に含まれている可能性があります。
* RD ゲートウェイと RD Web アクセスの役割の公開の信頼された証明書が構成されていることを確認します。
* ユーザーが接続する、すべてのコンピューターが実行されている OS バージョンを次のいずれかを確認します。
  * Windows 10
  * Windows Server 2008 r2 以降

ユーザーより優れたパフォーマンスには、Windows Server 2016 (またはそれ以降) が接続していると Windows 10 (バージョン 1611 以降) に表示されます。

>[!IMPORTANT]
>プレビュー期間中に、web クライアントを使用して、1.0.0 より前のバージョンをインストールした場合は、新しいバージョンに移動する前に古いクライアントをアンインストールする必要があります。 "Web クライアントがインストールされている RDWebClientManagement の以前のバージョンを使用して、新しいバージョンを展開する前に削除する必要があります"というエラーが発生した場合は、次の手順に従います。
>
>1. 管理者特権の PowerShell プロンプトを開きます。
>2. 新しいモジュールをアンインストールするのには、**アンインストール モジュール RDWebClientManagement**を実行します。
>3. 管理者特権の PowerShell プロンプトを閉じてから。
>4. 実行**古いモジュールをインストールするインストール モジュール RDWebClientManagement-requiredversion \<old version>** 。
>5. 以前の web client をアンインストールする**アンインストール RDWebClient**を実行します。
>6. 以前のモジュールをアンインストールするのには、**アンインストール モジュール RDWebClientManagement**を実行します。
>7. 管理者特権の PowerShell プロンプトを閉じてから。
>8. 次のように通常のインストールの手順に進みます。

## リモート デスクトップ web クライアントを公開する方法

最初に、web クライアントをインストールするには、次の次の手順を実行します。

1. RD 接続ブローカー サーバーでリモート デスクトップ接続に使用される証明書を取得し、.cer ファイルとしてエクスポートします。 RD 接続ブローカーから RD Web の役割を実行しているサーバーに、.cer ファイルをコピーします。
2. RD Web アクセス サーバーでは、管理者特権の PowerShell プロンプトを開きます。
3. Windows Server 2016 では、受信トレイのバージョンをサポートしていない web クライアント管理モジュールをインストールするため、PowerShellGet モジュールを更新します。 PowerShellGet を更新するには、次のコマンドレットを実行します。
    ```PowerShell
    Install-Module -Name PowerShellGet -Force
    ```

    >[!IMPORTANT]
    >更新プログラムを有効、それ以外の場合、モジュールが機能しない前に、PowerShell を再起動する必要があります。

4. 次のコマンドレットで PowerShell ギャラリーから、リモート デスクトップ web クライアント管理 PowerShell モジュールをインストールします。
    ```PowerShell
    Install-Module -Name RDWebClientManagement
    ```

5. その後、リモート デスクトップ web クライアントの最新バージョンをダウンロードする次のコマンドレットを実行します。
    ```PowerShell
    Install-RDWebClientPackage
    ```

6. 次に、置き換えられる RD ブローカーからコピーした .cer ファイルのパスで囲まれた値を次のコマンドレットを実行します。
    ```PowerShell
    Import-RDWebClientBrokerCert <.cer file path>
    ```

7. 最後に、リモート デスクトップ web クライアントを公開するには、このコマンドレットを実行します。
    ```PowerShell
    Publish-RDWebClientPackage -Type Production -Latest
    ```
    Web クライアント URL で web クライアントを使用するサーバー名、書式設定され、アクセスできるように<https://server_FQDN/RDWeb/webclient/index.html>します。 RD Web アクセスに URL (通常、サーバーの FQDN) でパブリック証明書と一致するサーバー名を使用する重要です。

    >[!NOTE]
    >**発行 RDWebClientPackage**コマンドレットを実行しているときは、ユーザーごとの Cal 構成、展開されている場合でも、デバイスごとの Cal という警告はサポートされていませんを表示する場合があります。 展開では、ユーザーごとの Cal を使用する場合は、この警告を無視できます。 表示されるは、構成の制限を認識かどうかを確認します。
8. Web クライアントへのアクセスをユーザーの準備ができたら、だけ URL を送信して web クライアントを作成します。

>[!NOTE]
>RDWebClientManagement モジュールのサポートされているすべてのコマンドレットの一覧を表示するには、PowerShell で次のコマンドレットを実行します。
>```PowerShell
>Get-Command -Module RDWebClientManagement
>```

## リモート デスクトップ web クライアントを更新する方法

リモート デスクトップ web クライアントの新しいバージョンが利用可能な新しいクライアントで、展開を更新する次の手順に従います。

1. RD Web アクセス サーバー上の管理者特権の PowerShell プロンプトを開き、web クライアントの利用できる最新バージョンをダウンロードする次のコマンドレットを実行します。
    ```PowerShell
    Install-RDWebClientPackage
    ```

2. 必要に応じて、このコマンドレットを実行して公式リリースの前にテストするため、クライアントを発行できます。
    ```PowerShell
    Publish-RDWebClientPackage -Type Test -Latest
    ```

    クライアントは、web クライアントの URL に対応する URL のテストに表示する必要があります (たとえば、 <https://server_FQDN/RDWeb/webclient-test/index.html>)。
3. 次のコマンドレットを実行して、ユーザーのクライアントを公開します。
    ```PowerShell
    Publish-RDWebClientPackage -Type Production -Latest
    ```

    Web ページを再起動するときは、すべてのユーザーのクライアントに置き換わります。

## リモート デスクトップ web クライアントをアンインストールする方法

Web クライアントのすべてのトレースを削除するには、次の手順を実行します。

1. RD Web アクセス サーバーでは、管理者特権の PowerShell プロンプトを開きます。
2. テストおよび運用環境のクライアントを非公開、ローカルのすべてのパッケージをアンインストールし、web クライアント設定を削除します。

   ```PowerShell
   Uninstall-RDWebClient
   ```

3. リモート デスクトップ web クライアント管理の PowerShell モジュールをアンインストールします。

   ```PowerShell
   Uninstall-Module -Name RDWebClientManagement
   ```

## インターネット接続がない場合、リモート デスクトップ web クライアントをインストールする方法

インターネット接続がない RD Web アクセス サーバーに web クライアントを展開する手順に従います。

> [!NOTE]
> インターネット接続が以降 1.0.1 のバージョンで利用可能なせずにインストールする RDWebClientManagement PowerShell モジュールのします。

> [!NOTE]
> オフラインのサーバーに転送する前に必要なファイルをダウンロードするインターネットにアクセスできる管理者 PC でも必要があります。

> [!NOTE]
> エンドユーザーの PC では、ここでは、インターネット接続が必要があります。 これは、完全なオフライン シナリオを提供するクライアントの今後のリリースで修正されます。

### インターネットにアクセスできるデバイスから

1. PowerShell プロンプトを開きます。

2. PowerShell ギャラリーから、リモート デスクトップ web クライアント管理 PowerShell モジュールをインポートします。
    ```PowerShell
    Import-Module -Name RDWebClientManagement
    ```

3. リモート デスクトップ web クライアントを別のデバイスにインストールするための最新バージョンをダウンロードするには。
    ```PowerShell
    Save-RDWebClientPackage "C:\WebClient\"
    ```

4. RDWebClientManagement PowerShell モジュールの最新バージョンをダウンロードするには。
    ```PowerShell
    Find-Module -Name "RDWebClientManagement" -Repository "PSGallery" | Save-Module -Path "C:\WebClient\"
    ```

5. RD Web アクセスのサーバーに"C:\WebClient\"の内容をコピーします。

### RD Web アクセスのサーバーから

[[リモート デスクトップ web クライアントを公開する方法](remote-desktop-web-client-admin.md#how-to-publish-the-remote-desktop-web-client)手順 4. ~ 5 を置き換えて次のように指示します。

4. ローカル フォルダーから、リモート デスクトップ web クライアント管理 PowerShell モジュールをインポートします。
    ```PowerShell
    Import-Module -Name "C:\WebClient\"
    ```

5. リモート デスクトップ web クライアントをローカル フォルダー (適切な zip ファイルを置換)) からの最新バージョンを展開するには。
    ```PowerShell
    Install-RDWebClientPackage -Source "C:\WebClient\rdwebclient-1.0.1.zip"
    ```

## Windows Server 2019 の RD ゲートウェイせず RD ブローカーに接続します。
このセクションでは、Windows Server 2019 の RD ゲートウェイせず、RD ブローカーに web クライアント接続を有効にする方法について説明します。

### RD ブローカー サーバーをセットアップします。

#### RD ブローカー サーバーにバインドされている証明書がない場合は、次の手順をに従ってください。

1. **サーバー マネージャー**を開きます > **リモート デスクトップ サービス**です。

2. **展開の概要**」セクションでは、**タスク**のドロップダウン メニューを選択します。

3. [**展開のプロパティの編集**、**展開**のプロパティを新しいウィンドウが開きます。

4. **展開のプロパティ**] ウィンドウで、左側のメニューで、**証明書**を選択します。

5. 証明書のレベルの一覧で、**有効にするシングル サインオンの RD 接続ブローカー**を選択します。 2 つのオプションがある: (1) 新しい証明書または (2)、既にある証明書を作成します。

#### 次の手順以前 RD ブローカー サーバーにバインドされている証明書がある場合

1. ブローカーおよびコピー**拇印**の値にバインドされている証明書を開いています。

2. この証明書をセキュリティで保護されたポート 3392 をバインドするには、管理者特権の PowerShell ウィンドウを開きし、 **"_lt _ 拇印 _gt"** を前の手順からコピーした値に置き換えて、次のコマンドを実行します。

    ```PowerShell
    netsh http add sslcert ipport=0.0.0.0:3392 certhash="<thumbprint>" certstorename="Remote Desktop" appid="{00000000-0000-0000-0000-000000000000}"
    ```

    > [!NOTE]
    > 確認するには、証明書が正しくバインドされているかどうかは、次のコマンドを実行します。
    >
    > ```PowerShell
    > netsh http show sslcert
    > ```
    >
    > SSL 証明書のバインドの一覧で、適切な証明書が 3392 ポートにバインドされていることを確認します。

3. 開き、Windows レジストリ (regedit) に nagivate ```HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp``` **WebSocketURI**キーを探します。 値を設定する必要があります**https://+:3392/rdp/** します。

### RD セッション ホストの設定
RD セッション ホスト サーバーが RD ブローカー サーバーと異なる場合は、次の手順に従います。

1. RD セッション ホスト マシン用の証明書を作成し、それを開き**拇印**の値をコピーします。

2. この証明書をセキュリティで保護されたポート 3392 をバインドするには、管理者特権の PowerShell ウィンドウを開きし、 **"_lt _ 拇印 _gt"** を前の手順からコピーした値に置き換えて、次のコマンドを実行します。

    ```PowerShell
    netsh http add sslcert ipport=0.0.0.0:3392 certhash="<thumbprint>" appid="{00000000-0000-0000-0000-000000000000}"
    ```

    > [!NOTE]
    > 確認するには、証明書が正しくバインドされているかどうかは、次のコマンドを実行します。
    >
    > ```PowerShell
    > netsh http show sslcert
    > ```
    >
    > SSL 証明書のバインドの一覧で、適切な証明書が 3392 ポートにバインドされていることを確認します。

3. 開き、Windows レジストリ (regedit) に nagivate ```HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp``` **WebSocketURI**キーを探します。 値を設定する必要があります**https://+:3392/rdp/** します。

### 一般的な観測

* RD セッション ホストと RD ブローカーの両方のサーバーが Windows Server 2019 を実行していることを確認します。

* RD セッション ホストと RD ブローカーの両方のサーバーの証明書を構成するパブリックが信頼できることを確認します。
    > [!NOTE]
    > RD セッション ホストと RD ブローカー サーバーの両方に、同じコンピューターを共有している場合は、RD ブローカー サーバー証明書のみを設定します。 RD セッション ホストと RD ブローカー サーバーは、さまざまなコンピューターを使用して、独自の証明書両方構成しなければなりません。

* 各証明書の**サブジェクト代替名 (SAN)** は、コンピューターの**完全修飾ドメイン名 (FQDN)** に設定する必要があります。 **共通名 (CN)** は、各証明書の SAN と一致する必要があります。

## トラブルシューティング

最初に、web クライアントを開くとき、次の問題のいずれかのユーザーを報告する場合、次のセクションがわかりますを修正するにはどのような。

### ユーザーのブラウザーが web クライアントへのアクセスしようとすると、セキュリティの警告を表示する場合の対処

RD Web アクセスの役割で信頼された証明書を使用しない可能性があります。 公的に信頼された証明書を使って、RD Web アクセスの役割が構成されていることを確認します。

した場合は、web サーバー名クライアント URL 可能性があります名前が一致 RD Web 証明書によって提供されます。 RD Web の役割をホストするサーバーの FQDN を使用する URL を確認します。

### ユーザーは、web クライアントと場合でも、すべてのリソースの下の項目に表示されることで、リソースに接続できない場合の対処

接続できないという web クライアントでのリソースを表示できる場合でも、ユーザーが報告された場合は、次のことを確認します。

* 信頼された公開証明書を使用する RD ゲートウェイの役割が正しく構成されてかどうか。
* RD ゲートウェイ サーバーが必要な更新プログラムがインストールされているかどうか。 サーバーが[、KB4025334 更新](https://support.microsoft.com/en-us/help/4025334/windows-10-update-kb4025334)インストールされていることを確認します。

ユーザーが「予期しないサーバー認証証明書が受け取ら」エラーを取得するかどうかはメッセージのしようとすると、接続し、証明書のサムプリントをメッセージが表示されます。 その拇印を使用して、適切な証明書を検索する RD ブローカー サーバーの証明書マネージャーを検索します。 リモート デスクトップ展開のプロパティ ページで RD ブローカーの役割に使用する証明書が構成されていることを確認します。 証明書を確認する前に限ります有効期限が切れた後は、.cer ファイル形式で RD Web アクセスのサーバーに証明書をコピーして、証明書のファイルのパスに置き換えで囲まれた値を持つ RD Web アクセス サーバーで、次のコマンドを実行します。

```PowerShell
Import-RDWebClientBrokerCert <certificate file path>
```

### コンソールのログの問題を診断します。

コンソールを見て、問題の原因を自分で診断しようとするできる場合、この記事のトラブルシューティングの手順に基づく問題を解決できない場合は、ブラウザーでログに記録します。 Web クライアントは、web クライアントを使用して、問題の診断に役立つブラウザー コンソールのログの利用状況を記録するためのメソッドを提供します。

* 右上隅の省略記号を選択し、ドロップダウン メニューで、**に関する**ページに移動します。
* [**キャプチャのサポート情報****の記録を開始**] ボタンを選択します。
* 診断しようとしている問題を生成する web クライアントでの処理を実行します。
* **に関する**ページに移動し、**録画を停止**を選択します。
* お使いのブラウザーは、タイトル**RD コンソール Logs.txt**.txt ファイルを自動的にダウンロードされます。 このファイルには、ターゲットの問題を再現するときに生成されたコンソールへのフル ログ アクティビティが含まれます。

コンソールにも、ブラウザーから直接アクセスできます。 コンソールは、開発者ツールの下にある一般にします。 または、省略記号を選択し、**他のツール**に移動することによって、 **F12**キーを押してに、Microsoft Edge でログにアクセスするなど、 > **開発者ツール**です。

## Web クライアントをヘルプします。

この記事の情報で解決できないという問題が発生したしたら、それを報告する[までご連絡](mailto:rdwbclnt@microsoft.com)をできます。 要求したり、[提案ボックス](https://aka.ms/rdwebfbk)の新機能の投票できます。