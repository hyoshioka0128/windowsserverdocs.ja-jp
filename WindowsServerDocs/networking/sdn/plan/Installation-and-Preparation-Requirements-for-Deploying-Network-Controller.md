---
title: ネットワークコントローラーを展開するための要件
description: ネットワークコントローラーを展開するために、1台以上のコンピューターまたは Vm、1台のコンピューターまたは VM を必要とするデータセンターを準備します。 ネットワークコントローラーを展開する前に、セキュリティグループ、ログファイルの場所 (必要な場合)、および動的 DNS の登録を構成する必要があります。
manager: grcusanz
ms.topic: get-started-article
ms.assetid: 7f899e62-6e5b-4fca-9a59-130d4766ee2f
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/10/2018
ms.openlocfilehash: 051518873bd028e8b1253b9bf7cb17dcff344d0d
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87996601"
---
# <a name="requirements-for-deploying-network-controller"></a>ネットワークコントローラーを展開するための要件

>適用先:Windows Server (半期チャネル)、Windows Server 2016

ネットワークコントローラーを展開するために、1台以上のコンピューターまたは Vm、1台のコンピューターまたは VM を必要とするデータセンターを準備します。 ネットワークコントローラーを展開する前に、セキュリティグループ、ログファイルの場所 (必要な場合)、および動的 DNS の登録を構成する必要があります。


## <a name="network-controller-requirements"></a>ネットワークコントローラーの要件

ネットワークコントローラーの展開には、ネットワークコントローラーとして機能する1つ以上のコンピューターまたは Vm、およびネットワークコントローラーの管理クライアントとして機能する1台のコンピューターまたは VM が必要です。

- ネットワークコントローラーノードとして計画されているすべての Vm とコンピューターは、Windows Server 2016 Datacenter edition を実行している必要があります。
- ネットワークコントローラーをインストールするすべてのコンピューターまたは仮想マシン (VM) で、Windows Server 2016 の Datacenter edition が実行されている必要があります。
- 管理クライアントコンピューターまたはネットワークコントローラーの VM は、Windows 10 を実行している必要があります。


## <a name="configuration-requirements"></a>構成要件

ネットワークコントローラーを展開する前に、セキュリティグループ、ログファイルの場所 (必要な場合)、および動的 DNS の登録を構成する必要があります。

### <a name="step-1-configure-your-security-groups"></a>手順 1. セキュリティグループを構成する

まず、Kerberos 認証用に2つのセキュリティグループを作成します。

次の権限を持つユーザーのグループを作成します。

1. ネットワークコントローラーの構成<p>このグループには、たとえばネットワークコントローラーの管理者という名前を指定できます。
2.  ネットワークコントローラーを使用してネットワークを構成および管理する<p>このグループには、ネットワークコントローラーのユーザーなどの名前を指定できます。 ネットワークコントローラーを構成および管理するには、表現を使用します。

>[!NOTE]
>追加するすべてのユーザーは、Active Directory ユーザーとコンピューターの Domain Users グループのメンバーである必要があります。

### <a name="step-2-configure-log-file-locations-if-needed"></a>手順 2. 必要に応じてログファイルの場所を構成する

次に行う必要があるのは、ネットワークコントローラーのデバッグログをネットワークコントローラーコンピューターまたは VM、またはリモートファイル共有に保存するようにファイルの場所を構成することです。

>[!NOTE]
>リモートファイル共有にログを保存する場合は、ネットワークコントローラーから共有にアクセスできることを確認してください。


### <a name="step-3-configure-dynamic-dns-registration-for-network-controller"></a>手順 3. ネットワークコントローラーの動的 DNS 登録を構成する

最後に、同じサブネットまたは異なるサブネットにネットワークコントローラークラスターノードを展開します。


|         条件         |                                                                                                                                                         結果                                                                                                                                                         |
|-----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  同じサブネット上で、  |                                                                                                                                ネットワークコントローラーの REST IP アドレスを指定する必要があります。                                                                                                                                 |
| 異なるサブネットでは、 | ネットワークコントローラーの REST DNS 名を指定する必要があります。これは、展開プロセスで作成します。 また、次の操作を行う必要があります。<ul><li>Dns サーバーで、ネットワークコントローラーの DNS 名の DNS 動的更新を構成します。</li><li>DNS 動的更新をネットワークコントローラーノードのみに制限します。</li></ul> |

---

> [!NOTE]
> これらの手順を実行するには、 **Domain Admins**のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。

