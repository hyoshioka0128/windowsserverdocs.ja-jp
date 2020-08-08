---
title: SQL Server を使用した Windows Server 2016 での AD FS へのアップグレード
author: billmath
manager: mtillman
ms.date: 04/11/2018
ms.topic: article
ms.assetid: 70f279bf-aea1-4f4f-9ab3-e9157233e267
ms.author: billmath
ms.openlocfilehash: 434ee97a352ad30caef83e495a387583da1f955b
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87940560"
---
# <a name="upgrading-to-ad-fs-in-windows-server-2016-with-sql-server"></a>SQL Server を使用した Windows Server 2016 での AD FS へのアップグレード


> [!NOTE]
> 完了のために計画された明確な時間枠でアップグレードを開始するだけです。 混合モードで AD FS を維持すると、ファームで問題が発生する可能性があるため、長時間にわたって混在モードの状態で AD FS を維持することはお勧めしません。


## <a name="moving-from-a-windows-server-2012-r2-ad-fs-farm-to-a-windows-server-2016-ad-fs-farm"></a>Windows Server 2012 R2 AD FS ファームから Windows Server 2016 AD FS ファームへの移行
次のドキュメントでは、AD FS データベースに SQL Server を使用している場合に、windows server 2012 R2 ファーム AD FS を Windows Server 2016 の AD FS にアップグレードする方法について説明します。

### <a name="upgrading-ad-fs-to-windows-server-2016-fbl"></a>Windows Server 2016 FBL への AD FS のアップグレード
Windows Server 2016 の AD FS の新機能は、ファームの動作レベル (FBL) です。   この機能はファーム全体で、AD FS ファームで使用できる機能を決定します。   既定では、Windows Server 2012 R2 AD FS ファームの FBL は、Windows Server 2012 R2 FBL にあります。

Windows server 2016 AD FS サーバーは、windows server 2012 R2 ファームに追加することができ、windows server 2012 R2 と同じ FBL で動作します。  この方法で Windows Server 2016 AD FS サーバーが動作している場合、ファームは "mixed" と呼ばれます。  ただし、FBL が Windows Server 2016 に対して発生するまで、新しい Windows Server 2016 機能を利用することはできません。  ファームが混在している場合:

-   管理者は、windows server 2016 の新しいフェデレーションサーバーを既存の Windows Server 2012 R2 ファームに追加できます。  その結果、ファームは "混在モード" になり、Windows Server 2012 R2 ファームの動作レベルを操作します。  ファーム全体で動作が一貫しているように、新しい Windows Server 2016 の機能を構成したり、このモードで使用したりすることはできません。

-   すべての Windows Server 2012 R2 フェデレーションサーバーが混在モードファームから削除され、WID ファームの場合は、新しい Windows サービス2016フェデレーションサーバーの1つがプライマリノードの役割に昇格された後、管理者は Windows Server 2012 R2 から Windows Server 2016 に FBL を上げることができます。  その結果、新しい AD FS Windows Server 2016 の機能を構成して使用できるようになります。

-   ファーム機能が混在しているため、windows server 2016 へのアップグレードを検討している Windows Server 2012 R2 組織では、まったく新しいファームを展開し、構成データをエクスポートしてインポートする必要はありません AD FS。  その代わりに、Windows Server 2016 ノードをオンラインにしている既存のファームに追加することができ、FBL の発生に伴うダウンタイムは比較的短くなります。

ファームモードが混在している場合、AD FS ファームは、Windows Server 2016 の AD FS で導入された新しい機能には対応していないことに注意してください。  これは、新しい機能を試す必要がある組織は、FBL が発生するまでこれを行うことができないことを意味します。  そのため、FBL を使用する前に、新しい機能をテストすることを検討している組織では、これを行うために別のファームをデプロイする必要があります。

このドキュメントの残りの部分では、windows server 2016 フェデレーションサーバーを windows server 2012 R2 環境に追加し、windows Server 2016 に FBL を発生させる手順について説明します。  これらの手順は、以下のアーキテクチャ図に示されているテスト環境で実行されました。

> [!NOTE]
> Windows Server 2016 FBL の AD FS に移行する前に、すべての Windows 2012 R2 ノードを削除する必要があります。  Windows Server 2012 R2 OS を Windows Server 2016 にアップグレードするだけで、それが2016ノードになるようにすることはできません。  これを削除し、新しい2016ノードに置き換える必要があります。

次のアーキテクチャ図は、次の手順を検証して記録するために使用されたセットアップを示しています。

![Architecture](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/arch.png)


#### <a name="join-the-windows-2016-ad-fs-server-to-the-ad-fs-farm"></a>Windows 2016 AD FS サーバーを AD FS ファームに参加させる

1.  サーバーマネージャー使用して Active Directory フェデレーションサービス (AD FS) の役割を Windows Server 2016 にインストールする

2.  AD FS 構成ウィザードを使用して、新しい Windows Server 2016 サーバーを既存の AD FS ファームに参加させます。  [**ようこそ**] 画面で [**次へ**] をクリックします。
 ![ファームに参加](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/configure1.png)
