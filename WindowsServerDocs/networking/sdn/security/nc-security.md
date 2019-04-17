---
title: ネットワーク コントローラーのセキュリティ
description: このトピックを使用すると、ネットワーク コントローラーとその他のソフトウェアとデバイス間ですべての通信のセキュリティを構成するのに方法について説明します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: bc625de9-ee31-40a4-9ad2-7448bfbfb6e6
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ab04d3f528beb037988e6390fe85ad9af219266b
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="network-controller-security"></a>ネットワーク コントローラーのセキュリティ

このトピックを使用すると、ネットワーク コントローラーとその他のソフトウェアとデバイス間ですべての通信のセキュリティを構成するのに方法について説明します。 

>[!NOTE]
>ネットワーク コントローラーの概要については、次を参照してください。[ネットワーク コントローラー](../technologies/network-controller/network-controller.md)します。

セキュリティで保護することができる通信パスには、管理面、クラスターでは、ネットワーク コントローラーの仮想マシン \(VMs\) と Southbound の通信データ面の間のクラスター通信での通信 Northbound にはが含まれます。

1. **Northbound 通信**します。 ネットワーク コントローラーのように Windows PowerShell および System Center Virtual Machine Manager \(SCVMM\) SDN\ 対応の管理ソフトウェアを使用して管理平面上と通信します。 これらの管理ツールは、ネットワーク ポリシーを定義して、目標とする状態と同等に実際の構成を移植する実際のネットワーク構成を比較する対象となる、ネットワークの目的の状態を作成する機能を提供します。

2. **ネットワーク コントローラー クラスター通信**します。 ネットワーク コントローラーのクラスター ノードとして次の 3 つ以上の Vm を構成するときに、これらのノードは、相互に通信します。 この通信は、ノード、またはネットワーク コントローラー サービス間の特定の通信経由で同期してデータのレプリケーションに関連する可能性があります。

3.  **Southbound 通信**します。 ネットワーク コントローラーは、SDN インフラストラクチャとソフトウェア ロード バランサー、ゲートウェイ、およびホスト コンピューターと同様に、その他のデバイスを使用してデータの平面に通信します。 ネットワーク コントローラーを使用して、構成およびネットワーク用に構成する目的の状態を維持するように、southbound これらのデバイスを管理することができます。

## <a name="northbound-communication"></a>Northbound 通信

ネットワーク コントローラーは、Northbound 通信の認証、承認、および暗号化をサポートします。 次のセクションでは、これらのセキュリティ設定を構成する方法についてを説明します。

**認証**

ネットワーク コントローラーの Northbound 通信の認証を構成するときにクラスター ノードのネットワーク コントローラーと通信しているデバイスの ID を確認するクライアントを管理できるようにします。

ネットワーク コントローラーは、次の 3 つのモードのクライアント管理とネットワーク コントローラーのノード間で認証をサポートしています。

>[!Note]
>System Center Virtual Machine Manager でのネットワーク コントローラーをのみ展開するかどうか**Kerberos**モードをサポートします。

1. **Kerberos**します。 認証に使用されるドメイン アカウントを持つ、SCVMM とネットワーク コントローラーのすべてのクラスター ノードを実行しているコンピューターなどの両方の管理クライアントが、Active Directory ドメインに参加している場合は、Kerberos 認証を使用できます。

2. **X509**します。 X509 は、certificate\ ベースの認証には X509 を使用する管理クライアントが Active Directory ドメインに参加していないときに認証します。 使用するには X509 証明書をすべてのクラスター ノードのネットワーク コントローラーとクライアントの管理を登録する必要があり、すべてのノードとクライアントを管理する必要があります相互に信頼関係の"証明書。

3. **None**します。 このモードを選択すると、認証のクライアント管理とネットワーク コントローラーの間で実行されることはありません。 このモードでは、テスト目的で、だけが提供され、実稼働環境での使用はお勧めしません。 

Northbound 通信の認証モードを構成するには、Windows PowerShell コマンドを使用して**インストール NetworkController**と、**ClientAuthentication**パラメーター。 

