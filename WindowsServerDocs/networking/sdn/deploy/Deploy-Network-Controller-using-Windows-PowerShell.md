---
title: Windows PowerShell を使用してネットワーク コントローラーを展開する
description: このトピックでは、Windows PowerShell を使用して、コンピューターまたは Windows Server 2016 を実行している仮想マシン (Vm) の 1 つまたは複数のネットワーク コント ローラーを展開するについて説明します。
manager: dougkim
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 2448d381-55aa-4c14-997a-202c537c6727
ms.author: pashort
author: shortpatti
ms.date: 08/23/2018
ms.openlocfilehash: 31c1579dc840f6f4eb805ac4e10f51192a6b4c99
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816193"
---
# <a name="deploy-network-controller-using-windows-powershell"></a>Windows PowerShell を使用してネットワーク コントローラーを展開する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックでは、Windows PowerShell を使用して、1 つまたは複数の仮想マシン (Vm) Windows Server 2016 を実行しているのネットワーク コント ローラーを展開するについて説明します。

>[!IMPORTANT]
>物理ホストでネットワーク コント ローラー サーバーの役割を展開しないでください。 ネットワーク コント ローラーを展開するには、HYPER-V 仮想マシンでネットワーク コント ローラー サーバーの役割をインストールする必要があります\(VM\) HYPER-V ホストにインストールされています。 次の 3 つの異なるハイパースレッディング上の Vm でネットワーク コント ローラーをインストールした後\-V のホスト、ハイパースレッディングが有効にする必要があります\-ソフトウェアによるネットワーク制御の V ホスト\(SDN\)ネットワーク コント ローラーを使用するホストを追加することでWindows PowerShell コマンド**新規 NetworkControllerServer**します。 これにより、関数には、SDN ソフトウェア ロード バランサーを有効にします。 詳細については、次を参照してください。[新規 NetworkControllerServer](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollerserver)します。

このトピックは次のセクションで構成されます。