3.  [ **Active Directory Domain Services への接続**] 画面で、p) フェデレーションサービスの構成を実行するアクセス許可を持つ**管理者アカウント**を設定し、[**次へ**] をクリックします。
4.  [**ファームの指定**] 画面で、SQL server およびインスタンスの名前を入力し、[**次へ**] をクリックします。
![ファームに参加](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/configure3.png)
5.  [ **SSL 証明書の指定**] 画面で、証明書を指定し、[**次へ**] をクリックします。
![ファームに参加](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/configure4.png)
6.  [**サービスアカウントの指定**] 画面で、サービスアカウントを指定し、[**次へ**] をクリックします。
7.  [**オプションの確認**] 画面で、オプションを確認し、[**次へ**] をクリックします。
8.  **前提条件の確認**画面で、前提条件のチェックがすべて合格したことを確認し、[**構成**] をクリックします。
9.  [**結果**] 画面で、[サーバー] が正常に構成されていることを確認し、[**閉じる**] をクリックします。


#### <a name="remove-the-windows-server-2012-r2-ad-fs-server"></a>Windows Server 2012 R2 AD FS サーバーの削除

>[!NOTE]
>SQL をデータベースとして使用する場合は、AdfsSyncProperties-Role を使用してプライマリ AD FS サーバーを設定する必要はありません。  この構成では、すべてのノードがプライマリと見なされるためです。

1.  Windows Server 2012 R2 AD FS サーバーのサーバーマネージャーで、[**管理**] の [**役割と機能の削除**] を使用します。
![サーバーの削除](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/remove1.png)
2.  [**開始する前に**] 画面で、[**次へ**] をクリックします。
3.  [**サーバーの選択**] 画面で、[**次へ**] をクリックします。
4.  [**サーバーの役割**] 画面で、[ **Active Directory フェデレーションサービス (AD FS)** の横にあるチェックボックスをオフにし、[**次へ**] をクリックします。
![サーバーの削除](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/remove2.png)
5.  [**機能**] 画面で、[**次へ**] をクリックします。
6.  [**確認**] 画面で、[**削除**] をクリックします。
7.  この処理が完了したら、サーバーを再起動します。

#### <a name="raise-the-farm-behavior-level-fbl"></a>ファームの動作レベルを上げる (FBL)
この手順の前に、Active Directory 環境で forestprep と domainprep が実行されていること、および Active Directory に Windows Server 2016 スキーマがあることを確認する必要があります。  このドキュメントは、Windows 2016 ドメインコントローラーから開始され、AD のインストール時に実行されたため、これらのドメインコントローラーを実行する必要はありませんでした。

>[!NOTE]
>以下のプロセスを開始する前に、[設定] から Windows Update を実行して、Windows Server 2016 が最新であることを確認してください。  更新の必要がなくなるまで、このプロセスを続けます。 さらに、ADFS サービスアカウントアカウントが、SQL server と ADFS ファーム内の各サーバーに対する管理アクセス許可を持っていることを確認します。

1. Windows Server 2016 サーバーで PowerShell を開き、次のように実行します。 **$cred = 取得**して、enter キーを押します。
2. SQL Server に対して管理者特権を持つ資格情報を入力します。
3. PowerShell で、次のように入力します。 **AdfsFarmBehaviorLevelRaise-Credential $cred**
2. プロンプトが表示されたら、「 **Y**」と入力します。 これにより、レベルの引き上げが開始されます。  これが完了すると、FBL が正常に発生しました。
![更新の完了](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/finish1.png)
3. ここで、[AD FS 管理] にアクセスすると、Windows Server 2016 で AD FS に追加された新しいノードが表示されます。
4. 同様に、PowerShell の cmdlt: AdfsFarmInformation を使用して、現在の FBL を表示できます。
![更新の完了](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/finish2.png)

#### <a name="upgrade-the-configuration-version-of-existing-wap-servers"></a>既存の WAP サーバーの構成バージョンをアップグレードする
1. 各 Web アプリケーションプロキシで、管理者特権のウィンドウで次の PowerShell コマンドを実行して、WAP を再構成します。
    ```powershell
    $trustcred = Get-Credential -Message "Enter Domain Administrator credentials"
    Install-WebApplicationProxy -CertificateThumbprint {SSLCert} -fsname fsname -FederationServiceTrustCredential $trustcred
    ```
2. クラスターから古いサーバーを削除し、次の Powershell コマンドレットを実行して、上記で再構成された最新のサーバーバージョンを実行している WAP サーバーのみを保持します。
    ```powershell
    Set-WebApplicationProxyConfiguration -ConnectedServersName WAPServerName1, WAPServerName2
    ```
3. Get WebApplicationProxyConfiguration commmandlet を実行して、WAP の構成を確認します。 ConnectedServersName には、前のコマンドからのサーバー実行が反映されます。
    ```powershell
    Get-WebApplicationProxyConfiguration
    ```
4. WAP サーバーの ConfigurationVersion をアップグレードするには、次の Powershell コマンドを実行します。
    ```powershell
    Set-WebApplicationProxyConfiguration -UpgradeConfigurationVersion
    ```
5. Get WebApplicationProxyConfiguration Powershell コマンドを使用して ConfigurationVersion がアップグレードされていることを確認します。
