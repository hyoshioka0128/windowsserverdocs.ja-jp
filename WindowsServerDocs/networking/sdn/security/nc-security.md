---
title: ネットワーク コントローラーのセキュリティ
description: このトピックでは、ネットワークコントローラーとその他のソフトウェアおよびデバイス間のすべての通信のセキュリティを構成する方法について説明します。
manager: grcusanz
ms.topic: article
ms.assetid: bc625de9-ee31-40a4-9ad2-7448bfbfb6e6
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/30/2018
ms.openlocfilehash: 42bed85fed8da210d3a7583caf0170064fd2aff5
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87962076"
---
# <a name="secure-the-network-controller"></a>ネットワーク コントローラーをセキュリティで保護する

このトピックでは、[ネットワークコントローラー](../technologies/network-controller/network-controller.md)とその他のソフトウェアおよびデバイス間のすべての通信のセキュリティを構成する方法について説明します。

セキュリティで保護できる通信パスには、管理プレーンでの Northbound 通信、クラスター内のネットワークコントローラー仮想マシン vm 間のクラスター通信、 \( \) およびデータプレーンでの通信の Southbound が含まれます。

1. **Northbound 通信**。 ネットワークコントローラーは、管理プレーンと、 \- Windows PowerShell や System Center Virtual Machine Manager SCVMM などの SDN 対応管理ソフトウェアとの通信を \( \) 行います。 これらの管理ツールを使用すると、ネットワークポリシーを定義し、ネットワークの目標状態を作成することができます。これにより、実際のネットワーク構成を比較して、実際の構成を目標の状態でパリティにすることができます。

2. **ネットワークコントローラーのクラスター通信**。 3つ以上の Vm をネットワークコントローラークラスターノードとして構成すると、これらのノードは相互に通信します。 この通信は、ノード間でのデータの同期とレプリケーション、またはネットワークコントローラーサービス間の特定の通信に関連している場合があります。

3.  **Southbound 通信**。 ネットワークコントローラーは、データプレーンと SDN インフラストラクチャ、およびソフトウェアロードバランサー、ゲートウェイ、ホストコンピューターなどの他のデバイスと通信します。 ネットワークコントローラーを使用して、これらの southbound デバイスを構成および管理し、ネットワーク用に構成した目標の状態を維持することができます。


## <a name="northbound-communication"></a>Northbound 通信

ネットワークコントローラーは、Northbound 通信の認証、承認、および暗号化をサポートしています。 以下のセクションでは、これらのセキュリティ設定を構成する方法について説明します。

### <a name="authentication"></a>認証

ネットワークコントローラーの Northbound 通信の認証を構成すると、ネットワークコントローラーのクラスターノードと管理クライアントは、通信しているデバイスの id を確認できます。

ネットワークコントローラーは、管理クライアントとネットワークコントローラーのノード間で、次の3つの認証モードをサポートしています。

>[!Note]
>System Center Virtual Machine Manager を使用してネットワークコントローラーを展開する場合は、 **Kerberos**モードのみがサポートされます。

1. **Kerberos**。 管理クライアントとすべてのネットワークコントローラークラスターノードを Active Directory ドメインに参加させる場合は、Kerberos 認証を使用します。 Active Directory ドメインには、認証に使用するドメインアカウントが必要です。

2. **X509**。 \-Active Directory ドメインに参加していない管理クライアントに対しては、証明書ベースの認証に X509 を使用します。 すべてのネットワークコントローラークラスターノードと管理クライアントに証明書を登録する必要があります。 また、すべてのノードと管理クライアントは、他のすべての証明書を信頼する必要があります。

3. **なし**。 テスト環境でテスト目的には None を使用するため、運用環境では使用しないことをお勧めします。 このモードを選択した場合、ノードと管理クライアントの間で認証は実行されません。