- [ネットワーク コント ローラー サーバーの役割をインストールします。](#bkmk_role)

- [ネットワーク コント ローラー クラスターを構成します。](#bkmk_configure)

- [ネットワーク コント ローラー アプリケーションを構成します。](#bkmk_app)

- [ネットワーク コント ローラーの展開の検証](#bkmk_validation)

- [ネットワーク コント ローラーの追加の Windows PowerShell コマンド](#bkmk_ps)

- [ネットワーク コント ローラー構成のサンプル スクリプト](#bkmk_script)

- [Kerberos 以外のデプロイのデプロイ後の手順](#bkmk_nonkerb)

## <a name="install-the-network-controller-server-role"></a>ネットワーク コント ローラー サーバーの役割をインストールします。

この手順を使用するには、仮想マシンにネットワーク コント ローラー サーバーの役割をインストールする\(VM\)します。

>[!IMPORTANT]
>物理ホストでネットワーク コント ローラー サーバーの役割を展開しないでください。 ネットワーク コント ローラーを展開するには、HYPER-V 仮想マシンでネットワーク コント ローラー サーバーの役割をインストールする必要があります\(VM\) HYPER-V ホストにインストールされています。 次の 3 つの異なるハイパースレッディング上の Vm でネットワーク コント ローラーをインストールした後\-V のホスト、ハイパースレッディングが有効にする必要があります\-ソフトウェアによるネットワーク制御の V ホスト\(SDN\)ネットワーク コント ローラーにホストを追加することで。 これにより、関数には、SDN ソフトウェア ロード バランサーを有効にします。

メンバーシップ **管理者**, 、同等の権限をこの手順を実行するために必要な最低限のですか。  

>[!NOTE]
>ネットワーク コント ローラーをインストールするを参照してください、Windows PowerShell の代わりにサーバー マネージャーを使用したい場合[サーバー マネージャーを使用して、ネットワーク コント ローラー サーバーの役割のインストール](https://technet.microsoft.com/library/mt403348.aspx)

Windows PowerShell を使用してネットワーク コント ローラーをインストールするには、Windows PowerShell プロンプトで次のコマンドを入力し、し、ENTER キーを押します。

`Install-WindowsFeature -Name NetworkController -IncludeManagementTools`

ネットワーク コント ローラーのインストールでは、コンピューターを再起動する必要があります。 これを行うには、次のコマンドを入力し、し、ENTER キーを押します。

`Restart-Computer`

## <a name="configure-the-network-controller-cluster"></a>ネットワーク コント ローラー クラスターを構成します。

ネットワーク コント ローラーがクラスターでは、高可用性とスケーラビリティ、クラスターの作成後に構成することができ、クラスター上にホストされている、ネットワーク コント ローラー アプリケーションを提供します。

>[!NOTE]
>手順を実行できます、次のセクションで、ネットワーク コント ローラーのインストールまたは実行しているリモート コンピューターから、手順を実行するリモート サーバー管理ツールの Windows Server 2016 を使用することができます、VM に対して直接Windows Server 2016 または Windows 10 のいずれか。 さらに、メンバーシップ**管理者**、またはそれと同等がこの手順を実行するために必要な最低限です。 ユーザー アカウントのメンバーである場合は、コンピューターまたはネットワーク コント ローラーをインストールした VM がドメインに参加している**Domain Users**します。

ネットワーク コント ローラー クラスターを作成するには、ノードのオブジェクトを作成し、クラスターを構成します。

### <a name="create-a-node-object"></a>ノードのオブジェクトを作成します。

ネットワーク コント ローラー クラスターのメンバーである各 vm ノード オブジェクトを作成する必要があります。

ノード オブジェクトを作成するには、Windows PowerShell のコマンド プロンプトで次のコマンドを入力し、ENTER キーを押します。 展開に適切である各パラメーターの値を追加することを確認します。  

```
New-NetworkControllerNodeObject -Name <string> -Server <String> -FaultDomain <string>-RestInterface <string> [-NodeCertificate <X509Certificate2>]
```

次の表はの各パラメーターの説明、**新規 NetworkControllerNodeObject**コマンド。

|パラメーター|説明|
|-------------|---------------|
|名前|**名前**クラスターに追加するサーバーのフレンドリ名を指定します。|
|Server|**Server**パラメーターは、ホスト名、完全修飾ドメイン名 (FQDN)、またはクラスターに追加するサーバーの IP アドレスを指定します。 ドメインに参加しているコンピューターでは、FQDN が必要です。|
|FaultDomain|**FaultDomain**パラメーターは、クラスターに追加するサーバーの障害ドメインを指定します。 このパラメーターは、サーバー クラスターに追加すると同時に障害を発生する可能性があるサーバーを定義します。 このエラーは、電源やネットワーク ソースなど、共有の物理的な依存関係があります。 障害ドメインは、通常、障害ドメイン ツリー内のより高い観点から同時に失敗する可能性がより多くのサーバーで、共有される依存関係に関連する階層を表します。 実行時に、ネットワーク コント ローラーは、クラスターの障害ドメインを認識し、別個の障害ドメインにいるように、ネットワーク コント ローラー サービスを分散しようとしています。 このプロセスにより、そのサービスとその状態の可用性が損なわれないようにを任意の 1 つの障害ドメインの障害が発生した場合こと。 障害ドメインは、階層形式で指定されます。 次に、例を示します。"Fd:/DC1、構造体、Host1 のラック 1"DC1 は、データ センターの名前、ラック 1 は、ラックの名前、Host1 が、ノードが配置されているホストの名前。|
|RestInterface|**RestInterface**パラメーターは、Representational State Transfer (REST) の通信の終了位置のノードで、インターフェイスの名前を指定します。 このネットワーク コント ローラーのインターフェイスは、ネットワークの管理のレイヤーから Northbound API 要求を受信します。|
|NodeCertificate|**NodeCertificate**パラメーターは、ネットワーク コント ローラーがコンピューターの認証に使用する証明書を指定します。 は、クラスター内の通信証明書ベースの認証を使用する場合は、証明書が必要です証明書は、ネットワーク コント ローラーのサービス間のトラフィックの暗号化にも使用されます。 証明書のサブジェクト名は、ノードの DNS 名と同じである必要があります。|

### <a name="configure-the-cluster"></a>クラスターを構成します。

クラスターを構成するには、Windows PowerShell のコマンド プロンプトで次のコマンドを入力し、ENTER キーを押します。 展開に適切である各パラメーターの値を追加することを確認します。

```
Install-NetworkControllerCluster -Node <NetworkControllerNode[]> -ClusterAuthentication <ClusterAuthentication> [-ManagementSecurityGroup <string>][-DiagnosticLogLocation <string>][-LogLocationCredential <PSCredential>] [-CredentialEncryptionCertificate <X509Certificate2>][-Credential <PSCredential>][-CertificateThumbprint <String>] [-UseSSL][-ComputerName <string>][-LogSizeLimitInMBs<UInt32>] [-LogTimeLimitInDays<UInt32>]
```

次の表はの各パラメーターの説明、**インストール NetworkControllerCluster**コマンド。
  
|パラメーター|説明|
|-------------|---------------|
|ClusterAuthentication|**ClusterAuthentication**パラメーターがノード間の通信をセキュリティで保護するために使用して、ネットワーク コント ローラーのサービス間のトラフィックの暗号化にも使用する認証の種類を指定します。 サポートされる値は**Kerberos**、 **X509**と**None**します。 Kerberos 認証は、ドメイン アカウントを使用し、ネットワーク コント ローラー ノードがドメインに参加している場合にのみ使用できます。 X509 ベースの認証を指定する場合は、NetworkControllerNode オブジェクト内の証明書を指定する必要があります。 さらに、このコマンドを実行する前に、証明書を手動でプロビジョニングする必要があります。|
|ManagementSecurityGroup|**ManagementSecurityGroup**パラメーターをリモート コンピューターからの管理コマンドレットの実行を許可するユーザーを含むセキュリティ グループの名前を指定します。 これは、ClusterAuthentication が Kerberos の場合だけです。 ローカル コンピューターのドメイン セキュリティ グループとセキュリティ グループではなくを指定する必要があります。|
|ノード|**ノード**パラメーターを使用して作成したネットワーク コント ローラー ノードの一覧を指定します、**新規 NetworkControllerNodeObject**コマンド。|
|DiagnosticLogLocation|**DiagnosticLogLocation**パラメーターが、診断ログを定期的にアップロードして共有の場所を指定します。 このパラメーターの値を指定しない場合、各ノードで、ログがローカルに格納されます。 ログは、フォルダーの %systemdrive%\windows\tracing\sdndiagnostics でローカルに格納されます。 クラスターのログは、フォルダー %systemdrive%\ProgramData\Microsoft\Service fabric \log\traces でローカルに格納されます。|
|LogLocationCredential|**LogLocationCredential**パラメーターが、ログが格納されている共有の場所にアクセスするために必要な資格情報を指定します。|
|CredentialEncryptionCertificate|**CredentialEncryptionCertificate**パラメーターは、ネットワーク コント ローラーを使用してネットワーク コント ローラー バイナリへのアクセスに使用される資格情報を暗号化する証明書を指定し、 **LogLocationCredential**指定されて 場合。 このコマンドを実行する前に、ネットワーク コント ローラー ノードのすべての証明書をプロビジョニングする必要があり、すべてのクラスター ノードで同じ証明書を登録する必要があります。 このパラメーターを使用して、ネットワーク コント ローラーのバイナリおよびログを保護するは、運用環境で使用することをお勧めします。 このパラメーターを指定しない資格情報はクリア テキストで保存され、権限のないユーザーによって悪用される可能性が。|
|資格情報|このパラメーターは、リモート コンピューターからこのコマンドを実行している場合にのみ必要です。 **資格情報**パラメーターが、ターゲット コンピューターでこのコマンドを実行するアクセス許可を持つユーザー アカウントを指定します。|
|CertificateThumbprint|このパラメーターは、リモート コンピューターからこのコマンドを実行している場合にのみ必要です。 **CertificateThumbprint**パラメーターは、のデジタル公開キー証明書 (X509) をターゲット コンピューターでこのコマンドを実行するためのアクセス許可を持つユーザー アカウントを指定します。|
|UseSSL|このパラメーターは、リモート コンピューターからこのコマンドを実行している場合にのみ必要です。 **UseSSL**パラメーターをリモート コンピューターへの接続を確立するために使用される、Secure Sockets Layer (SSL) プロトコルを指定します。 既定では、SSL は使用されません。|
|ComputerName|**ComputerName**パラメーターは、実行は次のコマンドをネットワーク コント ローラーのノードを指定します。 このパラメーターの値を指定しない場合は、ローカル コンピューターが既定で使用されます。|
|LogSizeLimitInMBs|このパラメーターは、(mb)、ネットワーク コント ローラーに格納できる最大ログ サイズを指定します。 ログは、循環形式で格納されます。 DiagnosticLogLocation が提供されている場合、このパラメーターの既定値は 40 GB です。 DiagnosticLogLocation が指定されていない場合は、ネットワーク コント ローラーのノードでログは保存され、このパラメーターの既定値は 15 GB。|
|LogTimeLimitInDays|このパラメーターは、ログが格納されている日数時間の上限を指定します。 ログは、循環形式で格納されます。 このパラメーターの既定値は、3 日間です。|

## <a name="configure-the-network-controller-application"></a>ネットワーク コント ローラー アプリケーションを構成します。
でネットワーク コント ローラー アプリケーションを構成するには、Windows PowerShell のコマンド プロンプトで次のコマンドを入力し、ENTER キーを押します。 展開に適切である各パラメーターの値を追加することを確認します。

```
Install-NetworkController -Node <NetworkControllerNode[]> -ClientAuthentication <ClientAuthentication>  [-ClientCertificateThumbprint <string[]>]  [-ClientSecurityGroup <string>] -ServerCertificate <X509Certificate2> [-RESTIPAddress <String>] [-RESTName <String>] [-Credential <PSCredential>][-CertificateThumbprint <String> ] [-UseSSL]
```

次の表はの各パラメーターの説明、**インストール NetworkController**コマンド。

|パラメーター|説明|
|-------------|---------------|
|ClientAuthentication|**ClientAuthentication**パラメーターは、REST とネットワーク コント ローラー間の通信を保護するために使用される認証の種類を指定します。 サポートされる値は**Kerberos**、 **X509**と**None**します。 Kerberos 認証は、ドメイン アカウントを使用し、ネットワーク コント ローラー ノードがドメインに参加している場合にのみ使用できます。 X509 ベースの認証を指定する場合は、NetworkControllerNode オブジェクト内の証明書を指定する必要があります。 さらに、このコマンドを実行する前に、証明書を手動でプロビジョニングする必要があります。|
|ノード|**ノード**パラメーターを使用して作成したネットワーク コント ローラー ノードの一覧を指定します、**新規 NetworkControllerNodeObject**コマンド。|
|ClientCertificateThumbprint|ネットワーク コント ローラーのクライアントの証明書ベースの認証を使用している場合にのみ、このパラメーターが必要です。 **ClientCertificateThumbprint** Northbound レイヤー上のクライアントに登録されている証明書の拇印を指定します。|
|ServerCertificate|**ServerCertificate**パラメーターは、ネットワーク コント ローラーがクライアントに身元を証明するために使用する証明書を指定します。 サーバー証明書は、拡張キー使用法の拡張機能では、サーバー認証の目的を含める必要があり、クライアントによって信頼されている CA からネットワーク コント ローラーに発行する必要があります。|
|RESTIPAddress|値を指定する必要はありません**RESTIPAddress**ネットワーク コント ローラーの単一ノード展開にします。 複数ノードの展開、 **RESTIPAddress**パラメーターは、CIDR 表記法での REST エンドポイントの IP アドレスを指定します。 たとえば、192.168.1.10/24 します。 サブジェクト名値**ServerCertificate**の値に解決する必要があります、 **RESTIPAddress**パラメーター。 同じサブネット上のすべてのノードが、すべての複数ノード ネットワーク コント ローラーの展開のこのパラメーターを指定する必要があります。 使用する必要があるノードが異なるサブネット上にある場合、 **RestName**パラメーターを使用してではなく**RESTIPAddress**します。|
|RestName|値を指定する必要はありません**RestName**ネットワーク コント ローラーの単一ノード展開にします。 唯一の時間の値を指定する必要があります**RestName**は、複数ノードの展開は異なるサブネット上にあるノードがある場合。 複数ノードの展開、 **RestName**パラメーターは、ネットワーク コント ローラー クラスターの FQDN を指定します。|
|ClientSecurityGroup|**ClientSecurityGroup**パラメーターを持つメンバーは、ネットワーク コント ローラーのクライアントの Active Directory セキュリティ グループの名前を指定します。 このパラメーターは、の Kerberos 認証を使用する場合にのみ必要**ClientAuthentication**します。 セキュリティ グループは、REST Api にアクセスできるアカウントを含める必要があり、セキュリティ グループを作成し、このコマンドを実行する前にメンバーを追加する必要があります。|
|資格情報|このパラメーターは、リモート コンピューターからこのコマンドを実行している場合にのみ必要です。 **資格情報**パラメーターが、ターゲット コンピューターでこのコマンドを実行するアクセス許可を持つユーザー アカウントを指定します。|
|CertificateThumbprint|このパラメーターは、リモート コンピューターからこのコマンドを実行している場合にのみ必要です。 **CertificateThumbprint**パラメーターは、のデジタル公開キー証明書 (X509) をターゲット コンピューターでこのコマンドを実行するためのアクセス許可を持つユーザー アカウントを指定します。|
|UseSSL|このパラメーターは、リモート コンピューターからこのコマンドを実行している場合にのみ必要です。 **UseSSL**パラメーターをリモート コンピューターへの接続を確立するために使用される、Secure Sockets Layer (SSL) プロトコルを指定します。 既定では、SSL は使用されません。|

ネットワーク コント ローラー アプリケーションの構成を完了すると、ネットワーク コント ローラーの配置が完了しました。

## <a name="network-controller-deployment-validation"></a>ネットワーク コント ローラーの展開の検証

ネットワーク コント ローラーの展開を検証するには、ネットワーク コント ローラーに、資格情報を追加し、資格情報を取得できます。

メンバーシップ、ClientAuthentication メカニズムとして Kerberos を使用しているかどうか、 **ClientSecurityGroup**この手順を実行するために必要な最小値は、作成しました。

**手順:**

1.  クライアント コンピューター、ClientAuthentication メカニズムとして Kerberos を使用する場合でログインのメンバーであるユーザー アカウント、 **ClientSecurityGroup**します。

2. Windows PowerShell を開き、ネットワーク コント ローラーに、資格情報を追加するには、次のコマンドを入力し、ENTER キーを押します。 展開に適切である各パラメーターの値を追加することを確認します。

    ```
    $cred=New-Object Microsoft.Windows.Networkcontroller.credentialproperties
    $cred.type="usernamepassword"
    $cred.username="admin"
    $cred.value="abcd"

    New-NetworkControllerCredential -ConnectionUri https://networkcontroller -Properties $cred -ResourceId cred1
    ```

3. ネットワーク コント ローラーに追加した、資格情報を取得するには、次のコマンドを入力し、ENTER キーを押します。 展開に適切である各パラメーターの値を追加することを確認します。

    ```
    Get-NetworkControllerCredential -ConnectionUri https://networkcontroller -ResourceId cred1  
    ```

4. コマンドの出力例を次のようになりますが、出力結果を確認します。

    ```
    Tags                   :
    ResourceRef     : /credentials/cred1
    CreatedTime    : 1/1/0001 12:00:00 AM
    InstanceId        : e16ffe62-a701-4d31-915e-7234d4bc5a18
    Etag                  : W/"1ec59631-607f-4d3e-ac78-94b0822f3a9d"
    ResourceMetadata :
    ResourceId       : cred1
    Properties       : Microsoft.Windows.NetworkController.CredentialProperties
    ```

    > [!NOTE]
    > 実行すると、 **Get NetworkControllerCredential**コマンド、資格情報のプロパティを一覧表示、ドット演算子を使用して、コマンドの出力を変数に割り当てることができます。 たとえば、$cred です。プロパティ。

## <a name="additional-windows-powershell-commands-for-network-controller"></a>ネットワーク コント ローラーの追加の Windows PowerShell コマンド

ネットワーク コント ローラーを展開した後、展開を管理する Windows PowerShell コマンドを使用できます。 デプロイを行うことができます、変更の一部を次に示します。

- ネットワーク コント ローラーのノード、クラスター、およびアプリケーションの設定を変更します。

- ネットワーク コント ローラーがクラスターとアプリケーションを削除します。

- などの追加、削除、有効化、およびノードを無効にすると、ネットワーク コント ローラーのクラスター ノードを管理します。

次の表では、これらのタスクの実行に使用できるコマンドを Windows PowerShell の構文を提供します。

|タスク|コマンド|構文|
|--------|-------|----------|
|ネットワーク コント ローラー クラスターの設定を変更します。|セット NetworkControllerCluster|`Set-NetworkControllerCluster [-ManagementSecurityGroup <string>][-Credential <PSCredential>] [-computerName <string>][-CertificateThumbprint <String> ] [-UseSSL]`
|ネットワーク コント ローラー アプリケーション設定を変更します。|セット NetworkController|`Set-NetworkController [-ClientAuthentication <ClientAuthentication>] [-Credential <PSCredential>] [-ClientCertificateThumbprint <string[]>] [-ClientSecurityGroup <string>] [-ServerCertificate <X509Certificate2>] [-RestIPAddress <String>] [-ComputerName <String>][-CertificateThumbprint <String> ] [-UseSSL]`
|ネットワーク コント ローラーのノードの設定を変更します。|セット NetworkControllerNode|`Set-NetworkControllerNode -Name <string> > [-RestInterface <string>] [-NodeCertificate <X509Certificate2>] [-Credential <PSCredential>] [-ComputerName <string>][-CertificateThumbprint <String> ] [-UseSSL]`
|ネットワーク コント ローラーの診断設定を変更します。|セット NetworkControllerDiagnostic|`Set-NetworkControllerDiagnostic [-LogScope <string>] [-DiagnosticLogLocation <string>] [-LogLocationCredential <PSCredential>] [-UseLocalLogLocation] >] [-LogLevel <loglevel>][-LogSizeLimitInMBs <uint32>] [-LogTimeLimitInDays <uint32>] [-Credential <PSCredential>] [-ComputerName <string>][-CertificateThumbprint <String> ] [-UseSSL]`
|ネットワーク コント ローラー アプリケーションを削除します。|アンインストール NetworkController|`Uninstall-NetworkController [-Credential <PSCredential>][-ComputerName <string>] [-CertificateThumbprint <String> ] [-UseSSL]`
|ネットワーク コント ローラー クラスターを削除します。|アンインストール NetworkControllerCluster|`Uninstall-NetworkControllerCluster [-Credential <PSCredential>][-ComputerName <string>][-CertificateThumbprint <String> ] [-UseSSL]`
|ネットワーク コント ローラーがクラスターにノードを追加します。|追加 NetworkControllerNode|`Add-NetworkControllerNode -FaultDomain <String> -Name <String> -RestInterface <String> -Server <String> [-CertificateThumbprint <String> ] [-ComputerName <String> ] [-Credential <PSCredential> ] [-Force] [-NodeCertificate <X509Certificate2> ] [-PassThru] [-UseSsl]`
|ネットワーク コント ローラーのクラスター ノードを無効にします。|無効にする NetworkControllerNode|`Disable-NetworkControllerNode -Name <String> [-CertificateThumbprint <String> ] [-ComputerName <String> ] [-Credential <PSCredential> ] [-PassThru] [-UseSsl]`
|ネットワーク コント ローラーのクラスター ノードを有効にします。|有効にする NetworkControllerNode|`Enable-NetworkControllerNode -Name <String> [-CertificateThumbprint <String> ] [-ComputerName <String> ] [-Credential <PSCredential> ] [-PassThru] [-UseSsl]`
|ネットワーク コント ローラーのノードをクラスターから削除します。|削除 NetworkControllerNode|`Remove-NetworkControllerNode [-CertificateThumbprint <String> ] [-ComputerName <String> ] [-Credential <PSCredential> ] [-Force] [-Name <String> ] [-PassThru] [-UseSsl]`

>[!NOTE]
>ネットワーク コント ローラーの Windows PowerShell コマンドは、TechNet ライブラリの「[ネットワーク コント ローラー コマンドレット](https://technet.microsoft.com/library/mt576401.aspx)します。

## <a name="sample-network-controller-configuration-script"></a>ネットワーク コント ローラー構成のサンプル スクリプト

次のサンプル構成スクリプトでは、マルチノード ネットワーク コント ローラーのクラスターを作成し、ネットワーク コント ローラー アプリケーションをインストールする方法を示します。 さらに、$cert 変数では、サブジェクト名の文字列"networkController.contoso.com"に一致するローカル コンピューターの証明書ストアから証明書を選択します。

```
$a = New-NetworkControllerNodeObject -Name Node1 -Server NCNode1.contoso.com -FaultDomain fd:/rack1/host1 -RestInterface Internal
$b = New-NetworkControllerNodeObject -Name Node2 -Server NCNode2.contoso.com -FaultDomain fd:/rack1/host2 -RestInterface Internal
$c = New-NetworkControllerNodeObject -Name Node3 -Server NCNode3.contoso.com -FaultDomain fd:/rack1/host3 -RestInterface Internal

$cert= get-item Cert:\LocalMachine\My | get-ChildItem | where {$_.Subject -imatch "networkController.contoso.com" }

Install-NetworkControllerCluster -Node @($a,$b,$c)  -ClusterAuthentication Kerberos -DiagnosticLogLocation \\share\Diagnostics - ManagementSecurityGroup Contoso\NCManagementAdmins -CredentialEncryptionCertificate $cert  
Install-NetworkController -Node @($a,$b,$c) -ClientAuthentication Kerberos -ClientSecurityGroup Contoso\NCRESTClients -ServerCertificate $cert -RestIpAddress 10.0.0.1/24
```

## <a name="post-deployment-steps-for-non-kerberos-deployments"></a>Kerberos 以外のデプロイのデプロイ後の手順

ネットワーク コント ローラーの展開で Kerberos を使用していない場合は、証明書を展開する必要があります。

詳細については、次を参照してください。[ネットワーク コント ローラーの展開後の手順](../technologies/network-controller/post-deploy-steps-nc.md)します。


