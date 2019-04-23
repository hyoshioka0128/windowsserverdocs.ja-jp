---
title: ネットワーク コントローラーのセキュリティ
description: このトピックを使用すると、ネットワーク コント ローラーとその他のソフトウェアおよびデバイス間のすべての通信のセキュリティを構成するのに方法について説明します。
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: bc625de9-ee31-40a4-9ad2-7448bfbfb6e6
ms.author: pashort
author: shortpatti
ms.date: 08/30/2018
ms.openlocfilehash: fccd6ee1ba734d72629264bd5b3bb7d93ddcdb70
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59884763"
---
# <a name="secure-the-network-controller"></a>ネットワーク コントローラーをセキュリティで保護する

このトピックでは、すべての通信のセキュリティを構成する方法がについて説明します。[ネットワーク コント ローラー](../technologies/network-controller/network-controller.md)とその他のソフトウェアおよびデバイス。 

セキュリティで保護することがある通信パスは、管理プレーンでネットワーク コント ローラー仮想マシン間のクラスター通信の Northbound 通信\(Vm\)クラスター、およびデータの Southbound 通信で平面。

1. **Northbound 通信**します。 ネットワーク コント ローラーが SDN での管理プレーンの通信\-対応の管理ソフトウェアなど、Windows PowerShell と System Center Virtual Machine Manager \(SCVMM\)します。 これらの管理ツールは、ネットワーク ポリシーを定義して、目標とする状態と同等に実際の構成を実際のネットワーク構成を比較する対象となるネットワークの目的の状態を作成する機能を提供します。

2. **ネットワーク コント ローラーのクラスター通信**します。 ネットワーク コント ローラーがクラスター ノードとして 3 つ以上の Vm を構成するときにこれらのノードは、互いと通信します。 この通信は、ノード、またはネットワーク コント ローラーのサービス間の特定の通信と、同期とデータのレプリケーションに関連する可能性があります。

3.  **Southbound 通信**します。 ネットワーク コント ローラーは、SDN インフラストラクチャおよびソフトウェア ロード バランサー、ゲートウェイ、およびホスト コンピューターのような他のデバイスとデータ プレーンで通信します。 ネットワーク コント ローラーを使用して、構成して、ネットワーク用に構成した目的の状態を維持するように、southbound デバイスを管理することができます。


## <a name="northbound-communication"></a>Northbound 通信

ネットワーク コント ローラーは、Northbound 通信の認証、承認、および暗号化をサポートします。 次のセクションでは、これらのセキュリティ設定を構成する方法についてを説明します。

### <a name="authentication"></a>認証

ネットワーク コント ローラーの Northbound 通信の認証を構成するときに、クラスター ノードのネットワーク コント ローラーと通信しているデバイスの id を確認する管理クライアントを許可します。

ネットワーク コント ローラーには、次の 3 つの管理クライアントとネットワーク コント ローラーのノード間の認証モードがサポートしています。

>[!Note]
>System Center Virtual Machine Manager でのネットワーク コント ローラーをのみに展開するかどうか**Kerberos**モードがサポートされています。

1. **Kerberos** です。 管理クライアントとネットワーク コント ローラーのすべてのクラスター ノードの両方を Active Directory ドメインに参加させる場合は、Kerberos 認証を使用します。 Active Directory ドメインには、認証に使用されるドメイン アカウントが必要です。

2. **X509**します。 証明書の X509 を使用して\-ベースの Active Directory ドメインに参加していない管理クライアントを認証します。 すべてのクラスター ノードのネットワーク コント ローラーと管理のクライアント証明書を登録する必要があります。 また、すべてのノードと管理クライアントは、互いの証明書を信頼する必要があります。

3. **None**。 使用 None テストをテスト環境で目的し、そのため、使用しないで、実稼働環境での使用 このモードを選択すると、ノードと管理クライアントの間で実行される認証がありません。