Northbound 通信の認証モードを構成するには、Windows PowerShell コマンド**[NetworkController](https://docs.microsoft.com/powershell/module/networkcontroller/install-networkcontroller)** と_clientauthentication_パラメーターを使用します。


### <a name="authorization"></a>承認

ネットワークコントローラーの Northbound 通信の承認を構成すると、ネットワークコントローラーのクラスターノードと管理クライアントは、通信しているデバイスが信頼されており、通信に参加するためのアクセス許可を持っていることを確認できます。

ネットワークコントローラーでサポートされている各認証モードには、次の承認方法を使用します。

1.  **Kerberos**。 Kerberos 認証方法を使用する場合は、Active Directory でセキュリティグループを作成してから、承認されたユーザーとコンピューターをグループに追加することによって、ネットワークコントローラーとの通信を許可するユーザーとコンピューターを定義します。 **[NetworkController](https://docs.microsoft.com/powershell/module/networkcontroller/install-networkcontroller)** Windows PowerShell コマンドの_ClientSecurityGroup_パラメーターを使用して、認証にセキュリティグループを使用するようにネットワークコントローラーを構成できます。 ネットワークコントローラーをインストールした後、 **[NetworkController](https://docs.microsoft.com/powershell/module/networkcontroller/Set-NetworkController)** コマンドと _-ClientSecurityGroup_パラメーターを使用して、セキュリティグループを変更できます。 SCVMM を使用する場合は、デプロイ時にパラメーターとしてセキュリティグループを指定する必要があります。

2.  **X509**。 X509 認証方法を使用している場合、ネットワークコントローラーは、証明書の拇印がネットワークコントローラーに認識されている管理クライアントからの要求のみを受け入れます。 これらの拇印は、 **[NetworkController](https://docs.microsoft.com/powershell/module/networkcontroller/install-networkcontroller)** Windows PowerShell コマンドの_clientcertificatethumbprint_パラメーターを使用して構成できます。 **[NetworkController](https://docs.microsoft.com/powershell/module/networkcontroller/Set-NetworkController)** コマンドを使用して、いつでも他のクライアントの拇印を追加できます。

3.  **なし**。 このモードを選択した場合、ノードと管理クライアントの間で認証は実行されません。 テスト環境でテスト目的には None を使用するため、運用環境では使用しないことをお勧めします。


### <a name="encryption"></a>暗号化

Northbound 通信では Secure Sockets Layer \( SSL を使用し \) て、管理クライアントとネットワークコントローラーノードの間に暗号化されたチャネルを作成します。 Northbound 通信の SSL 暗号化には、次の要件があります。

- すべてのネットワークコントローラーノードには、拡張キー使用法 EKU 拡張でのサーバー認証とクライアント認証を含む、同一の証明書が必要です \( \) 。

- ネットワークコントローラーとの通信に管理クライアントが使用する URI は、証明書のサブジェクト名である必要があります。 証明書のサブジェクト名には、完全修飾ドメイン名 (FQDN) またはネットワークコントローラー REST エンドポイントの IP アドレスのいずれかが含まれている必要があります。

- ネットワークコントローラーノードが異なるサブネット上にある場合、証明書のサブジェクト名は、 **NetworkController** Windows PowerShell コマンドの_た restname_パラメーターに使用されている値と同じである必要があります。

- すべての管理クライアントは、SSL 証明書を信頼する必要があります。


### <a name="ssl-certificate-enrollment-and-configuration"></a>SSL 証明書の登録と構成

SSL 証明書は、ネットワークコントローラーのノードに手動で登録する必要があります。

証明書が登録されたら、 **NetworkController** Windows PowerShell コマンドの **-servercertificate**パラメーターで証明書を使用するようにネットワークコントローラーを構成できます。 ネットワークコントローラーを既にインストールしている場合は、 **NetworkController**コマンドを使用して、いつでも構成を更新できます。

>[!NOTE]
>SCVMM を使用している場合は、証明書をライブラリリソースとして追加する必要があります。 詳細については、「 [VMM ファブリックでの SDN ネットワークコントローラーのセットアップ](https://docs.microsoft.com/system-center/vmm/sdn-controller)」を参照してください。

## <a name="network-controller-cluster-communication"></a>ネットワークコントローラーのクラスター通信

ネットワークコントローラーは、ネットワークコントローラーノード間の通信の認証、承認、および暗号化をサポートしています。 通信は[Windows Communication Foundation](https://docs.microsoft.com/dotnet/framework/wcf/whats-wcf) \( WCF と TCP を経由し \) ます。

このモードは、 **NetworkControllerCluster** Windows PowerShell コマンドの**clusterauthentication**パラメーターを使用して構成できます。

詳細については、「 [NetworkControllerCluster](https://docs.microsoft.com/powershell/module/networkcontroller/install-networkcontrollercluster)」を参照してください。

### <a name="authentication"></a>認証

ネットワークコントローラークラスター通信の認証を構成すると、ネットワークコントローラークラスターノードは、通信している他のノードの id を確認できるようになります。

ネットワークコントローラーは、ネットワークコントローラーノード間で次の3つの認証モードをサポートしています。

>[!NOTE]
>SCVMM を使用してネットワークコントローラーを展開する場合、 **Kerberos**モードのみがサポートされます。

1. **Kerberos**。 認証に使用されるドメインアカウントを使用して、すべてのネットワークコントローラークラスターノードが Active Directory ドメインに参加している場合は、Kerberos 認証を使用できます。

2. **X509**。 X509 は証明書 \- ベースの認証です。 ネットワークコントローラーのクラスターノードが Active Directory ドメインに参加していない場合は、X509 認証を使用できます。 X509 を使用するには、すべてのネットワークコントローラークラスターノードに証明書を登録する必要があります。また、すべてのノードが証明書を信頼する必要があります。 また、各ノードに登録されている証明書のサブジェクト名は、ノードの DNS 名と同じである必要があります。

3. **なし**。 このモードを選択すると、ネットワークコントローラーノード間で認証は実行されません。 このモードはテスト目的でのみ提供されており、運用環境での使用は推奨されていません。

### <a name="authorization"></a>承認

ネットワークコントローラークラスター通信の承認を構成すると、ネットワークコントローラークラスターノードは、通信しているノードが信頼されていること、および通信に参加するためのアクセス許可を持っていることを確認できるようになります。

ネットワークコントローラーでサポートされている各認証モードについて、次の承認方法が使用されます。

1. **Kerberos**。 ネットワークコントローラーのノードは、他のネットワークコントローラーのコンピューターアカウントからの通信要求のみを受け入れます。 [NetworkControllerNodeObject](https://docs.microsoft.com/powershell/module/networkcontroller/new-networkcontrollernodeobject) Windows PowerShell コマンドの**Name**パラメーターを使用して、ネットワークコントローラーを展開するときにこれらのアカウントを構成できます。

2. **X509**。 ネットワークコントローラーのノードは、他のネットワークコントローラーのコンピューターアカウントからの通信要求のみを受け入れます。 [NetworkControllerNodeObject](https://docs.microsoft.com/powershell/module/networkcontroller/new-networkcontrollernodeobject) Windows PowerShell コマンドの**Name**パラメーターを使用して、ネットワークコントローラーを展開するときにこれらのアカウントを構成できます。

3. **なし**。 このモードを選択した場合、ネットワークコントローラーノード間で承認は実行されません。 このモードはテスト目的でのみ提供されており、運用環境での使用は推奨されていません。

### <a name="encryption"></a>暗号化

ネットワークコントローラーノード間の通信は、WCF トランスポートレベルの暗号化を使用して暗号化されます。 この形式の暗号化は、認証と承認の方法が Kerberos 証明書または X509 証明書のいずれかである場合に使用されます。 詳細については、次の各トピックを参照してください。

- [方法: Windows 資格情報でサービスをセキュリティで保護する](https://docs.microsoft.com/dotnet/framework/wcf/how-to-secure-a-service-with-windows-credentials)
- [方法: X.509 証明書を使用してサービスをセキュリティで保護](https://docs.microsoft.com/dotnet/framework/wcf/feature-details/how-to-secure-a-service-with-an-x-509-certificate)する。

## <a name="southbound-communication"></a>Southbound 通信

ネットワークコントローラーは、Southbound 通信用にさまざまな種類のデバイスと対話します。 これらの相互作用は異なるプロトコルを使用します。 このため、デバイスとの通信にネットワークコントローラーが使用するデバイスとプロトコルの種類に応じて、認証、承認、および暗号化に関するさまざまな要件があります。

次の表は、さまざまな southbound デバイスとのネットワークコントローラーの相互作用に関する情報を示しています。

| Southbound デバイス/サービス | Protocol              | 使用される認証    |
|---------------------------|-----------------------|------------------------|
| ソフトウェア ロード バランサー    | WCF (MUX)、TCP (ホスト) | 証明書           |
| ファイアウォール                  | OVSDB                 | 証明書           |
| Gateway                   | WinRM                 | Kerberos、証明書 |
| 仮想ネットワーク        | [すべての]、[WCF]            | 証明書           |
| ユーザー定義ルーティング      | OVSDB                 | 証明書           |

これらのプロトコルごとに、次のセクションで通信メカニズムについて説明します。

### <a name="authentication"></a>認証

Southbound 通信では、次のプロトコルと認証方法が使用されます。

1. **WCF/TCP//////////////** の これらのプロトコルでは、X509 証明書を使用して認証が実行されます。 ネットワークコントローラーとピアソフトウェア負荷分散 \( SLB \) マルチプレクサー \( MUX \) /host マシンは、相互認証のために証明書を相互に提示します。 各証明書は、リモートピアによって信頼されている必要があります。

    Southbound 認証の場合、Northbound クライアントとの通信を暗号化するように構成されているのと同じ SSL 証明書を使用できます。 また、SLB MUX とホストデバイスで証明書を構成する必要があります。 証明書のサブジェクト名は、デバイスの DNS 名と同じである必要があります。

2. **WinRM**。 このプロトコルでは、ドメインに参加しているコンピューターには Kerberos を使用し、ドメインに参加して \( \) いないコンピューターには証明書を使用して認証が実行され \( \) ます。

### <a name="authorization"></a>承認

Southbound 通信では、次のプロトコルと承認方法が使用されます。

1. **WCF/TCP**。 これらのプロトコルでは、承認はピアエンティティのサブジェクト名に基づいて行われます。 ネットワークコントローラーは、ピアデバイスの DNS 名を保存し、承認に使用します。 この DNS 名は、証明書内のデバイスのサブジェクト名と一致している必要があります。 同様に、ネットワークコントローラー証明書は、ピアデバイスに格納されているネットワークコントローラーの DNS 名と一致している必要があります。

2. **WinRM**。 Kerberos が使用されている場合は、Active Directory 内の事前定義されたグループまたはサーバーのローカル管理者グループに WinRM クライアントアカウントが存在している必要があります。 証明書が使用されている場合、クライアントは、サーバーがサブジェクト名/発行者を使用して承認した証明書をサーバーに提示し、サーバーは、マップされたユーザーアカウントを使用して認証を実行します。

3.  このよう**にして**います。 このプロトコルには認証は提供されません。

### <a name="encryption"></a>暗号化

Southbound 通信では、次の暗号化方法がプロトコルに使用されます。

1. **WCF/TCP//////////////** の これらのプロトコルでは、クライアントまたはサーバーに登録されている証明書を使用して暗号化が実行されます。

2. **WinRM**。 WinRM のトラフィックは、Kerberos セキュリティサポートプロバイダーの SSP を使用して既定で暗号化され \( \) ます。 WinRM サーバーでは、SSL の形式で追加の暗号化を構成できます。
