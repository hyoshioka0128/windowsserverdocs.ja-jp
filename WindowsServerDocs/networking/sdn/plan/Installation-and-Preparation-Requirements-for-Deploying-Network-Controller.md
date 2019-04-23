---
title: ネットワーク コント ローラーの展開の要件
description: データ センターを準備する、ネットワーク コント ローラーの展開は、1 つまたは複数のコンピューターまたは Vm と 1 台のコンピューターまたは VM が必要です。 ネットワーク コント ローラーを展開する前に、セキュリティ グループ、ログ ファイルの場所 (必要な場合)、および DNS 動的登録を構成する必要があります。
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: get-started-article
ms.assetid: 7f899e62-6e5b-4fca-9a59-130d4766ee2f
ms.author: pashort
author: shortpatti
ms.date: 08/10/2018
ms.openlocfilehash: 9db7609f6f1273c46cba1dd29f81c297bb26f94b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829863"
---
# <a name="requirements-for-deploying-network-controller"></a>ネットワーク コント ローラーの展開の要件

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

データ センターを準備する、ネットワーク コント ローラーの展開は、1 つまたは複数のコンピューターまたは Vm と 1 台のコンピューターまたは VM が必要です。 ネットワーク コント ローラーを展開する前に、セキュリティ グループ、ログ ファイルの場所 (必要な場合)、および DNS 動的登録を構成する必要があります。


## <a name="network-controller-requirements"></a>ネットワーク コント ローラーの要件

ネットワーク コント ローラーの展開では、1 つ以上のコンピューターまたはネットワーク コント ローラーの管理クライアントとして機能するには、ネットワーク コント ローラーと 1 台のコンピューターとして機能する Vm または VM が必要です。 

- すべての Vm とネットワーク コント ローラーのノードとして計画的なコンピューターに Windows Server 2016 Datacenter edition を実行する必要があります。 
- 任意のコンピューターまたはネットワーク コント ローラーをインストールするとなる仮想マシン (VM) に Windows Server 2016 の Datacenter edition を実行する必要があります。 
- 管理クライアント コンピューターまたはネットワーク コント ローラーの VM に Windows 10 を実行する必要があります。 

  
## <a name="configuration-requirements"></a>構成要件

ネットワーク コント ローラーを展開する前に、セキュリティ グループ、ログ ファイルの場所 (必要な場合)、および DNS 動的登録を構成する必要があります。
  
### <a name="step-1-configure-your-security-groups"></a>手順 1. セキュリティ グループを構成します。
  
最初に実行するには、Kerberos 認証の 2 つのセキュリティ グループを作成します。 

アクセス許可を持つユーザーのグループを作成します。 

1. ネットワーク コント ローラーを構成します。<p>Network Controller Admins では、このグループは、たとえば名前をことができます。 
2.  構成し、ネットワーク コント ローラーを使用して、ネットワークの管理<p>このグループのネットワーク コント ローラー ユーザーは、たとえば名前をことができます。 構成して、ネットワーク コント ローラーを管理するには、Representational State Transfer (REST) を使用します。

>[!NOTE]
>Active Directory ユーザーとコンピューター で、Domain Users グループのメンバーであるすべてのユーザーを追加する必要があります。

### <a name="step-2-configure-log-file-locations-if-needed"></a>手順 2.  必要に応じて、ログ ファイルの場所を構成します。

次に実行することは、ネットワーク コント ローラーのコンピューターまたは VM 上またはリモート ファイル共有のいずれかのネットワーク コント ローラーがデバッグ ログを格納するファイルの場所を構成します。 

>[!NOTE]
>リモート ファイル共有に、ログを格納する場合は、共有は、ネットワーク コント ローラーからアクセスできることを確認します。


### <a name="step-3-configure-dynamic-dns-registration-for-network-controller"></a>手順 3. ネットワーク コント ローラーの DNS 動的登録を構成します。
  
最後に、次に実行することでは、同じサブネットまたは異なるサブネットにネットワーク コント ローラー クラスターのノードを展開します。 

|もし...  |結果  |
|---------|---------|
|同じサブネット上 |ネットワーク コント ローラー REST IP アドレスを指定する必要があります。 |
|異なるサブネット上 |展開プロセス中に作成したネットワーク コント ローラー REST DNS 名を指定する必要があります。 次の実行もあります。<ul><li>DNS サーバーでは、ネットワーク コント ローラーの DNS 名の DNS 動的更新を構成します。</li><li>DNS 動的更新をネットワーク コント ローラーのノードのみに制限します。</li></ul> |
---

> [!NOTE]
> メンバーシップ**Domain Admins**、またはそれと同等がこれらの手順を実行するために必要な最低限です。
  
1. ゾーンの DNS 動的更新を許可します。

   a.  DNS マネージャーを開き、コンソール ツリーで、該当のゾーンを右クリックし、し順にクリックします**プロパティ**します。 
      
   b.  **全般** タブで、ゾーンの種類は、いずれかを確認します。**プライマリ**または**Active Directory 統合**します。

   c. **動的更新**、ことを確認します**Secure のみ**が選択されているし、をクリックし、 **[ok]** します。

