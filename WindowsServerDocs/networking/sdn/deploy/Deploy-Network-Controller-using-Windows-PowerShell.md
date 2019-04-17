---
title: Windows PowerShell を使用してネットワーク コントローラーを展開します。
description: このトピックでは、Windows PowerShell を使用して、コンピューターまたは Windows Server 2016 を実行している仮想マシン (Vm) の 1 つまたは複数のネットワーク コントローラーを展開する手順について説明します。
manager: brianlic
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
ms.openlocfilehash: cfd06662f317381fb77bf31db5ed60c2489ff871
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="deploy-network-controller-using-windows-powershell"></a>Windows PowerShell を使用してネットワーク コントローラーを展開します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックで Windows PowerShell を使用して、1 つまたは複数仮想マシン (Vm) Windows Server 2016 を実行しているネットワーク コントローラーを展開する手順を示します。

>[!IMPORTANT]
>物理ホスト上で、ネットワーク コントローラー サーバーの役割を展開しないでください。 ネットワーク コントローラーを展開するには、Hyper-V 仮想マシンのネットワーク コントローラー サーバーの役割をインストールする必要があります \(VM\) Hyper-V ホストにインストールされています。 Windows PowerShell コマンドを使用してネットワーク コントローラーにホストを追加することでのソフトウェアがネットワーク定義 \(SDN\) Hyper\ V ホストを有効にする必要があります Vm 上で次の 3 つの異なる Hyper\ V ホストでネットワーク コントローラーをインストールした後**新規 NetworkControllerServer**します。 これにより、有効にすると、SDN ソフトウェア ロード バランサーが機能します。 詳細については、次を参照してください。[新規 NetworkControllerServer](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollerserver)します。

このトピックには、次のセクションが含まれています。