Northbound 通信の認証モードを構成するには、Windows PowerShell コマンドを使用して**[インストール NetworkController](https://technet.microsoft.com/itpro/powershell/windows/network-controller/install-networkcontroller)** で、 _ClientAuthentication_パラメーター。 


### <a name="authorization"></a>Authorization

ネットワーク コント ローラーがクラスター ノードと通信しているデバイスが信頼されていることを確認に参加するアクセス許可を持つ管理クライアントを許可するネットワーク コント ローラーの Northbound 通信用の承認を構成するときに、通信します。

各ネットワーク コント ローラーでサポートされる認証モードの次の承認方法を使用します。

1.  **Kerberos** です。 Kerberos 認証メソッドを使用しているときに、ユーザーとコンピューターを Active Directory でセキュリティ グループを作成して、承認されたユーザーとコンピューターをグループに追加し、ネットワーク コント ローラーと通信する権限を定義します。 使用して、承認、セキュリティ グループを使用するネットワーク コント ローラーを構成することができます、 _ClientSecurityGroup_のパラメーター、 **[インストール NetworkController](https://technet.microsoft.com/itpro/powershell/windows/network-controller/install-networkcontroller)** Windows PowerShell コマンド。 ネットワーク コント ローラーをインストールした後を使用してセキュリティ グループを変更することができます、 **[セット NetworkController](https://technet.microsoft.com/itpro/powershell/windows/network-controller/set-networkcontroller)** コマンド、パラメーターと _- ClientSecurityGroup_. SCVMM を使用する場合は、デプロイ中にパラメーターとしてセキュリティ グループを指定する必要があります。

2.  **X509**します。 X509 を使用しているときに認証方法、ネットワーク コント ローラーのみを受け入れますが証明書の拇印はネットワーク コント ローラーに既知の管理クライアントからの要求。 これらの拇印を使用して構成することができます、 _ClientCertificateThumbprint_のパラメーター、 **[インストール NetworkController](https://technet.microsoft.com/itpro/powershell/windows/network-controller/install-networkcontroller)**  Windows PowerShell コマンド。 使用して、いつでも他のクライアントのサムプリントを追加することができます、 **[セット NetworkController](https://technet.microsoft.com/itpro/powershell/windows/network-controller/set-networkcontroller)** コマンド。

3.  **None**。 このモードを選択すると、ノードと管理クライアントの間で実行される認証がありません。 使用 None テストをテスト環境で目的し、そのため、使用しないで、実稼働環境での使用 


### <a name="encryption"></a>暗号化

Northbound 通信は、Secure Sockets Layer を使用して\(SSL\)管理クライアントとネットワーク コント ローラーのノード間で暗号化されたチャネルを作成します。 Northbound 通信に SSL 暗号化には、次の要件が含まれています。

- ネットワーク コント ローラーのすべてのノードで同じ証明書が拡張キー使用法にサーバー認証とクライアント認証の目的を含む必要があります\(EKU\)拡張機能。 

- ネットワーク コント ローラーと通信する管理クライアントによって使用される URI は、証明書のサブジェクト名である必要があります。 証明書のサブジェクト名には、完全修飾ドメイン名 (FQDN) またはネットワーク コント ローラーの REST エンドポイントの IP アドレスのいずれかを含める必要があります。

- その証明書のサブジェクト名が使用される値と同じある必要がありますネットワーク コント ローラーのノードが異なるサブネット上にある場合は、 _RestName_パラメーター、**インストール NetworkController** WindowsPowerShell コマンド。 

- SSL 証明書を信頼のすべてのクライアント管理する必要があります。


### <a name="ssl-certificate-enrollment-and-configuration"></a>SSL 証明書の登録と構成

ネットワーク コント ローラーのノード上の SSL 証明書を手動で登録する必要があります。

証明書を登録すると後で証明書を使用するネットワーク コント ローラーを構成できます、 **- ServerCertificate**のパラメーター、**インストール NetworkController** Windows PowerShell コマンド. 使用して、いつでも構成を更新するにはネットワーク コント ローラーを既にインストールした場合、**セット NetworkController**コマンド。

>[!NOTE]
>SCVMM を使用している場合は、ライブラリ リソースとして、証明書を追加する必要があります。 詳細については、次を参照してください。 [VMM ファブリックで SDN ネットワーク コント ローラー設定](https://technet.microsoft.com/system-center-docs/vmm/scenario/sdn-network-controller)します。

## <a name="network-controller-cluster-communication"></a>ネットワーク コント ローラー クラスターの通信

ネットワーク コント ローラーは、ネットワーク コント ローラーのノード間の通信、認証、承認、および暗号化をサポートしています。 通信が経由で[Windows Communication Foundation](https://msdn.microsoft.com/library/ms731082.aspx) \(WCF\)と TCP です。

このモードを構成することができます、 **ClusterAuthentication**のパラメーター、**インストール NetworkControllerCluster** Windows PowerShell コマンド。 

詳細については、次を参照してください。[インストール NetworkControllerCluster](https://technet.microsoft.com/itpro/powershell/windows/network-controller/install-networkcontrollercluster)します。

### <a name="authentication"></a>認証

ネットワーク コント ローラーのクラスター間の通信の認証を構成するときにネットワーク コント ローラーのクラスター ノードが通信している他のノードの id を確認できます。

ネットワーク コント ローラーには、次の 3 つのネットワーク コント ローラーのノード間の認証モードがサポートしています。

>[!NOTE]
>SCVMM をのみを使用して、ネットワーク コント ローラーを展開するかどうかは**Kerberos**モードがサポートされています。

1. **Kerberos** です。 ネットワーク コント ローラーのすべてのクラスター ノードが認証に使用されるドメイン アカウントで、Active Directory ドメインに参加している場合は、Kerberos 認証を使用できます。

2. **X509**します。 X509 証明書は、\-ベースの認証。 クラスター ノードのネットワーク コント ローラーとの認証は、Active Directory ドメインに参加していない X509 を使用することができます。 X509 を使用するには、すべてのネットワーク コント ローラーがクラスター ノードに証明書を登録する必要があり、すべてのノードは、証明書を信頼する必要があります。 さらに、各ノードで登録されている証明書のサブジェクト名が、ノードの DNS 名と同じである必要があります。

3. **None**。 このモードを選択すると、ネットワーク コント ローラーのノード間で実行される認証がありません。 このモードでは、テスト目的にのみ提供され、実稼働環境での使用は推奨されません。

### <a name="authorization"></a>Authorization

ネットワーク コント ローラーのクラスター通信のための承認を構成する場合は、ネットワーク コント ローラー クラスターのノードが通信しているノードが信頼されていることを確認し、通信に参加するアクセス許可を持つを許可します。

ネットワーク コント ローラーでサポートされる認証モードのそれぞれについて、次の認証方法が使用されます。

1. **Kerberos** です。 ネットワーク コント ローラーのノードでは、その他のネットワーク コント ローラー コンピューター アカウントからのみ通信要求を受け入れます。 これらのアカウントを構成するを使用してネットワーク コント ローラーを展開するときに、**名前**のパラメーター、[新規 NetworkControllerNodeObject](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollernodeobject) Windows PowerShell コマンド。

2. **X509**します。 ネットワーク コント ローラーのノードでは、その他のネットワーク コント ローラー コンピューター アカウントからのみ通信要求を受け入れます。 これらのアカウントを構成するを使用してネットワーク コント ローラーを展開するときに、**名前**のパラメーター、[新規 NetworkControllerNodeObject](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollernodeobject) Windows PowerShell コマンド。

3. **None**。 このモードを選択すると、ネットワーク コント ローラーのノード間で実行される承認はありません。 このモードでは、テスト目的にのみ提供され、実稼働環境での使用は推奨されません。

### <a name="encryption"></a>暗号化

ネットワーク コント ローラーのノード間の通信は、WCF トランスポート レベルの暗号化を使用して暗号化されます。 認証と承認のメソッドで、Kerberos または X509 のいずれかの形態の暗号化が使用される証明書。 詳しくは、次のトピックをご覧ください。

- 「[Windows 資格情報でサービスをセキュリティで保護します。](https://msdn.microsoft.com/library/ms734673.aspx)
- 「[X.509 証明書でサービスをセキュリティで保護された](https://msdn.microsoft.com/library/ms788968.aspx)します。

## <a name="southbound-communication"></a>Southbound 通信

ネットワーク コント ローラーは、さまざまな種類の Southbound 通信用のデバイスと対話します。 これらのインタラクションは、さまざまなプロトコルを使用します。 このため、認証、承認、およびデバイスとネットワーク コント ローラーで、デバイスとの通信に使用されるプロトコルの種類に応じて暗号化のさまざまな要件があります。

次の表では、southbound のさまざまなデバイスとネットワーク コント ローラーの対話に関する情報を提供します。

| Southbound デバイス/サービス | プロトコル              | 認証の使用    |
|---------------------------|-----------------------|------------------------|
| ソフトウェア ロード バランサー    | WCF (マルチプレクサー) TCP (ホスト) | 証明書           |
| ファイアウォール                  | OVSDB                 | 証明書           |
| ゲートウェイ                   | WinRM                 | 証明書、Kerberos |
| 仮想ネットワーク        | OVSDB、WCF            | 証明書           |
| ユーザー定義ルーティング      | OVSDB                 | 証明書           |

これらのプロトコルのそれぞれについて、通信メカニズムは、次のセクションについて説明します。

### <a name="authentication"></a>認証

Southbound 通信は、次のプロトコルと認証方法を使用します。

1. **WCF/TCP/OVSDB**します。 X509 を使用してこれらのプロトコルの認証が実行される証明書。 ネットワーク コント ローラーとソフトウェアの負荷分散ピア\(SLB\)マルチプレクサー \(MUX \) /ホスト コンピューターが互いに相互認証に証明書を提示します。 各証明書は、リモート ピアによって信頼されている必要があります。

    Southbound 認証では、Northbound クライアントとの通信を暗号化するために構成されている同じ SSL 証明書を使用できます。 SLB MUX とホスト デバイスに証明書を構成することも必要があります。 証明書のサブジェクト名は、デバイスの DNS 名と同じである必要があります。

2. **WinRM**します。 このプロトコルでは、認証は Kerberos を使用して実行\(ドメインに参加しているマシン\)と証明書を使用して\(非ドメインに参加しているマシン\)します。

### <a name="authorization"></a>Authorization

Southbound 通信には、次のプロトコルおよび承認方式を使用します。

1. **WCF/TCP**します。 これらのプロトコルの承認は、ピア エンティティのサブジェクト名に基づいています。 ネットワーク コント ローラーは、ピア デバイスの DNS 名を格納し、承認に使用します。 この DNS 名は、デバイスの証明書のサブジェクト名と一致する必要があります。 同様に、ネットワーク コント ローラーの証明書は、ピア デバイスに格納されているネットワーク コント ローラーの DNS 名と一致する必要があります。

2. **WinRM**します。 Kerberos を使用している場合、WinRM クライアントのアカウントが Active Directory またはサーバー上のローカルの Administrators グループの定義済みグループに存在する場合があります。 証明書を使用している場合、クライアントは、サブジェクト名/発行者を使用して、サーバーの承認サーバーは、認証を実行するマップされたユーザー アカウントを使用しているサーバーに証明書を提示します。

3.  **OVSDB**します。 このプロトコルで提供される承認はありません。

### <a name="encryption"></a>暗号化

Southbound 通信は、次の暗号化方法は、プロトコルに使用されます。

1. **WCF/TCP/OVSDB**します。 これらのプロトコルの暗号化は、クライアントまたはサーバーに登録されている証明書を使用して実行されます。

2. **WinRM**します。 WinRM のトラフィックは既定では Kerberos セキュリティ サポート プロバイダーを使用して暗号化されます\(SSP\)します。 WinRM のサーバーで、SSL のフォームでは、追加の暗号化を構成できます。