2. ネットワーク コント ローラーのノードの DNS ゾーンのセキュリティ アクセス許可を構成します。

   a.   **[セキュリティ]** タブをクリックし、**[詳細設定]** をクリックします。 

   b.  **Advanced Security Settings**、 をクリックして**追加**します。 
  
   c. **[プリンシパルの選択]** をクリックします。 

   d. **ユーザーの選択、コンピューター、サービス アカウントまたはグループ**ダイアログ ボックスで、をクリックして**オブジェクトの種類**します。 

   e. **オブジェクトの種類**を選択します**コンピューター**、 をクリックし、 **OK**。

   f. **ユーザーの選択、コンピューター、サービス アカウントまたはグループ**ダイアログ ボックスで、展開でネットワーク コント ローラーのノードの 1 つの NetBIOS 名を入力し、順にクリックします**OK**します。

   g. **アクセス許可エントリ**、次の値を確認します。

      - **型**= を許可します。
      - **適用対象**= このオブジェクトとすべての子オブジェクト
  
   h.  **アクセス許可**を選択します**すべてのプロパティの書き込み**と**削除**、順にクリックします**OK**。

3. ネットワーク コント ローラーがクラスター内のすべてのコンピューターと Vm を繰り返します。

### <a name="step-4-configure-service-principal-name-if-using-kerberos-based-authentication"></a>手順 4. Kerberos を使用してベースの認証の場合は、サービス プリンシパル名を構成します。

ネットワーク コント ローラーが管理クライアントとの通信で Kerberos ベースの認証を使用している場合は、Active Directory でのネットワーク コント ローラーのサービス プリンシパル名 (SPN) を構成する必要があります。 ネットワーク コント ローラーには、SPN が自動的に構成されます。 行う必要があるすべては、登録およびは SPN を変更するには、ネットワーク コント ローラー コンピューターのアクセス許可を提供します。 詳細については、次を参照してください。[を構成するサービス プリンシパル名 (SPN)](https://docs.microsoft.com/windows-server/networking/sdn/security/kerberos-with-spn#configure-service-principal-names-spn)します。

## <a name="deployment-options"></a>展開オプション

### <a name="network-controller-deployment"></a>ネットワーク コント ローラーの展開

セットアップは、仮想マシンで構成されている 3 つのネットワーク コント ローラーのノードが高可用性です。 また、web 層とデータベース層をシミュレートする 2 つの仮想サブネットに分割されたテナント 2 の仮想ネットワークと 2 つのテナントも示します。  

![SDN NC の計画](../../media/Plan-a-Software-Defined-Network-Infrastructure/SDN-NC-Planning.png)

### <a name="network-controller-and-software-load-balancer-deployment"></a>ネットワーク コント ローラーとソフトウェア ロード バランサーの展開

高可用性は、2 つ以上の SLB/MUX ノードがあります。
   
![SDN NC の計画](../../media/Plan-a-Software-Defined-Network-Infrastructure/SDN-SLB-Deployment.png)
  
### <a name="network-controller-software-load-balancer-and-ras-gateway-deployment"></a>ネットワーク コント ローラー、ソフトウェア ロード バランサー、および RAS ゲートウェイの展開

次の 3 つのゲートウェイ仮想マシン; があります。2 つがアクティブになり、1 つが冗長です。

![SDN NC の計画](../../media/Plan-a-Software-Defined-Network-Infrastructure/SDN-GW-Deployment.png)  
  
  
  
TP5 ベースのデプロイの自動化、Active Directory が使用可能なこれらのサブネットから到達可能である必要があります。 Active Directory の詳細については、次を参照してください。 [Active Directory Domain Services の概要](https://docs.microsoft.com/windows-server/identity/ad-ds/get-started/virtual-dc/active-directory-domain-services-overview)します。  
  
>[!IMPORTANT] 
>VMM を使用してを展開する場合は、インフラストラクチャ、仮想マシンを確認します (SQL Server を VMM サーバー、AD と DNS など)、図に示す 4 つのホストのいずれかでホストされていません。  


## <a name="next-steps"></a>次のステップ
[ソフトウェア定義ネットワーク インフラストラクチャ計画](https://technet.microsoft.com/windows-server-docs/networking/sdn/plan/plan-a-software-defined-network-infrastructure)します。

## <a name="related-topics"></a>関連トピック
- [ネットワーク コント ローラー](../technologies/network-controller/Network-Controller.md) 
- [ネットワーク コント ローラーの高可用性](../technologies/network-controller/network-controller-high-availability.md) 
- [Windows PowerShell を使用してネットワーク コント ローラーを展開します。](../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)   
- [サーバー マネージャーを使用して、ネットワーク コント ローラー サーバーの役割をインストールします。](../technologies/network-controller/Install-the-Network-Controller-server-role-using-Server-Manager.md)   
