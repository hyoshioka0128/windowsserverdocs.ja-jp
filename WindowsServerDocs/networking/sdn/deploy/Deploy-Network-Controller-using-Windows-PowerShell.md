---
title: Windows PowerShell を使用してネットワーク コントローラーを展開する
description: このトピックでは、windows PowerShell を使用して、Windows Server 2016 を実行している1台以上のコンピューターまたは仮想マシン (Vm) にネットワークコントローラーを展開する方法について説明します。
manager: dougkim
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 2448d381-55aa-4c14-997a-202c537c6727
ms.author: pashort
author: shortpatti
ms.date: 08/23/2018
ms.openlocfilehash: 294466ef70a9ffc230953b48bb292938be519eac
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406115"
---
# <a name="deploy-network-controller-using-windows-powershell"></a>Windows PowerShell を使用してネットワーク コントローラーを展開する

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、windows PowerShell を使用して、Windows Server 2016 を実行している1つ以上の仮想マシン (Vm) にネットワークコントローラーを展開する方法について説明します。

>[!IMPORTANT]
>ネットワークコントローラーのサーバーの役割を物理ホストに展開しないでください。 ネットワーク コント ローラーを展開するには、ホストにインストールされている HYPER-V 仮想マシン\(VM\)でネットワーク コントローラー サーバーの役割をインストールする必要があります。 次の 3 つの異なる HYPER\-V ホスト上の VM にでネットワーク コントローラーをインストールした後、Windows PowerShell コマンド **New-NetworkControllerServer** を使用してホストをネットワーク コント ローラーに追加して、ソフトウェア定義ネットワーク\(SDN\)のHYPER\-Vホストを有効にする必要があります。 これにより、SDN ソフトウェア ロード バランサーが機能するようになります。 詳細については、[New-NetworkControllerServer](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollerserver)します。

このトピックは次のセクションで構成されます。

