---
title: 'AD FS と Web アプリケーション プロキシを使ったワーク フォルダーの展開 - 手順 3: ワーク フォルダーのセットアップ'
ms.topic: article
manager: klaasl
ms.author: jeffpatt
author: JeffPatt24
ms.date: 4/5/2017
ms.assetid: 5a43b104-4d02-4d73-a385-da1cfb67e341
ms.openlocfilehash: 784b4467fccaefc2911c501d49ac4c1cd9196c67
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87970079"
---
# <a name="deploy-work-folders-with-ad-fs-and-web-application-proxy-step-3-set-up-work-folders"></a>AD FS と Web アプリケーション プロキシを使ったワーク フォルダーの展開: 手順 3: ワーク フォルダーのセットアップ

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、Active Directory フェデレーション サービス (AD FS) と Web アプリケーション プロキシを使用して、ワーク フォルダーを展開する 3 番目の手順について説明します。 このプロセスの他の手順は、次のトピックで確認できます。

-   [AD FS と Web アプリケーション プロキシを使ったワーク フォルダーの展開: 概要](deploy-work-folders-adfs-overview.md)

-   [AD FS と Web アプリケーション プロキシを使ったワーク フォルダーの展開: 手順 1: AD FS のセットアップ](deploy-work-folders-adfs-step1.md)

-   [AD FS と Web アプリケーション プロキシを使ったワーク フォルダーの展開: 手順 2、AD FS の構成後の作業](deploy-work-folders-adfs-step2.md)

-   [AD FS と Web アプリケーション プロキシを使ったワーク フォルダーの展開: 手順 4: Web アプリケーション プロキシのセットアップ](deploy-work-folders-adfs-step4.md)

-   [AD FS と Web アプリケーション プロキシを使ったワーク フォルダーの展開: 手順 5: クライアントのセットアップ](deploy-work-folders-adfs-step5.md)

> [!NOTE]
>   このセクションで説明する手順は、Windows Server 2019 または Windows Server 2016 環境向けです。 Windows Server 2012 R2 を使用している場合には、[Windows Server 2012 R2 の手順](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn747208(v=ws.11)) に従います。

ワーク フォルダーをセットアップするには、次の手順を使用します。

## <a name="pre-installment-work"></a>事前 \- 分割作業
ワーク フォルダーをインストールするには、ドメインに参加している、Windows Server 2016 を実行しているサーバーが必要です。 サーバーには、有効なネットワーク構成が必要です。

このテストの例では、ワーク フォルダーを実行するコンピューターは Contoso ドメイン に参加し、以下のセクションの説明のようにネットワーク インターフェイスをセットアップします。

### <a name="set-the-server-ip-address"></a>サーバー IP アドレスの設定
サーバーの IP アドレスを静的 IP アドレスに変更します。 テストの例では、IP クラス A を使用し、192.168.0.170 / サブネット マスク: 255.255.0.0 / 既定のゲートウェイ: 192.168.0.1 / 優先 DNS: 192.168.0.150 (ドメイン コントローラーの IP アドレス) とします。

### <a name="create-the-cname-record-for-work-folders"></a>ワーク フォルダーの CNAME レコードの作成
ワーク フォルダーの CNAME レコードを作成するには、次の手順を実行します。

1.  ドメイン コントローラーで、**[DNS マネージャー]** を開きます。

2.  [前方参照ゾーン] フォルダーを展開し、ドメインで右クリックして、**[新しいエイリアス (CNAME)]** をクリックします。

3.  **[新しいリソース レコード]** ウィンドウで、**[エイリアス名]** フィールドに、ワーク フォルダーのエイリアスを入力します。 このテストの例では、「**workfolders**」とします。

4.  **[完全修飾ドメイン名]** フィールドの値は「**workfolders.contoso.com**」です。

5.  **[ターゲット ホスト用の完全修飾ドメイン名]** フィールドに、ワーク フォルダーのサーバーの FQDN を入力します。 このテストの例では、「**2016-WF.contoso.com**」とします。

6.  **[OK]** をクリックします。

Windows PowerShell で同等の手順を実行するには、次のコマンドを使用します。 コマンドは、ドメイン コントローラーで実行する必要があります。