- [ネットワーク コントローラー サーバーの役割をインストールします。](#bkmk_role)

- [ネットワーク コントローラー クラスターを構成します。](#bkmk_configure)

- [ネットワーク コントローラーのアプリケーションを構成します。](#bkmk_app)

- [ネットワーク コントローラーの展開の検証](#bkmk_validation)

- [ネットワーク コントローラーの他の Windows PowerShell コマンド](#bkmk_ps)

- [ネットワーク コントローラー構成のサンプル スクリプト](#bkmk_script)

- [後の Post-DeploymentKerberos 以外の展開の手順を実行します。](#bkmk_nonkerb)

## <a name="bkmk_role"></a>ネットワーク コントローラー サーバーの役割をインストールします。

この手順を使用するには、バーチャル マシン上のネットワーク コントローラー サーバーの役割のインストールを \(VM\) します。

>[!IMPORTANT]
>物理ホスト上で、ネットワーク コントローラー サーバーの役割を展開しないでください。 ネットワーク コントローラーを展開するには、Hyper-V 仮想マシンのネットワーク コントローラー サーバーの役割をインストールする必要があります \(VM\) Hyper-V ホストにインストールされています。 Vm 上で次の 3 つの異なる Hyper\ V ホストでネットワーク コントローラーをインストールした後、ネットワーク コントローラーにホストを追加することでのソフトウェアがネットワーク定義 \(SDN\) Hyper\ V ホストを有効にする必要があります。 これにより、有効にすると、SDN ソフトウェア ロード バランサーが機能します。

メンバーシップ**管理者**、相当するものでは、この手順を実行するために必要な最低限またはします。  

>[!NOTE]
>Windows PowerShell ではなくでサーバー マネージャーを使用してを参照してくださいネットワーク コントローラーをインストールする場合[サーバー マネージャーを使用して、ネットワーク コントローラー サーバーの役割のインストール](https://technet.microsoft.com/library/mt403348.aspx)

Windows PowerShell を使用してネットワーク コントローラーをインストールするには、Windows PowerShell プロンプトで次のコマンドを入力し、Enter キーを押します。

`Install-WindowsFeature -Name NetworkController -IncludeManagementTools`

ネットワーク コントローラーのインストールでは、コンピューターを再起動する必要があります。 ためには、次のコマンドを入力し、Enter キーを押します。

`Restart-Computer`

## <a name="bkmk_configure"></a>ネットワーク コントローラー クラスターを構成します。

ネットワーク コントローラーのクラスターでは、高可用性とスケーラビリティをクラスターの作成後に構成でき、クラスター上にホストされている、ネットワーク コントローラー アプリケーションを提供します。

>[!NOTE]
>実行できる手順は、次のセクションでは、場所、ネットワーク コントローラーのインストールまたは Windows Server 2016 または Windows 10 のいずれかを実行しているリモート コンピューターから、手順を実行するリモート サーバー管理ツールの Windows Server 2016 を使用することができます、VM に対して直接します。 また、メンバーシップ**管理者**、相当するものでは、この手順を実行するために必要な最低限またはします。 自分のユーザー アカウントのメンバーである必要があります、コンピューターまたは VM のネットワーク コントローラーをインストールしたが、ドメインに参加させる場合**Domain Users**します。

ネットワーク コントローラー クラスターを作成するにはノード オブジェクトを作成し、クラスターを構成します。

### <a name="create-a-node-object"></a>ノードのオブジェクトを作成します。

ネットワーク コントローラーがクラスターのメンバーになっている各 VM のノード オブジェクトを作成する必要があります。

ノード オブジェクトを作成するには、Windows PowerShell のコマンド プロンプトで次のコマンドを入力し、Enter キーを押します。 展開に適切である各パラメーターの値を追加することを確認します。  

```
New-NetworkControllerNodeObject -Name <string> -Server <String> -FaultDomain <string>-RestInterface <string> [-NodeCertificate <X509Certificate2>]
```

次の表の各パラメーターの説明を提供する、**新規 NetworkControllerNodeObject**コマンド。

|パラメーター|説明|
|-------------|---------------|
|名|**名**クラスターに追加するサーバーのフレンドリ名を指定します。|
|サーバー|**サーバー**パラメーターは、ホスト名、完全修飾ドメイン名 (FQDN)、またはクラスターに追加するサーバーの IP アドレスを指定します。 ドメインに参加しているコンピューターでは、FQDN が必要です。|
|FaultDomain|**FaultDomain**パラメーターがクラスターに追加するサーバーの障害ドメインを指定します。 このパラメーターは、サーバーをクラスターに追加するサーバーと同時に障害が発生する可能性がありますを定義します。 このエラーは、電源とネットワーク ソースなど、共有の物理的な依存関係があります。 障害ドメインは、通常、フォールト ドメイン ツリー内のより高いポイントから一緒に失敗する可能性がより多くのサーバーで、これらの共有依存関係に関連する階層を表します。 実行時にネットワーク コントローラー、クラスターでの障害ドメインが考慮しようし、別個の障害ドメイン内にあるできるように、ネットワーク コントローラーのサービスを展開します。 このプロセスでは、任意の 1 つの障害ドメインに障害が発生した場合、そのサービスとその状態の可用性が侵害されないようにします。 障害ドメインは、階層の形式で指定されます。 例:"Fd: DC1/ラック 1/Host1/"、DC1 は、データ センターの名前、ラック 1 のラック マウント型名があり Host1 が、ノードが配置されているホストの名前。|
|RestInterface|**RestInterface**パラメーターは、Representational State Transfer (REST) 通信が終了したノードで、インターフェイスの名前を指定します。 このネットワーク コントローラーのインターフェイスは、ネットワークの管理レイヤーから Northbound API 要求を受信します。|
|NodeCertificate|**NodeCertificate**パラメーターは、ネットワーク コントローラーは、コンピューター認証に証明書を指定します。 クラスター内の通信に証明書ベースの認証を使用する場合は、証明書が必要証明書は、ネットワーク コントローラー サービス間のトラフィックの暗号化にも使用されます。 証明書のサブジェクト名は、ノードの DNS 名と同じである必要があります。|

### <a name="configure-the-cluster"></a>クラスターを構成します。

クラスターを構成するには、Windows PowerShell のコマンド プロンプトで次のコマンドを入力し、Enter キーを押します。 展開に適切である各パラメーターの値を追加することを確認します。

```
Install-NetworkControllerCluster -Node <NetworkControllerNode[]> -ClusterAuthentication <ClusterAuthentication> [-ManagementSecurityGroup <string>][-DiagnosticLogLocation <string>][-LogLocationCredential <PSCredential>] [-CredentialEncryptionCertificate <X509Certificate2>][-Credential <PSCredential>][-CertificateThumbprint <String>] [-UseSSL][-ComputerName <string>][-LogSizeLimitInMBs<UInt32>] [-LogTimeLimitInDays<UInt32>]
```

次の表の各パラメーターの説明を提供する、**インストール NetworkControllerCluster**コマンド。
  
|パラメーター|説明|
|-------------|---------------|
|ClusterAuthentication|**ClusterAuthentication**パラメーターは、ノード間で通信を保護するために使用して、ネットワーク コントローラー サービス間のトラフィックの暗号化にも使用する認証の種類を指定します。 サポートされる値は**Kerberos**、**X509**と**None**します。 Kerberos 認証では、ドメイン アカウントを使用し、ネットワーク コントローラーのノードがドメインに参加している場合にのみ使用できます。 X509 ベースの認証を指定する場合は、NetworkControllerNode オブジェクト内の証明書を指定する必要があります。 さらに、このコマンドを実行する前に、証明書を手動でプロビジョニングする必要があります。|
|ManagementSecurityGroup|**ManagementSecurityGroup**パラメーターをリモート コンピューターから管理コマンドレットの実行を許可するユーザーを含むセキュリティ グループの名前を指定します。 これは、ClusterAuthentication が Kerberos 場合だけです。 ローカル コンピューターのドメイン セキュリティ グループとセキュリティ グループではなくを指定する必要があります。|
|ノード|**ノード**パラメーターを使用して作成したネットワーク コントローラーのノードの一覧を指定する、**新規 NetworkControllerNodeObject**コマンド。|
|DiagnosticLogLocation|**DiagnosticLogLocation**診断ログが定期的にアップロードされた共有の場所を指定します。 このパラメーターの値を指定しない場合、ログは各ノードでローカルに保存します。 ログは、フォルダー %systemdrive%\windows\tracing\sdndiagnostics にローカルに保存されます。 クラスターのログは、フォルダー %systemdrive%\ProgramData\Microsoft\Service fabric \log\traces にローカルに保存されます。|
|LogLocationCredential|**LogLocationCredential**パラメーターは、ログが格納されている共有の場所にアクセスするために必要な資格情報を指定します。|
|CredentialEncryptionCertificate|**CredentialEncryptionCertificate**パラメーターは、ネットワーク コントローラーを使用してネットワーク コントローラーのバイナリ ファイルにアクセスするために使用する資格情報の暗号化証明書を指定し、**LogLocationCredential**指定されている場合、します。 このコマンドを実行する前にネットワーク コントローラーのノードのすべての証明書をプロビジョニングする必要があり、すべてのクラスター ノードで同じ証明書を登録する必要があります。 このパラメーターを使用してネットワーク コントローラーのバイナリとログを保護するのには、運用環境で使用することをお勧めします。 このパラメーターは、資格情報はクリア テキストで保存され、権限のないユーザーによって悪用される可能性が。|
|資格情報|このパラメーターは、リモート コンピューターからこのコマンドを実行している場合にのみ必要です。 **Credential**パラメーターはターゲット コンピューターでこのコマンドを実行するアクセス許可を持つユーザー アカウントを指定します。|
|CertificateThumbprint|このパラメーターは、リモート コンピューターからこのコマンドを実行している場合にのみ必要です。 **CertificateThumbprint**パラメーターは、のデジタル公開キー証明書 (X509) をターゲット コンピューターでこのコマンドを実行するためのアクセス許可を持つユーザー アカウントを指定します。|
|UseSSL|このパラメーターは、リモート コンピューターからこのコマンドを実行している場合にのみ必要です。 **UseSSL**パラメーターは、リモート コンピューターへの接続を確立するために使用される、Secure Sockets Layer (SSL) プロトコルを指定します。 既定では、SSL は使用されません。|
|コンピューター名|**ComputerName**パラメーターにこのコマンドは、実行、ネットワーク コントローラー ノードを指定します。 このパラメーターの値を指定しないと、既定では、ローカル コンピューターが使用されます。|
|LogSizeLimitInMBs|このパラメーターは、mb 単位でネットワーク コントローラーを格納できる最大ログ サイズを指定します。 ログは、循環形式に格納されます。 DiagnosticLogLocation が提供されると、このパラメーターの既定値は 40 GB です。 DiagnosticLogLocation が指定されていない場合は、ログは、ネットワーク コントローラーのノード上で保存され、このパラメーターの既定値は 15 GB。|
|LogTimeLimitInDays|このパラメーターは、日、ログが格納されている時間の上限を指定します。 ログは、循環形式に格納されます。 このパラメーターの既定値は、3 日間です。|

## <a name="bkmk_app"></a>ネットワーク コントローラーのアプリケーションを構成します。
ネットワーク コントローラーのアプリケーションを構成するのには、Windows PowerShell のコマンド プロンプトで次のコマンドを入力し、Enter キーを押します。 展開に適切である各パラメーターの値を追加することを確認します。

```
Install-NetworkController -Node <NetworkControllerNode[]> -ClientAuthentication <ClientAuthentication>  [-ClientCertificateThumbprint <string[]>]  [-ClientSecurityGroup <string>] -ServerCertificate <X509Certificate2> [-RESTIPAddress <String>] [-RESTName <String>] [-Credential <PSCredential>][-CertificateThumbprint <String> ] [-UseSSL]
```

次の表の各パラメーターの説明を提供する、**インストール NetworkController**コマンド。

|パラメーター|説明|
|-------------|---------------|
|クライアント認証|**ClientAuthentication**パラメーターは、残りの部分とネットワーク コントローラー間の通信を保護するために使用される認証の種類を指定します。 サポートされる値は**Kerberos**、**X509**と**None**します。 Kerberos 認証では、ドメイン アカウントを使用し、ネットワーク コントローラーのノードがドメインに参加している場合にのみ使用できます。 X509 ベースの認証を指定する場合は、NetworkControllerNode オブジェクト内の証明書を指定する必要があります。 さらに、このコマンドを実行する前に、証明書を手動でプロビジョニングする必要があります。|
|ノード|**ノード**パラメーターを使用して作成したネットワーク コントローラーのノードの一覧を指定する、**新規 NetworkControllerNodeObject**コマンド。|
|ClientCertificateThumbprint|ネットワーク コントローラーのクライアントの証明書ベースの認証を使用している場合にのみ、このパラメーターが必要です。 **ClientCertificateThumbprint**パラメーターは、Northbound レイヤー上のクライアントに登録されている証明書の拇印を指定します。|
|サーバー証明書|**サーバー証明書**パラメーターは、ネットワーク コントローラーを使用してクライアントに身元を証明する証明書を指定します。 サーバー証明書は、拡張キー使用法の拡張機能でサーバー認証の目的を含める必要があり、ネットワーク コントローラーにクライアントによって信頼されている CA によって発行される必要があります。|
|RESTIPAddress|値を指定する必要はありません**RESTIPAddress**ネットワーク コントローラーの 1 つのノード展開を使用します。 マルチノード展開で、**RESTIPAddress** CIDR 表記で REST エンドポイントの IP アドレスを指定します。 たとえば、192.168.1.10/24 です。 サブジェクト名の値の**サーバー証明書**の値に解決される必要があります、**RESTIPAddress**パラメーター。 このパラメーターは、同じサブネット上のすべてのノードが複数ノード ネットワーク コントローラーの展開をすべての指定する必要があります。 使用する必要がありますノードが異なるサブネット上にある場合、**RestName**パラメーターを使用せずに**RESTIPAddress**します。|
|RestName|値を指定する必要はありません**RestName**ネットワーク コントローラーの 1 つのノード展開を使用します。 唯一の時間の値を指定する必要があります**RestName**は複数ノード展開の場合は、異なるサブネット上にあるノードを持つ場合にします。 マルチノード展開で、**RestName**パラメーターは、ネットワーク コントローラーがクラスターの FQDN を指定します。|
|ClientSecurityGroup|**ClientSecurityGroup**パラメーターは、Active Directory セキュリティ グループのメンバーを含む、クライアントのネットワーク コントローラーの名前を指定します。 Kerberos 認証を使用する場合にのみ、このパラメーターは必須**ClientAuthentication**します。 元の REST API は、アクセス アカウントを含める必要があります、セキュリティ グループとセキュリティ グループを作成し、このコマンドを実行する前にメンバーを追加する必要があります。|
|資格情報|このパラメーターは、リモート コンピューターからこのコマンドを実行している場合にのみ必要です。 **Credential**パラメーターはターゲット コンピューターでこのコマンドを実行するアクセス許可を持つユーザー アカウントを指定します。|
|CertificateThumbprint|このパラメーターは、リモート コンピューターからこのコマンドを実行している場合にのみ必要です。 **CertificateThumbprint**パラメーターは、のデジタル公開キー証明書 (X509) をターゲット コンピューターでこのコマンドを実行するためのアクセス許可を持つユーザー アカウントを指定します。|
|UseSSL|このパラメーターは、リモート コンピューターからこのコマンドを実行している場合にのみ必要です。 **UseSSL**パラメーターは、リモート コンピューターへの接続を確立するために使用される、Secure Sockets Layer (SSL) プロトコルを指定します。 既定では、SSL は使用されません。|

ネットワーク コントローラーのアプリケーションの構成を完了すると、ネットワーク コントローラーの展開が完了します。

## <a name="bkmk_validation"></a>ネットワーク コントローラーの展開の検証

ネットワーク コントローラーの展開を検証するには、ネットワーク コントローラーに資格情報を追加し、資格情報を取得できます。

クライアント認証メカニズム、メンバーシップとして Kerberos を使用しているかどうか、**ClientSecurityGroup**この手順を実行するために必要な最小値は、作成しました。

#### <a name="to-validate-deployment-of-network-controller"></a>ネットワーク コントローラーの展開を検証するには

1.  クライアント コンピューターで、クライアント認証メカニズムとして Kerberos を使用する場合でログオンのメンバーであるユーザー アカウント、**ClientSecurityGroup**します。

2. Windows PowerShell を開き、ネットワーク コントローラーに資格情報を追加するには、次のコマンドを入力し、Enter キーを押します。 展開に適切である各パラメーターの値を追加することを確認します。

    ```
    $cred=New-Object Microsoft.Windows.Networkcontroller.credentialproperties
    $cred.type="usernamepassword"
    $cred.username="admin"
    $cred.value="abcd"

    New-NetworkControllerCredential -ConnectionUri https://networkcontroller -Properties $cred -ResourceId cred1
    ```

3. ネットワーク コントローラーに追加した資格情報を取得するには、次のコマンドを入力し、Enter キーを押します。 展開に適切である各パラメーターの値を追加することを確認します。

    ```
    Get-NetworkControllerCredential -ConnectionUri https://networkcontroller -ResourceId cred1  
    ```

4. コマンドの出力例を次のようにする必要がありますが、出力結果を確認します。

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
    > 実行すると、**Get NetworkControllerCredential**コマンド、資格情報のプロパティの一覧を表示する、ドット演算子を使用して、コマンドの出力を変数に割り当てることができます。 たとえば、$cred です。プロパティです。

## <a name="bkmk_ps"></a>ネットワーク コントローラーの他の Windows PowerShell コマンド

ネットワーク コントローラーを展開した後を管理および展開を変更する Windows PowerShell コマンドを使用することができます。 次に、いくつかの変更を展開を行うことができます。

- ネットワーク コントローラーのノード、クラスター、およびアプリケーションの設定を変更します。

- ネットワーク コントローラー クラスターとアプリケーションを削除します。

- などの追加、削除、有効にすると、およびノードを無効にすると、ネットワーク コントローラーのクラスター ノードを管理します。

次の表では、これらのタスクの実行に使用できるコマンドを Windows PowerShell の構文を示します。

|タスク|コマンド|構文|
|--------|-------|----------|
|ネットワーク コントローラー クラスター設定を変更します。|Set-NetworkControllerCluster|`Set-NetworkControllerCluster [-ManagementSecurityGroup <string>][-Credential <PSCredential>] [-computerName <string>][-CertificateThumbprint <String> ] [-UseSSL]`
|ネットワーク コントローラー アプリケーション設定を変更します。|Set-NetworkController|`Set-NetworkController [-ClientAuthentication <ClientAuthentication>] [-Credential <PSCredential>] [-ClientCertificateThumbprint <string[]>] [-ClientSecurityGroup <string>] [-ServerCertificate <X509Certificate2>] [-RestIPAddress <String>] [-ComputerName <String>][-CertificateThumbprint <String> ] [-UseSSL]`
|ネットワーク コントローラーのノードの設定を変更します。|Set-NetworkControllerNode|`Set-NetworkControllerNode -Name <string> > [-RestInterface <string>] [-NodeCertificate <X509Certificate2>] [-Credential <PSCredential>] [-ComputerName <string>][-CertificateThumbprint <String> ] [-UseSSL]`
|ネットワーク コントローラー診断設定を変更します。|Set-NetworkControllerDiagnostic|`Set-NetworkControllerDiagnostic [-LogScope <string>] [-DiagnosticLogLocation <string>] [-LogLocationCredential <PSCredential>] [-UseLocalLogLocation] >] [-LogLevel <loglevel>][-LogSizeLimitInMBs <uint32>] [-LogTimeLimitInDays <uint32>] [-Credential <PSCredential>] [-ComputerName <string>][-CertificateThumbprint <String> ] [-UseSSL]`
|ネットワーク コントローラーのアプリケーションを削除します。|Uninstall-NetworkController|`Uninstall-NetworkController [-Credential <PSCredential>][-ComputerName <string>] [-CertificateThumbprint <String> ] [-UseSSL]`
|ネットワーク コントローラーのクラスタを削除します。|Uninstall-NetworkControllerCluster|`Uninstall-NetworkControllerCluster [-Credential <PSCredential>][-ComputerName <string>][-CertificateThumbprint <String> ] [-UseSSL]`
|ネットワーク コントローラーがクラスターにノードを追加します。|Add-NetworkControllerNode|`Add-NetworkControllerNode -FaultDomain <String> -Name <String> -RestInterface <String> -Server <String> [-CertificateThumbprint <String> ] [-ComputerName <String> ] [-Credential <PSCredential> ] [-Force] [-NodeCertificate <X509Certificate2> ] [-PassThru] [-UseSsl]`
|ネットワーク コントローラーのクラスター ノードを無効にします。|Disable-NetworkControllerNode|`Disable-NetworkControllerNode -Name <String> [-CertificateThumbprint <String> ] [-ComputerName <String> ] [-Credential <PSCredential> ] [-PassThru] [-UseSsl]`
|ネットワーク コントローラーのクラスター ノードを有効にします。|Enable-NetworkControllerNode|`Enable-NetworkControllerNode -Name <String> [-CertificateThumbprint <String> ] [-ComputerName <String> ] [-Credential <PSCredential> ] [-PassThru] [-UseSsl]`
|ネットワーク コントローラーのノードをクラスターから削除します。|Remove-NetworkControllerNode|`Remove-NetworkControllerNode [-CertificateThumbprint <String> ] [-ComputerName <String> ] [-Credential <PSCredential> ] [-Force] [-Name <String> ] [-PassThru] [-UseSsl]`

>[!NOTE]
>ネットワーク コントローラーの Windows PowerShell のコマンドは、TechNet ライブラリの「[ネットワーク コントローラー コマンドレット](https://technet.microsoft.com/library/mt576401.aspx)します。

## <a name="bkmk_script"></a>ネットワーク コントローラー構成のサンプル スクリプト

次のサンプル構成スクリプトでは、ネットワーク コントローラーのマルチノード クラスターを作成し、ネットワーク コントローラーのアプリケーションをインストールする方法を示します。 さらに、$cert 変数は、サブジェクト名の文字列"networkController.contoso.com"に一致するローカル コンピューターの証明書ストアから証明書を選択します。

```
$a = New-NetworkControllerNodeObject -Name Node1 -Server NCNode1.contoso.com -FaultDomain fd:/rack1/host1 -RestInterface Internal
$b = New-NetworkControllerNodeObject -Name Node2 -Server NCNode2.contoso.com -FaultDomain fd:/rack1/host2 -RestInterface Internal
$c = New-NetworkControllerNodeObject -Name Node3 -Server NCNode3.contoso.com -FaultDomain fd:/rack1/host3 -RestInterface Internal

$cert= get-item Cert:\LocalMachine\My | get-ChildItem | where {$_.Subject -imatch "networkController.contoso.com" }

Install-NetworkControllerCluster -Node @($a,$b,$c)  -ClusterAuthentication Kerberos -DiagnosticLogLocation \\share\Diagnostics - ManagementSecurityGroup Contoso\NCManagementAdmins -CredentialEncryptionCertificate $cert  
Install-NetworkController -Node @($a,$b,$c) -ClientAuthentication Kerberos -ClientSecurityGroup Contoso\NCRESTClients -ServerCertificate $cert -RestIpAddress 10.0.0.1/24
```

## <a name="bkmk_nonkerb"></a>展開後の手順の非-Kerberos の展開

ネットワーク コントローラーの展開で Kerberos を使用していない場合は、証明書を展開する必要があります。

詳細については、次を参照してください。[ネットワーク コントローラーの展開後の手順](../technologies/network-controller/post-deploy-steps-nc.md)します。