- [ネットワークコントローラーのサーバーの役割をインストールする](#install-the-network-controller-server-role)

- [ネットワークコントローラークラスターを構成する](#configure-the-network-controller-cluster)

- [ネットワークコントローラーアプリケーションの構成](#configure-the-network-controller-application)

- [ネットワークコントローラーの展開の検証](#network-controller-deployment-validation)

- [ネットワークコントローラー用のその他の Windows PowerShell コマンド](#additional-windows-powershell-commands-for-network-controller)

- [ネットワークコントローラーの構成スクリプトの例](#sample-network-controller-configuration-script)

- [非 Kerberos 展開の配置後の手順](#post-deployment-steps-for-non-kerberos-deployments)

## <a name="install-the-network-controller-server-role"></a>ネットワークコントローラーのサーバーの役割をインストールする

次の手順を使用して、仮想マシンにネットワークコントローラーサーバーの役割をインストール \(VM @ no__t-1

>[!IMPORTANT]
>ネットワークコントローラーのサーバーの役割を物理ホストに展開しないでください。 ネットワーク コント ローラーを展開するには、ホストにインストールされている HYPER-V 仮想マシン\(VM\)でネットワーク コントローラー サーバーの役割をインストールする必要があります。 3つの異なるハイパー @ no__t ホスト上にある Vm にネットワークコントローラーをインストールした後、ソフトウェアで定義されたネットワーク \(SDN @ no__t をネットワークコントローラーに追加することにより、そのホストで Hyper-v ホストを有効にする必要があります。 これにより、SDN ソフトウェア ロード バランサーが機能するようになります。

メンバーシップ **管理者**, 、同等の権限をこの手順を実行するために必要な最低限のですか。  

>[!NOTE]
>Windows PowerShell の代わりにサーバーマネージャーを使用してネットワークコントローラーをインストールする場合は、「[を使用したネットワークコントローラーサーバーの役割のインストール](https://technet.microsoft.com/library/mt403348.aspx)」を参照してくださいサーバーマネージャー

Windows PowerShell を使用してネットワークコントローラーをインストールするには、Windows PowerShell プロンプトで次のコマンドを入力し、enter キーを押します。

`Install-WindowsFeature -Name NetworkController -IncludeManagementTools`

ネットワークコントローラーをインストールするには、コンピューターを再起動する必要があります。 これを行うには、次のコマンドを入力して、enter キーを押します。

`Restart-Computer`

## <a name="configure-the-network-controller-cluster"></a>ネットワークコントローラークラスターを構成する

ネットワークコントローラークラスターは、ネットワークコントローラーアプリケーションに高可用性とスケーラビリティを提供します。このアプリケーションは、クラスターの作成後に構成でき、クラスター上でホストされます。

>[!NOTE]
>次のセクションの手順は、ネットワークコントローラーをインストールした VM で直接実行できます。また、Windows Server 2016 のリモートサーバー管理ツールを使用して、を実行しているリモートコンピューターから手順を実行することもできます。Windows Server 2016 または Windows 10。 また、この手順を実行するには、 **Administrators**のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。 ネットワークコントローラーをインストールしたコンピューターまたは VM がドメインに参加している場合は、ユーザーアカウントが**Domain Users**のメンバーである必要があります。

ノードオブジェクトを作成し、クラスターを構成することによって、ネットワークコントローラークラスターを作成できます。

### <a name="create-a-node-object"></a>Node オブジェクトを作成する

ネットワークコントローラークラスターのメンバーである VM ごとにノードオブジェクトを作成する必要があります。

Node オブジェクトを作成するには、Windows PowerShell コマンドプロンプトで次のコマンドを入力し、enter キーを押します。 デプロイに適した各パラメーターの値を追加していることを確認します。  

```
New-NetworkControllerNodeObject -Name <string> -Server <String> -FaultDomain <string>-RestInterface <string> [-NodeCertificate <X509Certificate2>]
```

次の表では、 **NetworkControllerNodeObject**コマンドの各パラメーターについて説明します。

|パラメーター|説明|
|-------------|---------------|
|名前|**Name**パラメーターは、クラスターに追加するサーバーのフレンドリ名を指定します。|
|Server|**Server**パラメーターは、クラスターに追加するサーバーのホスト名、完全修飾ドメイン名 (FQDN)、または IP アドレスを指定します。 ドメインに参加しているコンピューターの場合は、FQDN が必要です。|
|FaultDomain|**Faultdomain**パラメーターは、クラスターに追加するサーバーの障害ドメインを指定します。 このパラメーターは、クラスターに追加するサーバーと同時にエラーが発生する可能性のあるサーバーを定義します。 このエラーは、電源やネットワークのソースなどの物理的な依存関係が共有されていることが原因である可能性があります。 フォールトドメインは、通常、これらの共有依存関係に関連する階層を表します。これにより、障害ドメインツリーの上位のポイントから、より多くのサーバーに障害が発生する可能性が高くなります。 実行時に、ネットワークコントローラーはクラスター内の障害ドメインを考慮し、ネットワークコントローラーサービスを分散して、別々の障害ドメインに配置しようとします。 このプロセスにより、1つの障害ドメインで障害が発生した場合に、そのサービスとその状態の可用性が損なわれないようにすることができます。 障害ドメインは、階層形式で指定します。 以下に例を示します。"Fd:/DC1/ラック 1/datac"。 DC1 はデータセンター名、ラック1はラック名、"ホスト名" はノードが配置されているホストの名前です。|
|RestInterface|**RestInterface**パラメーターは、指定された状態の転送 (REST) 通信が終了するノード上のインターフェイスの名前を指定します。 このネットワークコントローラーインターフェイスは、ネットワークの管理レイヤーから Northbound API 要求を受信します。|
|NodeCertificate|**NodeCertificate**パラメーターは、コンピューターの認証にネットワークコントローラーが使用する証明書を指定します。 証明書ベースの認証を使用してクラスター内の通信を行う場合は、証明書が必要です。証明書は、ネットワークコントローラーサービス間のトラフィックの暗号化にも使用されます。 証明書のサブジェクト名は、ノードの DNS 名と同じである必要があります。|

### <a name="configure-the-cluster"></a>クラスターを構成する

クラスターを構成するには、Windows PowerShell コマンドプロンプトで次のコマンドを入力し、enter キーを押します。 デプロイに適した各パラメーターの値を追加していることを確認します。

```
Install-NetworkControllerCluster -Node <NetworkControllerNode[]> -ClusterAuthentication <ClusterAuthentication> [-ManagementSecurityGroup <string>][-DiagnosticLogLocation <string>][-LogLocationCredential <PSCredential>] [-CredentialEncryptionCertificate <X509Certificate2>][-Credential <PSCredential>][-CertificateThumbprint <String>] [-UseSSL][-ComputerName <string>][-LogSizeLimitInMBs<UInt32>] [-LogTimeLimitInDays<UInt32>]
```

次の表では、 **NetworkControllerCluster**コマンドの各パラメーターについて説明します。
  
|パラメーター|説明|
|-------------|---------------|
|ClusterAuthentication|**Clusterauthentication**パラメーターは、ノード間の通信をセキュリティで保護するために使用される認証の種類を指定します。また、ネットワークコントローラーサービス間のトラフィックの暗号化にも使用されます。 サポートされている値は、 **Kerberos**、 **X509** 、および**None**です。 Kerberos 認証はドメインアカウントを使用し、ネットワークコントローラーノードがドメインに参加している場合にのみ使用できます。 X509 ベースの認証を指定する場合は、NetworkControllerNode オブジェクトに証明書を提供する必要があります。 また、このコマンドを実行する前に、証明書を手動でプロビジョニングする必要があります。|
|ManagementSecurityGroup|**ManagementSecurityGroup**パラメーターは、リモートコンピューターからの管理コマンドレットの実行を許可されているユーザーを含むセキュリティグループの名前を指定します。 これは、ClusterAuthentication が Kerberos の場合にのみ適用されます。 ローカルコンピューターのセキュリティグループではなく、ドメインセキュリティグループを指定する必要があります。|
|ノード|**Node**パラメーターは、 **NetworkControllerNodeObject**コマンドを使用して作成したネットワークコントローラーノードの一覧を指定します。|
|DiagnosticLogLocation|**DiagnosticLogLocation**パラメーターは、診断ログが定期的にアップロードされる共有の場所を指定します。 このパラメーターに値を指定しない場合、ログは各ノードにローカルに格納されます。 ログは%systemdrive%\Windows\tracing\SDNDiagnostics. フォルダーにローカルに格納されます。 クラスターログは%systemdrive%\ProgramData\Microsoft\Service Fabric\log\Traces. フォルダーにローカルに格納されます。|
|LogLocationCredential|**LogLocationCredential**パラメーターは、ログが保存されている共有の場所にアクセスするために必要な資格情報を指定します。|
|CredentialEncryptionCertificate|**Credentialencryptioncertificate**パラメーターは、ネットワークコントローラーのバイナリにアクセスするために使用される資格情報を暗号化するためにネットワークコントローラーが使用する証明書と、指定されている場合は**LogLocationCredential**を指定します。 このコマンドを実行する前に、すべてのネットワークコントローラーノードで証明書をプロビジョニングする必要があります。また、同じ証明書をすべてのクラスターノードに登録する必要があります。 運用環境では、このパラメーターを使用してネットワークコントローラーのバイナリとログを保護することをお勧めします。 このパラメーターを指定しない場合、資格情報はクリアテキストで格納され、承認されていないユーザーによって誤用される可能性があります。|
|資格情報|このパラメーターは、リモートコンピューターからこのコマンドを実行する場合にのみ必要です。 **Credential**パラメーターは、対象のコンピューターでこのコマンドを実行する権限を持つユーザーアカウントを指定します。|
|CertificateThumbprint|このパラメーターは、リモートコンピューターからこのコマンドを実行する場合にのみ必要です。 **CertificateThumbprint**パラメーターは、対象のコンピューターでこのコマンドを実行するアクセス許可を持つユーザーアカウントのデジタル公開キー証明書 (X509) を指定します。|
|UseSSL|このパラメーターは、リモートコンピューターからこのコマンドを実行する場合にのみ必要です。 **UseSSL**パラメーターは、リモートコンピューターへの接続を確立するために使用される SECURE SOCKETS LAYER (SSL) プロトコルを指定します。 既定では、SSL は使用されません。|
|ComputerName|**ComputerName**パラメーターは、このコマンドを実行するネットワークコントローラーノードを指定します。 このパラメーターに値を指定しない場合は、既定でローカルコンピューターが使用されます。|
|LogSizeLimitInMBs|このパラメーターは、ネットワークコントローラーが格納できる最大ログサイズを MB 単位で指定します。 ログは、循環形式で格納されます。 DiagnosticLogLocation が指定されている場合、このパラメーターの既定値は 40 GB です。 DiagnosticLogLocation が指定されていない場合、ログはネットワークコントローラーのノードに格納され、このパラメーターの既定値は 15 GB になります。|
|LogTimeLimitInDays|このパラメーターは、ログを格納する期間の制限を日数で指定します。 ログは、循環形式で格納されます。 このパラメーターの既定値は3日間です。|

## <a name="configure-the-network-controller-application"></a>ネットワークコントローラーアプリケーションの構成
ネットワークコントローラーアプリケーションを構成するには、Windows PowerShell コマンドプロンプトで次のコマンドを入力し、enter キーを押します。 デプロイに適した各パラメーターの値を追加していることを確認します。

```
Install-NetworkController -Node <NetworkControllerNode[]> -ClientAuthentication <ClientAuthentication>  [-ClientCertificateThumbprint <string[]>]  [-ClientSecurityGroup <string>] -ServerCertificate <X509Certificate2> [-RESTIPAddress <String>] [-RESTName <String>] [-Credential <PSCredential>][-CertificateThumbprint <String> ] [-UseSSL]
```

次の表では、 **NetworkController**コマンドの各パラメーターについて説明します。

|パラメーター|説明|
|-------------|---------------|
|ClientAuthentication|**Clientauthentication**パラメーターは、REST とネットワークコントローラー間の通信をセキュリティで保護するために使用される認証の種類を指定します。 サポートされている値は、 **Kerberos**、 **X509** 、および**None**です。 Kerberos 認証はドメインアカウントを使用し、ネットワークコントローラーノードがドメインに参加している場合にのみ使用できます。 X509 ベースの認証を指定する場合は、NetworkControllerNode オブジェクトに証明書を提供する必要があります。 また、このコマンドを実行する前に、証明書を手動でプロビジョニングする必要があります。|
|ノード|**Node**パラメーターは、 **NetworkControllerNodeObject**コマンドを使用して作成したネットワークコントローラーノードの一覧を指定します。|
|ClientCertificateThumbprint|このパラメーターは、ネットワークコントローラークライアントに証明書ベースの認証を使用している場合にのみ必要です。 **Clientcertificatethumbprint**パラメーターは、Northbound 層のクライアントに登録されている証明書の拇印を指定します。|
|ServerCertificate|**Servercertificate**パラメーターは、ネットワークコントローラーがクライアントに対してその id を証明するために使用する証明書を指定します。 サーバー証明書には、拡張キー使用法拡張でのサーバー認証の目的が含まれている必要があります。また、クライアントによって信頼されている CA によってネットワークコントローラーに発行する必要があります。|
|RESTIPAddress|ネットワークコントローラーの単一ノード展開で**RESTIPAddress**の値を指定する必要はありません。 複数ノードデプロイの場合、 **RESTIPAddress**パラメーターは、REST エンドポイントの IP アドレスを CIDR 表記で指定します。 たとえば、192.168.1.10/24 のようになります。 **Servercertificate**のサブジェクト名の値は、 **RESTIPAddress**パラメーターの値に解決される必要があります。 すべてのノードが同じサブネット上にある場合は、すべてのマルチノードネットワークコントローラーの展開に対してこのパラメーターを指定する必要があります。 ノードが異なるサブネット上にある場合は、 **RESTIPAddress**を使用する代わりに、**た restname**パラメーターを使用する必要があります。|
|た restname|ネットワークコントローラーの単一ノード展開で**た restname**の値を指定する必要はありません。 **た restname**の値を指定する必要があるのは、複数ノードの展開が異なるサブネット上にあるノードを持っている場合のみです。 複数ノード展開の場合、**た restname**パラメーターはネットワークコントローラークラスターの FQDN を指定します。|
|ClientSecurityGroup|**ClientSecurityGroup**パラメーターは、メンバーがネットワークコントローラークライアントである Active Directory セキュリティグループの名前を指定します。 このパラメーターは、 **clientauthentication**に Kerberos 認証を使用する場合にのみ必要です。 セキュリティグループには、REST Api へのアクセス元のアカウントが含まれている必要があります。このコマンドを実行する前に、セキュリティグループを作成してメンバーを追加する必要があります。|
|資格情報|このパラメーターは、リモートコンピューターからこのコマンドを実行する場合にのみ必要です。 **Credential**パラメーターは、対象のコンピューターでこのコマンドを実行する権限を持つユーザーアカウントを指定します。|
|CertificateThumbprint|このパラメーターは、リモートコンピューターからこのコマンドを実行する場合にのみ必要です。 **CertificateThumbprint**パラメーターは、対象のコンピューターでこのコマンドを実行するアクセス許可を持つユーザーアカウントのデジタル公開キー証明書 (X509) を指定します。|
|UseSSL|このパラメーターは、リモートコンピューターからこのコマンドを実行する場合にのみ必要です。 **UseSSL**パラメーターは、リモートコンピューターへの接続を確立するために使用される SECURE SOCKETS LAYER (SSL) プロトコルを指定します。 既定では、SSL は使用されません。|

ネットワークコントローラーアプリケーションの構成が完了すると、ネットワークコントローラーの展開が完了します。

## <a name="network-controller-deployment-validation"></a>ネットワークコントローラーの展開の検証

ネットワークコントローラーの展開を検証するには、資格情報をネットワークコントローラーに追加してから、資格情報を取得します。

ClientAuthentication メカニズムとして Kerberos を使用している場合、この手順を実行するには、作成した**ClientSecurityGroup**のメンバーシップが最低限必要です。

**作業**

1.  クライアントコンピューターで、ClientAuthentication メカニズムとして Kerberos を使用している場合は、 **ClientSecurityGroup**のメンバーであるユーザーアカウントでログオンします。

2. Windows PowerShell を開き、次のコマンドを入力して、ネットワークコントローラーに資格情報を追加してから、ENTER キーを押します。 デプロイに適した各パラメーターの値を追加していることを確認します。

    ```
    $cred=New-Object Microsoft.Windows.Networkcontroller.credentialproperties
    $cred.type="usernamepassword"
    $cred.username="admin"
    $cred.value="abcd"

    New-NetworkControllerCredential -ConnectionUri https://networkcontroller -Properties $cred -ResourceId cred1
    ```

3. ネットワークコントローラーに追加した資格情報を取得するには、次のコマンドを入力して、enter キーを押します。 デプロイに適した各パラメーターの値を追加していることを確認します。

    ```
    Get-NetworkControllerCredential -ConnectionUri https://networkcontroller -ResourceId cred1  
    ```

4. コマンドの出力を確認します。これは次の出力例のようになります。

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
    > **NetworkControllerCredential**コマンドを実行すると、ドット演算子を使用して資格情報のプロパティを一覧表示することで、コマンドの出力を変数に割り当てることができます。 たとえば、$cred のようにします。属性.

## <a name="additional-windows-powershell-commands-for-network-controller"></a>ネットワークコントローラー用のその他の Windows PowerShell コマンド

ネットワークコントローラーを展開した後、Windows PowerShell コマンドを使用して、展開を管理および変更できます。 デプロイに対して行うことができる変更の一部を次に示します。

- ネットワークコントローラーのノード、クラスター、およびアプリケーションの設定を変更する

- ネットワークコントローラーのクラスターとアプリケーションを削除する

- ノードの追加、削除、有効化、無効化など、ネットワークコントローラーのクラスターノードを管理します。

次の表は、これらのタスクを実行するために使用できる Windows PowerShell コマンドの構文を示しています。

|タスク|コマンド|構文|
|--------|-------|----------|
|ネットワークコントローラーのクラスター設定を変更する|NetworkControllerCluster|`Set-NetworkControllerCluster [-ManagementSecurityGroup <string>][-Credential <PSCredential>] [-computerName <string>][-CertificateThumbprint <String> ] [-UseSSL]`
|ネットワークコントローラーのアプリケーション設定を変更する|NetworkController|`Set-NetworkController [-ClientAuthentication <ClientAuthentication>] [-Credential <PSCredential>] [-ClientCertificateThumbprint <string[]>] [-ClientSecurityGroup <string>] [-ServerCertificate <X509Certificate2>] [-RestIPAddress <String>] [-ComputerName <String>][-CertificateThumbprint <String> ] [-UseSSL]`
|ネットワークコントローラーのノード設定を変更する|NetworkControllerNode|`Set-NetworkControllerNode -Name <string> > [-RestInterface <string>] [-NodeCertificate <X509Certificate2>] [-Credential <PSCredential>] [-ComputerName <string>][-CertificateThumbprint <String> ] [-UseSSL]`
|ネットワークコントローラーの診断設定を変更する|NetworkControllerDiagnostic|`Set-NetworkControllerDiagnostic [-LogScope <string>] [-DiagnosticLogLocation <string>] [-LogLocationCredential <PSCredential>] [-UseLocalLogLocation] >] [-LogLevel <loglevel>][-LogSizeLimitInMBs <uint32>] [-LogTimeLimitInDays <uint32>] [-Credential <PSCredential>] [-ComputerName <string>][-CertificateThumbprint <String> ] [-UseSSL]`
|ネットワークコントローラーアプリケーションを削除する|NetworkController|`Uninstall-NetworkController [-Credential <PSCredential>][-ComputerName <string>] [-CertificateThumbprint <String> ] [-UseSSL]`
|ネットワークコントローラーのクラスターを削除する|NetworkControllerCluster|`Uninstall-NetworkControllerCluster [-Credential <PSCredential>][-ComputerName <string>][-CertificateThumbprint <String> ] [-UseSSL]`
|ネットワークコントローラークラスターにノードを追加する|NetworkControllerNode|`Add-NetworkControllerNode -FaultDomain <String> -Name <String> -RestInterface <String> -Server <String> [-CertificateThumbprint <String> ] [-ComputerName <String> ] [-Credential <PSCredential> ] [-Force] [-NodeCertificate <X509Certificate2> ] [-PassThru] [-UseSsl]`
|ネットワークコントローラーのクラスターノードを無効にする|NetworkControllerNode|`Disable-NetworkControllerNode -Name <String> [-CertificateThumbprint <String> ] [-ComputerName <String> ] [-Credential <PSCredential> ] [-PassThru] [-UseSsl]`
|ネットワークコントローラーのクラスターノードを有効にする|NetworkControllerNode|`Enable-NetworkControllerNode -Name <String> [-CertificateThumbprint <String> ] [-ComputerName <String> ] [-Credential <PSCredential> ] [-PassThru] [-UseSsl]`
|ネットワークコントローラーのノードをクラスターから削除する|NetworkControllerNode|`Remove-NetworkControllerNode [-CertificateThumbprint <String> ] [-ComputerName <String> ] [-Credential <PSCredential> ] [-Force] [-Name <String> ] [-PassThru] [-UseSsl]`

>[!NOTE]
>ネットワークコントローラー用の Windows PowerShell コマンドは、TechNet ライブラリの「[ネットワークコントローラーコマンドレット](https://technet.microsoft.com/library/mt576401.aspx)」にあります。

## <a name="sample-network-controller-configuration-script"></a>ネットワークコントローラーの構成スクリプトの例

次のサンプル構成スクリプトは、マルチノードネットワークコントローラークラスターを作成し、ネットワークコントローラーアプリケーションをインストールする方法を示しています。 さらに、$cert 変数は、サブジェクト名文字列 "networkController.contoso.com" に一致する証明書をローカルコンピューターの証明書ストアから選択します。

```
$a = New-NetworkControllerNodeObject -Name Node1 -Server NCNode1.contoso.com -FaultDomain fd:/rack1/host1 -RestInterface Internal
$b = New-NetworkControllerNodeObject -Name Node2 -Server NCNode2.contoso.com -FaultDomain fd:/rack1/host2 -RestInterface Internal
$c = New-NetworkControllerNodeObject -Name Node3 -Server NCNode3.contoso.com -FaultDomain fd:/rack1/host3 -RestInterface Internal

$cert= get-item Cert:\LocalMachine\My | get-ChildItem | where {$_.Subject -imatch "networkController.contoso.com" }

Install-NetworkControllerCluster -Node @($a,$b,$c)  -ClusterAuthentication Kerberos -DiagnosticLogLocation \\share\Diagnostics - ManagementSecurityGroup Contoso\NCManagementAdmins -CredentialEncryptionCertificate $cert  
Install-NetworkController -Node @($a,$b,$c) -ClientAuthentication Kerberos -ClientSecurityGroup Contoso\NCRESTClients -ServerCertificate $cert -RestIpAddress 10.0.0.1/24
```

## <a name="post-deployment-steps-for-non-kerberos-deployments"></a>非 Kerberos 展開の配置後の手順

ネットワークコントローラーの展開で Kerberos を使用していない場合は、証明書を展開する必要があります。

詳細については、「[ネットワークコントローラーの展開後の手順](../technologies/network-controller/post-deploy-steps-nc.md)」を参照してください。