```powershell
Add-DnsServerResourceRecord  -ZoneName "contoso.com" -Name workfolders -CName  -HostNameAlias 2016-wf.contoso.com
```

### <a name="install-the-ad-fs-certificate"></a>AD FS 証明書のインストール
次の手順を使用して、AD FS のセットアップ中に作成されたAD FS 証明書を、ローカル コンピューターの証明書ストアにインストールします。

1.  **[スタート]** ボタンをクリックし、 **[ファイル名を指定して実行]** をクリックします。

2.  「**MMC**」と入力します。

3.  **[ファイル]** メニューの **[スナップインの追加と削除]** をクリックします。

4.  [**利用できるスナップイン**] の一覧で、[**証明書**]、[**追加**] の順に選択します。 証明書スナップイン ウィザードが開始されます。

5.  **[コンピューター アカウント]** を選択し、**[次へ]** をクリックします。

6.  **[ローカル コンピュータ (このコンソールを実行しているコンピュータ)]** を選択し、次に **[完了]** をクリックします。

7.  **[OK]** をクリックします。

8.  フォルダー**コンソール Root\Certificates \( Local Computer) \Personal\Certificates**を展開します。

9. [**証明書**] を右クリックし、[**すべてのタスク**]、[**インポート**] の順にクリックします。

10. AD FS 証明書を含むフォルダーを参照し、ウィザードの指示に従ってファイルをインポートして、証明書ストアに配置します。

11. フォルダー**コンソール Root\Certificates \( Local Computer) \Trusted ルート証明書 Authorities\Certificates**を展開します。

12. [**証明書**] を右クリックし、[**すべてのタスク**]、[**インポート**] の順にクリックします。

13. AD FS 証明書を含むフォルダーを参照し、ウィザードの指示に従ってファイルをインポートして、信頼されたルート証明機関ストアに配置します。

### <a name="create-the-work-folders-self-signed-certificate"></a>ワーク フォルダーの自己署名証明書を作成します。
ワーク フォルダーの自己署名証明書を作成するには、次の手順に従います。