1. ゾーンの DNS 動的更新を許可します。

   a. DNS マネージャーを開き、コンソールツリーで該当するゾーンを右クリックし、[**プロパティ**] をクリックします。

   b. [**全般**] タブで、ゾーンの種類が [**プライマリ**] または [ **Active Directory 統合**] であることを確認します。

   c. [**動的更新**] で、[**セキュリティのみ**] が選択されていることを確認し、[ **OK]** をクリックします。

2. ネットワークコントローラーノードの DNS ゾーンセキュリティアクセス許可を構成する

   a.  [**セキュリティ**] タブをクリックし、[**詳細設定**] をクリックします。

   b. [**セキュリティの詳細設定**] で、[**追加**] をクリックします。

   c. **[プリンシパルの選択]** をクリックします。

   d. [**ユーザー、コンピューター、サービスアカウントまたはグループの選択**] ダイアログボックスで、[**オブジェクトの種類**] をクリックします。

   e. [**オブジェクトの種類**] で、[**コンピューター**] を選択し、[ **OK**] をクリックします。

   f. **[ユーザー、コンピューター、サービスアカウント、またはグループの選択**] ダイアログボックスで、展開内のいずれかのネットワークコントローラーノードの NetBIOS 名を入力し、[ **OK]** をクリックします。

   g. [**アクセス許可エントリ**] で、次の値を確認します。

      - **種類**= 許可
      - **適用対象**= This オブジェクトとすべての子オブジェクト

   h. [**アクセス許可**] で [**すべてのプロパティの書き込み**] を選択し、[**削除**] をクリックして、[ **OK]** をクリックします。

3. ネットワークコントローラークラスター内のすべてのコンピューターと Vm に対して、この手順を繰り返します。

### <a name="step-4-configure-service-principal-name-if-using-kerberos-based-authentication"></a>手順 4. Kerberos ベースの認証を使用する場合のサービスプリンシパル名の構成

ネットワークコントローラーが管理クライアントとの通信に Kerberos ベースの認証を使用している場合は、Active Directory でネットワークコントローラーのサービスプリンシパル名 (SPN) を構成する必要があります。 SPN は、ネットワークコントローラーによって自動的に構成されます。 必要なのは、SPN を登録および変更するためのアクセス許可をネットワークコントローラーコンピューターに付与することだけです。 詳細については、「[サービスプリンシパル名 (SPN) の構成](../security/kerberos-with-spn.md#configure-service-principal-names-spn)」を参照してください。

## <a name="deployment-options"></a>配置オプション

### <a name="network-controller-deployment"></a>ネットワークコントローラーの展開

このセットアップは、仮想マシン上に3つのネットワークコントローラーノードが構成されている場合に高可用性を実現します。 また、web 層とデータベース層をシミュレートするために、2つの仮想サブネットに分類されたテナント2の仮想ネットワークを持つ2つのテナントも示しています。

![SDN NC 計画](../../media/Plan-a-Software-Defined-Network-Infrastructure/SDN-NC-Planning.png)

### <a name="network-controller-and-software-load-balancer-deployment"></a>ネットワークコントローラーとソフトウェアロードバランサーの展開

高可用性を高めるために、2つ以上の SLB/MUX ノードがあります。

![SDN NC 計画](../../media/Plan-a-Software-Defined-Network-Infrastructure/SDN-SLB-Deployment.png)

### <a name="network-controller-software-load-balancer-and-ras-gateway-deployment"></a>ネットワークコントローラー、ソフトウェア Load Balancer、RAS ゲートウェイの展開

ゲートウェイ仮想マシンは3つあります。2つはアクティブで、1つは冗長です。

![SDN NC 計画](../../media/Plan-a-Software-Defined-Network-Infrastructure/SDN-GW-Deployment.png)

>[!IMPORTANT]
>VMM を使用して展開する場合は、インフラストラクチャの仮想マシン (VMM サーバー、AD/DNS、SQL Server など) が、図に示されている4つのホストのいずれかでホストされていないことを確認してください。


## <a name="next-steps"></a>次のステップ
[ソフトウェアで定義されたネットワークインフラストラクチャを計画](./plan-a-software-defined-network-infrastructure.md)します。

## <a name="related-topics"></a>関連トピック
- [ネットワーク コントローラー](../technologies/network-controller/Network-Controller.md)
- [ネットワークコントローラーの高可用性](../technologies/network-controller/network-controller-high-availability.md)
- [Windows PowerShell を使用してネットワーク コントローラーを展開する](../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)
- [サーバー マネージャーを使用してネットワーク コントローラー サーバーの役割をインストールする](../technologies/network-controller/Install-the-Network-Controller-server-role-using-Server-Manager.md)