詳細については、次のトピックを参照してください。 

- [Install-NetworkController](https://technet.microsoft.com/itpro/powershell/windows/network-controller/install-networkcontroller)
- [Set-NetworkController](https://technet.microsoft.com/itpro/powershell/windows/network-controller/set-networkcontroller)

**承認**

ネットワーク コントローラーの Northbound 通信用の承認を構成するときに、クラスター ノードのネットワーク コントローラーと通信しているデバイスが信頼されているし、通信に参加するアクセス許可があることを確認するクライアントの管理を許可します。

ネットワーク コントローラーでサポートされている認証モードごとに、次の認証方法が使用されます。

1.  **Kerberos**します。 Kerberos 認証方法を使用している場合は、ユーザーと、Active Directory でセキュリティ グループを作成し、[承認されたユーザーとコンピューターをグループにネットワーク コントローラーと通信するために承認されているコンピューターを定義します。 使用して、承認のため、セキュリティ グループを使用するネットワーク コントローラーを構成することができます、**ClientSecurityGroup**のパラメーター、**インストール NetworkController**の Windows PowerShell コマンド。 使用して、セキュリティ グループを変更するにはネットワーク コントローラーをインストールした後、[セット NetworkController](https://technet.microsoft.com/itpro/powershell/windows/network-controller/set-networkcontroller)コマンド パラメーターに**- ClientSecurityGroup**します。 SCVMM を使用している場合、セキュリティ グループを展開時にパラメーターとして指定する必要があります。

2.  **X509**します。 使用する場合は、X509 認証方法、ネットワーク コントローラーのみを受け付けますネットワーク コントローラーが証明書の拇印がわかっている管理クライアントからの要求。 これらの拇印を使用して構成することができます、**ClientCertificateThumbprint**のパラメーター、**インストール NetworkController**の Windows PowerShell コマンド。 使用して、いつでもその他のクライアントの拇印を追加することができます、**セット NetworkController**コマンド。

3.  **None**します。 このモードを選択すると、クライアント管理とネットワーク コントローラーのノード間の通信が試行されたときに実行される承認はありません。 このモードでは、テスト目的で、だけが提供され、実稼働環境での使用はお勧めしません。 

詳細については、次のトピックを参照してください。 

- [Install-NetworkController](https://technet.microsoft.com/itpro/powershell/windows/network-controller/install-networkcontroller)
- [Set-NetworkController](https://technet.microsoft.com/itpro/powershell/windows/network-controller/set-networkcontroller)

**暗号化**

Northbound 通信では、Secure Sockets Layer \(SSL\) を使用して、管理のクライアントとネットワーク コントローラーのノード間で暗号化されたチャネルを作成します。 Northbound 通信用の SSL 暗号化には、次の要件が含まれています。

- ネットワーク コントローラーのすべてのノードを含むサーバー認証およびクライアント認証の目的上、拡張キー使用法 \(EKU\) 拡張機能と同じ証明書が必要です。 

- ネットワーク コントローラーと通信する管理クライアントによって使用される URI は、証明書のサブジェクト名にする必要があります。 証明書のサブジェクト名は、完全修飾ドメイン名 (FQDN) またはネットワーク コントローラーの REST エンドポイントの IP アドレスのいずれかを含める必要があります。

- 異なるサブネット上にネットワーク コントローラーのノードがある場合、証明書のサブジェクト名がありますに使用する値と同じ、**RestName**のパラメーター、**インストール NetworkController**の Windows PowerShell コマンド。 

- SSL 証明書は、すべてのクライアント管理で信頼されている必要があります。

### <a name="ssl-certificate-enrollment-and-configuration"></a>SSL 証明書の登録と構成

ネットワーク コントローラーのノード上の SSL 証明書を手動で登録する必要があります。

証明書を登録すると後で証明書を使用するネットワーク コントローラーを構成できます、**- サーバー証明書**のパラメーター、**インストール NetworkController**の Windows PowerShell コマンド。 使用して、いつでも構成を更新するには既にネットワーク コントローラーをインストールした場合、**セット NetworkController**コマンド。

>[!NOTE]
>SCVMM を使用している場合は、ライブラリ リソースとして、証明書を追加する必要があります。 詳細については、次を参照してください。[VMM ファブリックにおける、SDN ネットワーク コントローラーをセットアップ](https://technet.microsoft.com/system-center-docs/vmm/scenario/sdn-network-controller)します。

## <a name="network-controller-cluster-communication"></a>ネットワーク コントローラー クラスター通信

ネットワーク コントローラーは、ネットワーク コントローラーのノード間の通信、認証、承認、および暗号化をサポートしています。 経由で通信には[Windows Communication Foundation](https://msdn.microsoft.com/library/ms731082.aspx) \(WCF\) と TCP します。

このモードを構成することができます、**ClusterAuthentication**のパラメーター、**インストール NetworkControllerCluster**の Windows PowerShell コマンド。 

詳細については、次を参照してください。[インストール NetworkControllerCluster](https://technet.microsoft.com/itpro/powershell/windows/network-controller/install-networkcontrollercluster)します。

**認証**

ネットワーク コントローラー クラスター間の通信の認証を構成するときに、ネットワーク コントローラーのクラスター ノードが通信するその他のノードの ID を検証を許可します。

ネットワーク コントローラーは、次の 3 つのネットワーク コントローラーのノード間の認証モードをサポートしています。

>[!NOTE]
>SCVMM をのみを使用して、ネットワーク コントローラーを展開するかどうかは**Kerberos**モードをサポートします。

1. **Kerberos**します。 ネットワーク コントローラーのすべてのクラスター ノードが認証に使用されるドメイン アカウントで、Active Directory ドメインに参加している場合は、Kerberos 認証を使用できます。

2. **X509**します。 X509 は、certificate\ ベースの認証には クラスター ノードのネットワーク コントローラーとの認証は、Active Directory ドメインに参加していない X509 を使用することができます。 X509 を使用するには、ネットワーク コントローラーのすべてのクラスター ノードに対して証明書を登録する必要があり、すべてのノードが、証明書を信頼する必要があります。 さらに、各ノードで登録されている証明書のサブジェクト名がノードの DNS 名と同じである必要があります。

3. **None**します。 このモードを選択すると、ネットワーク コントローラーのノード間で行われる認証はありません。 このモードでは、テスト目的で、だけが提供され、実稼働環境での使用はお勧めしません。

**承認**

ネットワーク コントローラー クラスター通信用の承認を構成するときに、ネットワーク コントローラーのクラスター ノードを使用する通信しているノードが信頼されていることを確認し、通信に参加するアクセス許可を持ってを許可します。

ネットワーク コントローラーでサポートされている認証モードごとに、次の認証方法が使用されます。

1. **Kerberos**します。 ネットワーク コントローラーのノードでは、その他のネットワーク コントローラー コンピューター アカウントからのみ通信要求を受け入れます。 これらのアカウントを構成するを使用してネットワーク コントローラーを展開するときに、**名**のパラメーター、[新規 NetworkControllerNodeObject](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollernodeobject)の Windows PowerShell コマンド。

2. **X509**します。 ネットワーク コントローラーのノードでは、その他のネットワーク コントローラー コンピューター アカウントからのみ通信要求を受け入れます。 これらのアカウントを構成するを使用してネットワーク コントローラーを展開するときに、**名**のパラメーター、[新規 NetworkControllerNodeObject](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollernodeobject)の Windows PowerShell コマンド。

3. **None**します。 このモードを選択すると、ネットワーク コントローラーのノード間で実行される承認はありません。 このモードでは、テスト目的で、だけが提供され、実稼働環境での使用はお勧めしません。

**暗号化**

ネットワーク コントローラーのノード間の通信は、WCF トランスポート レベルの暗号化を使用して暗号化されます。 認証および承認の方法が Kerberos または X509 場合に、この形式の暗号化が使用される証明書。 詳細については、次のトピックを参照してください。

- [方法: Windows 資格情報を使用してサービスをセキュリティで保護されました。](https://msdn.microsoft.com/library/ms734673.aspx)
- [方法: X.509 証明書を使用してサービスをセキュリティで保護された](https://msdn.microsoft.com/library/ms788968.aspx)します。

## <a name="southbound-communication"></a>Southbound 通信

ネットワーク コントローラーは、Southbound 通信用のデバイスの種類とやり取りします。 これらの操作は、さまざまなプロトコルを使用します。 このためは、認証、承認、およびデバイスとネットワーク コントローラーで、デバイスとの通信に使用されるプロトコルの種類によって暗号化の要件は異なります。

次の表は、southbound のさまざまなデバイスとネットワーク コントローラーの対話に関する情報を提供します。

| Southbound デバイス/サービス | プロトコル              | 使用する認証    |
|---------------------------|-----------------------|------------------------|
| ソフトウェア ロード バランサー    | WCF (マルチプレクサー) TCP (ホスト) | 証明書           |
| ファイアウォール                  | OVSDB                 | 証明書           |
| ゲートウェイ                   | WinRM                 | Kerberos、証明書 |
| 仮想ネットワーク        | OVSDB、WCF            | 証明書           |
| ユーザー定義のルーティング      | OVSDB                 | 証明書           |

これらのプロトコルのそれぞれについては、通信メカニズムは、次のセクションで説明します。

**認証**

Southbound 通信は、次のプロトコルと認証方法が使用されます。

1. **WCF/TCP/OVSDB**します。 これらのプロトコル、認証が実行 X509 を使用して証明書。 ネットワーク コントローラーとソフトウェアの負荷分散 \(SLB\) ピア マルチプレクサー \ (MUX\)]、[ホストのマシンが相互に相互認証用証明書を提示します。 各証明書は、リモート ピアによって信頼されている必要があります。

    Southbound 認証は、Northbound クライアントとの通信を暗号化するために構成されている同じ SSL 証明書を使用できます。 SLB MUX とホスト デバイスの証明書を構成することも必要があります。 証明書のサブジェクト名は、デバイスの DNS 名と同じである必要があります。

2. **WinRM**します。 このプロトコルの認証は Kerberos を使用して実行 \ (ドメインに参加して machines\) の証明書を使用して \ (非ドメインに参加している machines\) 用です。

**承認**

Southbound 通信は、次のプロトコルと認証方法が使用されます。

1. **WCF/TCP**します。 これらのプロトコルの承認は、ピア エンティティのサブジェクト名に基づいています。 ネットワーク コントローラーでは、ピア デバイスの DNS 名を格納し、承認に使用します。 この DNS 名は、デバイスに証明書のサブジェクト名と一致する必要があります。 同様に、ネットワーク コントローラーの証明書は、ピア デバイスに保存されているネットワーク コントローラーの DNS 名と一致する必要があります。

2. **WinRM**します。 Kerberos が使用されている場合、WinRM クライアントのアカウントが Active Directory またはサーバーのローカルの Administrators グループの定義済みのグループに存在する必要があります。 証明書を使用している場合、クライアントは、サブジェクト名/発行者を使用して、サーバーを認証サーバーが認証を実行する、マップされたユーザー アカウントを使用しているサーバーに証明書を提示します。

3.  **OVSDB**します。 このプロトコルに提供される承認はありません。

**暗号化**

Southbound 通信は、プロトコル、次の暗号化方法が使用されます。

1. **WCF/TCP/OVSDB**します。 これらのプロトコルでは、暗号化は、クライアントまたはサーバーに登録されている証明書を使用して実行されます。

2. **WinRM**します。 既定では Kerberos セキュリティ サポート プロバイダーを使用して WinRM トラフィックは暗号化 \(SSP\) します。 WinRM サーバーで、SSL のフォームで、追加の暗号化を構成できます。