1.  「[AD FS と Web アプリケーション プロキシを使ったワーク フォルダーの展開](https://techcommunity.microsoft.com/t5/storage-at-microsoft/deploying-work-folders-with-ad-fs-and-web-application-proxy-wap/ba-p/425318)」のブログ投稿で提供されているスクリプトをダウンロードし、ファイル makecert.ps1 をワーク フォルダーのコンピューターにコピーします。

2.  管理者特権で Windows PowerShell ウィンドウを開きます。

3.  実行ポリシーを、Unrestricted に設定します。

    ```powershell
    PS C:\temp\scripts> Set-ExecutionPolicy -ExecutionPolicy Unrestricted
    ```

4.  スクリプトをコピーしたディレクトリに移動します。

5.  makeCert スクリプトを実行します。

    ```powershell
    PS C:\temp\scripts> .\makecert.ps1
    ```

6.  サブジェクトの証明書を変更するようにメッセージが表示されたら、サブジェクトの新しい値を入力します。 この例では、値を「**workfolders.contoso.com**」とします。

7.  SAN の名前を入力するメッセージが表示されたら、Y キーを押し、次にサブジェクト代替名 (SAN) の名前を一度に 1 つずつ入力します。

    この例では、「**workfolders.contoso.com**」と入力して、Enter キーを押します。 次に「**2016-WF.contoso.com**」と入力し、Enter キーを押します。

    すべての SAN の名前を入力したら、空の行で Enter キーを押します。

8.  信頼されたルート証明機関ストアに証明書をインストールするようにメッセージが表示されたら、Y キーを押します。

ワーク フォルダー証明書は、次の値を持つ SAN 証明書である必要があります。

-   **ワークフォルダー**。**ドメイン**

-   **コンピューター名**.**ドメイン**

テストの例では、値は以下のようになります。

-   **workfolders.contoso.com**

-   **2016-WF.contoso.com**

## <a name="install-work-folders"></a>ワーク フォルダーのインストール
ワーク フォルダーの役割をインストールするには、以下の手順を実行します。

1.  **[サーバー マネージャー]** を開き、**[役割と機能の追加]** をクリックして、**[次へ]** をクリックします。

2.  [**インストールの種類**] ページで、[**役割ベースまたは機能ベースのインストール**] を選択し、[**次へ**] をクリックします。

3.  **[サーバーの選択]** ページで現在のサーバーを選択し、**[次へ]** をクリックします。

4.  **[サーバーの役割]** ページで、**[ファイル サービスおよび記憶域サービス]**、**[ファイル サービスおよび iSCSI サービス]** の順に展開し、**[ワーク フォルダー]** を選択します。

5.  **[役割と機能の追加ウィザード]** ページで、**[機能の追加]** をクリックし、**[次へ]** をクリックします。

6.  [**機能**] ページで、[**次へ**] をクリックします。

7.  [**確認**] ページで [**インストール**] をクリックします。

## <a name="configure-work-folders"></a>ワーク フォルダーの構成
ワーク フォルダーを構成するには、次の手順に従います。

1.  **サーバー マネージャー**を開きます。

2.  **[ファイル サービスと記憶域サービス]**、**[ワーク フォルダー]** の順に選択します。

3.  **[ワーク フォルダー]** ページで、**[新しい同期共有ウィザード]** を開始して、**[次へ]** をクリックします。

4.  **[サーバーとパス]** ページで同期共有を作成するサーバーを選択し、ワーク フォルダーが保存されるローカル パスを入力して、**[次へ]** をクリックします。

    パスが存在しない場合は、作成するように求められます。 **[OK]** をクリックします。

5.  **[ユーザー フォルダーの構造]** ページで、**[ユーザーのエイリアス]** を選択し、**[次へ]** をクリックします。

6.  **[同期共有名]** ページで、同期共有の名前を入力します。 このテストの例では、「**WorkFolders**」とします。 **[次へ]** をクリックします。

7.  **[同期アクセス]** ページで、新しい同期共有にアクセスするユーザーまたはグループを追加します。 このテストの例では、すべてのドメイン ユーザーにアクセスを許可します。 **[次へ]** をクリックします。

8.  **[PC セキュリティ ポリシー]** ページで、**[ワーク フォルダーを暗号化する]** と **[自動的にページをロックし、パスワードを要求する]** を選択します。 **[次へ]** をクリックします。

9. **[確認]** ページで、**[作成]** をクリックして、構成処理を完了します。

## <a name="work-folders-post-configuration-work"></a>ワーク フォルダーの構成後の作業
ワーク フォルダーのセットアップを完了するには、次の追加の手順を実行します。

-   ワーク フォルダー証明書を SSL ポートにバインドする

-   ワーク フォルダーを構成して AD FS 認証を使う

-   ワーク フォルダー証明書をエクスポートする (自己署名証明書を使用している場合)

### <a name="bind-the-certificate"></a>証明書をバインドする
ワーク フォルダーは SSL 経由のみで通信し、以前に作成した自己署名証明書 (または証明書機関によって発行されている証明書) をポートにバインドする必要があります。

証明書をポートにバインドするために Windows PowerShell で使用できる 2 つの方法があります。IIS コマンドレットおよび netsh です。

#### <a name="bind-the-certificate-by-using-netsh"></a>netsh を使用した証明書のバインド
netsh コマンド ライン スクリプト ユーティリティを Windows PowerShell で使用するには、コマンドを netsh にパイプ処理する必要があります。 次のスクリプト例では、**workfolders.contoso.com** というサブジェクトの証明書を検索し、netsh を使ってそれをポート 443 にバインドします。

```powershell
$subject = "workfolders.contoso.com"
Try
{
#In case there are multiple certificates with the same subject, get the latest version
$cert = Get-ChildItem CERT:\LocalMachine\My |where {$_.Subject -match $subject} | sort $_.NotAfter -Descending | select -first 1 
$thumbprint = $cert.Thumbprint
$Command = "http add sslcert ipport=0.0.0.0:443 certhash=$thumbprint appid={CE66697B-3AA0-49D1-BDBD-A25C8359FD5D} certstorename=MY"
$Command | netsh
}
Catch
{
"     Error: unable to locate certificate for $($subject)"
Exit
}
```

#### <a name="bind-the-certificate-by-using-iis-cmdlets"></a>IIS コマンドレットを使用した証明書のバインド
IIS 管理コマンドレットを使ってポートに証明書をバインドすることもできます。IIS 管理コマンドレットは IIS 管理ツールとスクリプトをインストールした場合に使用できます。

> [!NOTE]
> IIS 管理ツールのインストールだけでは、ワーク フォルダー コンピューターで、インターネット インフォメーション サービス (IIS) のフルバージョンは有効になりません。IIS 管理ツールのインストールでは、管理コマンドレットのみが有効になります。 このセットアップには、いくつかの利点があります。 たとえば、netsh が提供している機能を提供するコマンドレットが必要な場合です。 New-WebBinding コマンドレットを使って証明書をポートにバインドすると、このバインドは IIS に一切依存しません。 バインド後に Web-Mgmt-Console 機能を削除することもでき、それでも証明書はポートにバインドされています。 netsh を使って「**netsh http show sslcert**」と入力して、バインドを確認することができます。

次の例では、New-WebBinding コマンドレットを使用して、**workfolders.contoso.com** というサブジェクトの証明書を検索し、ポート 443 にバインドします。

```powershell
$subject = "workfolders.contoso.com"
Try
{
#In case there are multiple certificates with the same subject, get the latest version
$cert =Get-ChildItem CERT:\LocalMachine\My |where {$_.Subject -match $subject } | sort $_.NotAfter -Descending | select -first 1
$thumbprint = $cert.Thumbprint
New-WebBinding -Name "Default Web Site" -IP * -Port 443 -Protocol https
#The default IIS website name must be used for the binding. Because Work Folders uses Hostable Web Core and its own configuration file, its website name, 'ECSsite', will not work with the cmdlet. The workaround is to use the default IIS website name, even though IIS is not enabled, because the NewWebBinding cmdlet looks for a site in the default IIS configuration file.
Push-Location IIS:\SslBindings
Get-Item cert:\LocalMachine\MY\$thumbprint | new-item *!443
Pop-Location
}
Catch
{
"     Error: unable to locate certificate for $($subject)"
Exit
}
```

### <a name="set-up-ad-fs-authentication"></a>AD FS 認証のセットアップ
AD FS 認証を使用するようにワーク フォルダーを構成するには、次の手順に従います。

1.  **サーバー マネージャー**を開きます。

2.  **[サーバー]** をクリックして、一覧からワーク フォルダーのサーバーを選択します。

3.  サーバー名を右クリックし、**[ワーク フォルダーの設定]** をクリックします。

4.  **[ワーク フォルダーの設定]** ウィンドウで、**[Active Directory フェデレーション サービス (AD FS)]** を選択し、フェデレーション サービスの URL を入力します。 **[適用]** をクリックします。

    テストの例では、URL は **https://blueadfs.contoso.com** です。

Windows PowerShell で同じタスクを実行するコマンドレットは次のとおりです。

```powershell
Set-SyncServerSetting -ADFSUrl "https://blueadfs.contoso.com"
```

自己署名証明書を使って AD FS を設定する場合、フェデレーション サービスの URL が正しくない、アクセスできない、証明書利用者信頼がセットアップされていない、などのエラー メッセージが表示される場合があります。

このエラーは、AD FS 証明書がワーク フォルダー サーバーにインストールされていない場合、または AD FS の CNAME が正しくセットアップされていない場合にも発生します。 続行する前に、それらの問題を修正する必要があります。

### <a name="export-the-work-folders-certificate"></a>ワーク フォルダー証明書のエクスポート
自己署名のワーク フォルダー証明書をエクスポートして、テスト環境の以下のコンピューターにインストールできるようにする必要があります。

-   Web アプリケーション プロキシに使用するサーバー

-   ドメインに参加している Windows クライアント

-   ドメインに参加していない Windows クライアント

証明書をエクスポートするには、以前に AD FS 証明書のエクスポートに使用したものと同じ手順に従います。これは、「[AD FS と Web アプリケーション プロキシを使ったワーク フォルダーの展開: 手順 2、AD FS の構成後の作業](deploy-work-folders-adfs-step2.md)」の「AD FS 証明書のエクスポート」で説明されています。

次の手順: [AD FS と Web アプリケーション プロキシを使ったワーク フォルダーの展開: 手順 4: Web アプリケーション プロキシのセットアップ](deploy-work-folders-adfs-step4.md)

## <a name="see-also"></a>参照
[ワーク フォルダーの概要](Work-Folders-Overview.md)

