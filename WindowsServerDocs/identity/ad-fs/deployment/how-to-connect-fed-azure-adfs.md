---
title: Azure active Directory フェデレーション サービス |Microsoft Docs
description: このドキュメントでは、高可用性を Azure に AD FS をデプロイする方法を学びます。
services: active-directory
documentationcenter: ''
author: billmath
manager: mtillman
editor: ''
ms.assetid: 692a188c-badc-44aa-ba86-71c0e8074510
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/28/2018
ms.subservice: hybrid
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 588bc3f87c78feccac47d18d31d37be3b1a02d2f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835103"
---
# <a name="deploying-active-directory-federation-services-in-azure"></a>Azure Active Directory フェデレーション サービスを展開します。
AD FS では、シンプルで安全な id フェデレーションと Web シングル サインオン (SSO) 機能を提供します。 Azure AD とのフェデレーションまたは O365 は、オンプレミスの資格情報を使用して認証し、クラウド内のすべてのリソースにアクセスするユーザーを有効にします。 オンプレミスのリソースにアクセスするために高可用性 AD FS インフラストラクチャに重要になりますこの結果、およびクラウドで。 Azure での AD FS を展開すると、最小限の手間で必要な高可用性を実現できます。
Azure での AD FS を展開するいくつかの利点は、その一部を以下に示します。

* **高可用性**-Azure 可用性セットの能力、高可用性インフラストラクチャを確認します。
* **簡単にスケールできます**– 高いパフォーマンスが必要ですか? 高性能なマシンを Azure でほんの数回のクリックで簡単に移行します。
* **地域を越えた冗長性**– に Azure Geo 冗長性を世界規模でのインフラストラクチャの高可用性を保証します。
* **簡単に管理**– を Azure portal の非常に簡略化された管理オプションでは、とても簡単で手間のかからない、インフラストラクチャの管理は 

## <a name="design-principles"></a>設計原則
![展開の設計](./media/how-to-connect-fed-azure-adfs/deployment.png)

上記の図は、Azure で AD FS インフラストラクチャの展開を開始することをお勧めの基本的なトポロジを示しています。 トポロジのさまざまなコンポーネントの背後にある原則は、以下に示します。

* **DC/ADFS サーバー**:1,000 人未満のユーザーがいる場合は、ドメイン コント ローラーに単に AD FS の役割をインストールできます。 ドメイン コント ローラーのパフォーマンスに対する影響しないようにする場合、または 1,000 を超えるユーザーがいる場合は、別のサーバーで AD FS をデプロイします。
* **WAP サーバー** – ユーザーが AD FS の場合は、企業ネットワーク上もに到達できるように、Web アプリケーション プロキシ サーバーを展開する必要は。
* **DMZ**:Web アプリケーション プロキシ サーバーは DMZ に配置して、DMZ と内部サブネット間のみ tcp/443 アクセスが許可されています。
* **ロード バランサー**:AD FS と Web アプリケーション プロキシ サーバーの高可用性を確保するには、Web アプリケーション プロキシ サーバーの AD FS サーバーと Azure Load Balancer の内部ロード バランサーの使用をお勧めします。
* **可用性セット**:AD FS デプロイに冗長性を提供するには、同様のワークロードの可用性セット内の 2 つ以上の仮想マシンをグループ化することをお勧めします。 この構成により、いずれかの中に、計画または計画外メンテナンス イベント中でも、少なくとも 1 つの仮想マシンは利用できること
* **ストレージ アカウント**:2 つのストレージ アカウントを持っていることをお勧めします。 1 つのストレージ アカウントがあることと、単一障害点を作成する可能性があります、可能性は低いシナリオでは、ストレージ アカウントがダウン使用不可になる展開が発生することができます。 2 つのストレージ アカウントには、障害系統ごとに 1 つのストレージ アカウントを関連付けることができます。
* **ネットワークの分離**:Web アプリケーション プロキシ サーバーは、別個の DMZ ネットワークにデプロイする必要があります。 1 つの仮想ネットワークを 2 つのサブネットに分割し、分離したサブネット内の Web アプリケーション プロキシ サーバーを展開できます。 単に、各サブネットに対してネットワーク セキュリティ グループの設定を構成し、2 つのサブネット間の通信に必要なもののみを許可できます。 詳細については次のデプロイ シナリオごとに与えられます

## <a name="steps-to-deploy-ad-fs-in-azure"></a>Azure での AD FS をデプロイする手順
このセクションで説明されている手順展開ガイドの概要、Azure で AD FS インフラストラクチャを示した以下。

### <a name="1-deploying-the-network"></a>1. ネットワークをデプロイします。
上記で説明した、することができますか、1 つの仮想ネットワークに 2 つのサブネットを作成します。 そうしない 2 つのまったく異なる仮想ネットワーク (VNet) を作成します。 この記事では、単一の仮想ネットワークをデプロイに集中し、2 つのサブネットに分割されます。 これは、現在、2 つの個別の Vnet との通信、VNet ゲートウェイに VNet を必要とするより簡単な方法です。

**1.1 仮想ネットワークを作成します。**

![仮想ネットワークを作成します。](./media/how-to-connect-fed-azure-adfs/deploynetwork1.png)

Azure portal の仮想ネットワークを選択して展開できます仮想ネットワークと 1 回のクリックですぐに 1 つのサブネット。 INT サブネットも定義されていて、準備が Vm を追加するようになりました整います。
次の手順では、ネットワーク (DMZ サブネット) に別のサブネットを追加します。 単に、DMZ サブネットを作成するには

* 新しく作成したネットワークを選択します。
* プロパティで、サブネットを選択します。
* サブネットのパネルは [追加] をクリックします。
* サブネットを作成するサブネットの名前とアドレス空間情報を提供します。

![［サブネット］](./media/how-to-connect-fed-azure-adfs/deploynetwork2.png)

![DMZ サブネット](./media/how-to-connect-fed-azure-adfs/deploynetwork3.png)

**1.2.ネットワーク セキュリティ グループを作成します。**

ネットワーク セキュリティ グループ (NSG) には、許可または仮想ネットワークの VM インスタンスへのネットワーク トラフィックを拒否するアクセス制御リスト (ACL) 規則の一覧が含まれています。 Nsg は、サブネットまたはそのサブネット内の個々 の VM インスタンスと関連付けることができます。 NSG がサブネットに関連付け、ACL 規則は、そのサブネット内のすべての VM インスタンスに適用されます。
ガイダンスについては、この目的では、2 つの Nsg を作成します。 内部ネットワークと DMZ に対して 1 つずつです。 これらはある NSG_INT と NSG_DMZ というそれぞれします。

![NSG を作成します。](./media/how-to-connect-fed-azure-adfs/creatensg1.png)

NSG を作成した後は、0 の受信と 0 送信規則があります。 それぞれのサーバー上の役割がインストールされ、機能すると、必要なセキュリティ レベルに従って受信と送信規則を作成できます。

![NSG を初期化します。](./media/how-to-connect-fed-azure-adfs/nsgint1.png)

Nsg が作成されると、nsg_int をサブネット INT と NSG_DMZ をサブネット DMZ にします。 次の例のスクリーン ショットのとおりです。

![NSG を構成します。](./media/how-to-connect-fed-azure-adfs/nsgconfigure1.png)

* サブネットのパネルを開くにはサブネットをクリックします。
* NSG に関連付けるサブネットを選択します。 

構成の後、サブネットのパネルは以下のようになる必要があります。

![NSG の後にサブネット](./media/how-to-connect-fed-azure-adfs/nsgconfigure2.png)

**1.3.オンプレミスへの接続を作成します。**

Azure でドメイン コント ローラー (DC) をデプロイするには、オンプレミスへの接続を必要になります。 Azure では、お客様のオンプレミス インフラストラクチャを Azure のインフラストラクチャに接続するさまざまな接続オプションを提供します。

* ポイント対サイト
* 仮想ネットワーク サイト対サイト
* ExpressRoute

ExpressRoute を使用することをお勧めします。 ExpressRoute を使用して、Azure データ センターとお客様のオンプレミスまたはコロケーション環境にあるインフラストラクチャの間にプライベート接続を作成できます。 ExpressRoute 接続は、パブリック インターネット経由ではなりません。 詳細の信頼性、速度、待機時間が少なく、およびセキュリティの高い一般的な接続よりも、インターネット経由で提供します。
ExpressRoute を使用することをお勧めしますが、任意の接続方法が組織に最適なこともできます。 ExpressRoute を使用して、さまざまな接続オプションと ExpressRoute の詳細については、読み取る[ExpressRoute の技術概要](https://aka.ms/Azure/ExpressRoute)します。

### <a name="2-create-storage-accounts"></a>2. ストレージ アカウントを作成します。
高可用性を維持し、1 つのストレージ アカウントへの依存を回避するためには、2 つのストレージ アカウントを作成できます。 各可用性セット内のマシンを 2 つのグループに分割し、別のストレージ アカウントを各グループに割り当てます。

![ストレージ アカウントを作成します。](./media/how-to-connect-fed-azure-adfs/storageaccount1.png)

### <a name="3-create-availability-sets"></a>3.可用性セットを作成します。
各ロール (DC/AD FS と WAP) の場合は、2 つのマシンには、少なくともを含む可用性セットを作成します。 これは各ロール用の高可用性の実現に役立ちます。 可用性セットを作成、次のように決定するために不可欠です。

* **障害ドメイン**:同じフォールト ドメイン内の仮想マシンは、同じ電源と物理ネットワーク スイッチを共有します。 2 つの障害ドメインの最小値がお勧めします。 既定値は 3 と、このデプロイはおくことができます。
* **更新ドメイン**:同じ更新ドメインに所属するマシンは、更新中に一緒に再起動されます。 少なくとも 2 つの更新ドメインのします。 既定値は 5 と、このデプロイはおくことができます。

![可用性セット](./media/how-to-connect-fed-azure-adfs/availabilityset1.png)

次の可用性セットを作成します。

| 可用性セット | ロール | 障害ドメイン | 更新ドメイン |
|:---:|:---:|:---:|:--- |
| contosodcset |DC/ADFS |3 |5 |
| contosowapset」と |［WAP］ |3 |5 |

### <a name="4-deploy-virtual-machines"></a>4。バーチャル マシンの展開
次の手順では、インフラストラクチャ内のさまざまな役割をホストする仮想マシンをデプロイします。 各可用性セットには、2 つのマシンの最小値がお勧めします。 基本的な展開の 4 つの仮想マシンを作成します。

| コンピューター | ロール | ［サブネット］ | 可用性セット | ストレージ アカウント | IP アドレス |
|:---:|:---:|:---:|:---:|:---:|:---:|
| contosodc1 |DC/ADFS |INT |contosodcset |contososac1 |スタティック |
| contosodc2 |DC/ADFS |INT |contosodcset |contososac2 |スタティック |
| contosowap1 |［WAP］ |DMZ |contosowapset」と |contososac1 |スタティック |
| contosowap2 |［WAP］ |DMZ |contosowapset」と |contososac2 |スタティック |

お気付きのように NSG が指定されていません。 これは、azure では、サブネット レベルで NSG を使用できるためです。 次に、いずれかのサブネットか NIC オブジェクトに関連付けられている個々 の NSG を使用してマシンのネットワーク トラフィックを制御できます。 詳細を読む[ネットワーク セキュリティ グループ (NSG) は](https://aka.ms/Azure/NSG)します。
DNS を管理している場合は、静的 IP アドレスを使うことをお勧めします。 Azure DNS を使用して、代わりに、ドメインの DNS レコードに対応する Azure Fqdn で新しいマシンを参照してください。
仮想マシン ウィンドウはする必要がありますデプロイが完了したら以下のようになります。

![デプロイされた仮想マシン](./media/how-to-connect-fed-azure-adfs/virtualmachinesdeployed_noadfs.png)

### <a name="5-configuring-the-domain-controller--ad-fs-servers"></a>5。ドメイン コント ローラーの構成/AD FS サーバー
 すべての受信要求を認証するためには、AD FS は、ドメイン コント ローラーに接続する必要があります。 認証のため、オンプレミスの DC に Azure からコストのかかるトリップを保存するには、Azure でドメイン コント ローラーのレプリカをデプロイすることをお勧めします。 高可用性を確保するために、少なくとも 2 つのドメイン コント ローラーの可用性セットを作成することをお勧めします。

| ドメイン コントローラー | ロール | ストレージ アカウント |
|:---:|:---:|:---:|
| contosodc1 |レプリカ |contososac1 |
| contosodc2 |レプリカ |contososac2 |

* 2 つのサーバーを DNS にレプリカ ドメイン コント ローラーとして昇格させる
* サーバー マネージャーを使用して AD FS の役割をインストールすることで、AD FS サーバーを構成します。

### <a name="6-deploying-internal-load-balancer-ilb"></a>6。内部ロード バランサー (ILB) を展開します。
**6.1.ILB を作成します。**

ILB をデプロイには、クリックして Azure portal でロード バランサーを選択は、(+) を追加します。

> [!NOTE]
> 表示されない場合**ロード バランサー** 、メニューの クリックして**参照**スクロール バーが表示されるまで、ポータルの左下にある**ロード バランサー**します。  次に、メニューに追加する黄色の星をクリックします。 これで、ロード バランサーの構成を開始するパネルを開くには、新しいロード バランサー アイコンを選択します。
> 
> 

![ロード バランサーを参照します。](./media/how-to-connect-fed-azure-adfs/browseloadbalancer.png)

* **名前**:ロード バランサーに任意の適切な名前を付ける
* **スキーム**:このロード バランサーは、AD FS サーバーの前に、内部ネットワークの接続のみのためのものですので、「内部」を選択します。
* **仮想ネットワーク**:AD FS を展開している仮想ネットワークを選択します。
* **サブネット**:内部サブネットを選択します。
* **IP アドレスの割り当て**:スタティック

![内部ロード バランサー](./media/how-to-connect-fed-azure-adfs/ilbdeployment1.png)

クリックした後は、作成、ILB が展開されていると、ロード バランサーの一覧に表示されます。

![ILB の後にロード バランサー](./media/how-to-connect-fed-azure-adfs/ilbdeployment2.png)

次の手順では、バックエンド プールとバックエンド プローブを構成します。

**6.2.ILB バックエンド プールを構成します。**

ロード バランサー パネルで、新しく作成した ILB を選択します。 [設定] パネルが開きます。 

1. [設定] パネルからバックエンド プールを選択します。
2. バックエンド プールの追加 パネルで、仮想マシンの追加をクリックします。
3. 可用性セットを選択できるパネルが表示されます。
4. AD FS の可用性セットを選択します。

![ILB バックエンド プールを構成します。](./media/how-to-connect-fed-azure-adfs/ilbdeployment3.png)

**6.3.プローブを構成します。**

ILB の設定 パネルでは、正常性プローブを選択します。

1. 追加します。
2. プローブの詳細を提供します。 **名前**:名前の b をプローブします。 **プロトコル**:HTTP c。 **Port**:80 (HTTP) d。 **パス**: プローブ/adfs/e。 **間隔**:5 (既定値) – これは、ILB が f のバックエンド プール内のマシンをプローブする間隔です。 **異常のしきい値制限**:2 (既定値) – これは、その後 ILB はバックエンド プール内のマシン - 応答のないと宣言トラフィックの送信を停止する連続したプローブ失敗のしきい値です。

![ILB のプローブを構成します。](./media/how-to-connect-fed-azure-adfs/ilbdeployment4.png)

私たちはエンドポイントを使用して/adfs/probe AD FS 環境で正常性チェックを明示的に作成された HTTPS パスを完全に確認が実行できません。  これは、AD FS の展開を最新の状態を正確に反映しないポート 443 の基本的なチェックをよりも大幅に優れています。  詳細については、これをご覧 https://blogs.technet.microsoft.com/applicationproxyblog/2014/10/17/hardware-load-balancer-health-checks-and-web-application-proxy-ad-fs-2012-r2/します。

**6.4.負荷分散規則を作成します。**

トラフィックを効果的に分散するには、するためには、負荷分散規則で ILB を構成する必要があります。 負荷分散規則を作成するには 

1. ILB の設定パネルから負荷分散規則を選択します。
2. [負荷分散規則] パネルで [追加] をクリックします。
3. 追加の負荷分散規則 パネルで、します。 **名前**:ルール b の名前を指定します。 **プロトコル**:TCP。 c を選択します。 **Port**:443 d. **バックエンド ポート**:443 e。 **バックエンド プール**:AD FS は、以前の f をクラスター用に作成したプールを選択します。 **プローブ**:以前に AD FS サーバーの作成、プローブを選択します。

![ILB の分散規則を構成します。](./media/how-to-connect-fed-azure-adfs/ilbdeployment5.png)

**6.5.ILB で DNS を更新します。**

DNS サーバーに移動し、ILB の CNAME を作成します。 CNAME が ILB の IP アドレスを指す IP アドレスを持つフェデレーション サービスのあります。 たとえば ILB の DIP アドレスが 10.3.0.8 であるとき、およびフェデレーション サービスがインストールされている場合は、fs.contoso.com は、10.3.0.8 を指す fs.contoso.com の cname レコードを作成します。
これにより、fs.contoso.com 終了に関するすべての通信が ILB にし、適切にルーティングされます。

### <a name="7-configuring-the-web-application-proxy-server"></a>7.Web アプリケーション プロキシ サーバーを構成します。
**7.1.AD FS サーバーに接続する Web アプリケーション プロキシ サーバーを構成します。**

Web アプリケーション プロキシ サーバーが ILB の背後にある AD FS サーバーに到達できることを確認するには、ilb の場合、%systemroot%\system32\drivers\etc\hosts にレコードを作成します。 識別名 (DN) で、fs.contoso.com などのフェデレーション サービス名があることに注意してください。 ILB の IP アドレス (例では、10.3.0.8) IP エントリになります。

**7.2.Web アプリケーション プロキシの役割のインストール**

Web アプリケーション プロキシ サーバーが ILB の内側の AD FS サーバーに到達できることを確認した後は、Web アプリケーション プロキシ サーバーを次にインストールできます。 Web アプリケーション プロキシ サーバーをドメインに参加していない必要があります。 リモート アクセスの役割を選択して、2 つの Web アプリケーション プロキシ サーバーで Web アプリケーション プロキシ役割をインストールします。 WAP のインストールを完了するには、サーバー マネージャーが説明します。
WAP をデプロイする方法の詳細については、読み取る[をインストールして、Web アプリケーション プロキシ サーバーを構成](https://technet.microsoft.com/library/dn383662.aspx)します。

### <a name="8--deploying-the-internet-facing-public-load-balancer"></a>8.インターネット接続 (パブリック) ロード バランサーを展開します。
**8.1.インターネット接続 (パブリック) ロード バランサーを作成します。**

Azure portal のロード バランサーを選択し、[追加] をクリックします。 作成するロード バランサー パネルで、次の情報を入力します。

1. **名前**:ロード バランサーの名前
2. **スキーム**:公開-このオプションは、このロード バランサーにパブリック アドレスは必要がありますを Azure に指示します。
3. **IP アドレス**:新しい IP アドレスを作成する (動的)

![インターネットに接続するロード バランサー](./media/how-to-connect-fed-azure-adfs/elbdeployment1.png)

展開後、ロード バランサーは、ロード バランサーの一覧に表示されます。

![ロード バランサーの一覧](./media/how-to-connect-fed-azure-adfs/elbdeployment2.png)

**8.2.パブリック IP に DNS ラベルを割り当てる**

構成用のパネルを表示するロード バランサー パネルで、新しく作成したロード バランサーのエントリをクリックします。 以下のパブリック IP の DNS ラベルを構成する手順に従います。

1. パブリック IP アドレスをクリックします。 パブリック IP とその設定のパネルが開きます
2. [構成] をクリックします。
3. DNS ラベルを提供します。 これには、たとえば contosofs.westus.cloudapp.azure.com どこからでもアクセスできるパブリック DNS ラベルになります。 外部ロード バランサー (contosofs.westus.cloudapp.azure.com) の DNS ラベルに解決されるフェデレーション サービス (fs.contoso.com) などの外部の dns エントリを追加することができます。

![インターネットに接続するロード バランサーを構成します。](./media/how-to-connect-fed-azure-adfs/elbdeployment3.png) 

![インターネットに接続するロード バランサー (DNS) を構成します。](./media/how-to-connect-fed-azure-adfs/elbdeployment4.png)

**8.3.インターネット接続 (パブリック) ロード バランサーのバックエンド プールを構成します。** 

WAP サーバーの可用性セットとして、インターネット接続 (パブリック) ロード バランサーのバックエンド プールを構成する、内部ロード バランサーの作成と同じ手順に従います。 たとえば、contosowapset」とします。

![インターネットに接続するロード バランサーのバックエンド プールを構成します。](./media/how-to-connect-fed-azure-adfs/elbdeployment5.png)

**8.4.プローブを構成します。**

WAP サーバーのバックエンド プールのプローブを構成する内部ロード バランサーの構成と同じ手順に従います。

![インターネットに接続するロード バランサーのプローブを構成します。](./media/how-to-connect-fed-azure-adfs/elbdeployment6.png)

**8.5.負荷分散規則を作成します。**

負荷分散、TCP 443 の規則を構成する ILB と同じ手順に従います。

![インターネットに接続するロード バランサーの分散の規則を構成します。](./media/how-to-connect-fed-azure-adfs/elbdeployment7.png)

### <a name="9-securing-the-network"></a>9.ネットワークをセキュリティで保護します。
**9.1.内部サブネットを保護します。**

全体的に見て、次の規則 (以下に記載された順序) で、内部サブネットを効率的にセキュリティで保護する必要があります。

| ルール | 説明 | フロー |
|:--- |:--- |:---:|
| AllowHTTPSFromDMZ |DMZ からの HTTPS 通信を許可します。 |受信 |
| DenyInternetOutbound |インターネットへのアクセスなし |送信 |

![INT へのアクセス ルール (受信)](./media/how-to-connect-fed-azure-adfs/nsg_int.png)

<!--
[comment]: <> (![INT access rules (inbound)](./media/how-to-connect-fed-azure-adfs/nsgintinbound.png))
[comment]: <> (![INT access rules (outbound)](./media/how-to-connect-fed-azure-adfs/nsgintoutbound.png))
-->

**9.2.DMZ サブネットを保護します。**

| ルール | 説明 | フロー |
|:--- |:--- |:---:|
| AllowHTTPSFromInternet |インターネットから DMZ への HTTPS を許可します。 |受信 |
| DenyInternetOutbound |インターネットへの HTTPS を除きすべてブロックされます。 |送信 |

![EXT アクセス ルール (受信)](./media/how-to-connect-fed-azure-adfs/nsg_dmz.png)

<!--
[comment]: <> (![EXT access rules (inbound)](./media/how-to-connect-fed-azure-adfs/nsgdmzinbound.png))
[comment]: <> (![EXT access rules (outbound)](./media/how-to-connect-fed-azure-adfs/nsgdmzoutbound.png))
-->

> [!NOTE]
> クライアント ユーザー証明書認証場合、(X509 を使用し、clientTLS 認証ユーザー証明書) が必要な場合は、AD FS には、TCP が必要がありますの着信アクセスに対するポート 49443 を有効にします。
> 
> 

### <a name="10-test-the-ad-fs-sign-in"></a>10.AD FS サインイン テストします。
最も簡単な方法は、IdpInitiatedSignon.aspx ページを使用して AD FS をテストするのには。 AD FS のプロパティで IdpInitiatedSignOn を有効にする必要があることを実行するにです。 AD FS の設定を確認するのには、次の手順に従います

1. 実行、以下の設定に有効な PowerShell を使用して、AD FS サーバーでコマンドレット。
   Set-adfsproperties EnableIdPInitiatedSignonPage $true 
2. 任意の外部のコンピューターから https へのアクセス:\//adfs-server.contoso.com/adfs/ls/IdpInitiatedSignon.aspx します。  
3. AD FS ページが表示する次のような。

![ログイン ページのテスト](./media/how-to-connect-fed-azure-adfs/test1.png)

成功したサインインにはする旨の成功メッセージを次に示すよう。

![テスト成功](./media/how-to-connect-fed-azure-adfs/test2.png)

## <a name="template-for-deploying-ad-fs-in-azure"></a>Azure での AD FS を展開するためのテンプレート
テンプレートでは、6 つのマシンのセットアップ、ドメイン コント ローラー、AD FS と WAP 2 各デプロイします。

[Azure のデプロイ テンプレートでの AD FS](https://github.com/paulomarquesc/adfs-6vms-regular-template-based)

既存の仮想ネットワークを使用して、このテンプレートをデプロイするときに、新しい VNET を作成したりできます。 展開のカスタマイズ可能なさまざまなパラメーターは、展開プロセスのパラメーターの使用状況の説明を以下に示します。 

| パラメーター | 説明 |
|:--- |:--- |
| Location |米国東部などに、リソースをデプロイするリージョン。 |
| StorageAccountType |作成したストレージ アカウントの種類 |
| VirtualNetworkUsage |新しい仮想ネットワークが作成されますか、既存の使用を示します |
| VirtualNetworkName |仮想ネットワークを作成、既存または新規の両方の仮想ネットワークの使用量に必須の名前 |
| VirtualNetworkResourceGroupName |既存の仮想ネットワークが存在するリソース グループの名前を指定します。 必須のパラメーターになりますこの展開は、既存の仮想ネットワークの ID を検索できるように既存の仮想ネットワークを使用する場合 |
| VirtualNetworkAddressRange |新しい VNET を新しい仮想ネットワークを作成する場合は、必須のアドレス範囲 |
| InternalSubnetName |両方の仮想ネットワークの使用状況オプション (新規または既存) の必須内部サブネットの名前 |
| InternalSubnetAddressRange |必須、ドメイン コント ローラーと ADFS のサーバーが含まれる新しい仮想ネットワークを作成する場合、内部サブネットのアドレス範囲。 |
| DMZSubnetAddressRange |新しい仮想ネットワークを作成する場合の必須 Windows アプリケーション プロキシ サーバーを含む dmz サブネットのアドレス範囲。 |
| DMZSubnetName |両方の仮想ネットワークの使用状況オプション (新規または既存) の必須内部サブネットの名前。 |
| ADDC01NICIPAddress |最初のドメイン コント ローラーの内部 IP アドレス、この IP アドレスは、DC に静的に割り当てられるし、内部サブネット内の有効な ip アドレスである必要があります。 |
| ADDC02NICIPAddress |2 番目のドメイン コント ローラーの内部 IP アドレス、この IP アドレスは、DC に静的に割り当てられるし、内部サブネット内の有効な ip アドレスである必要があります。 |
| ADFS01NICIPAddress |最初の ADFS サーバーの内部 IP アドレス、この IP アドレスは、ADFS サーバーに静的に割り当てられるし、内部サブネット内の有効な ip アドレスである必要があります。 |
| ADFS02NICIPAddress |2 番目の ADFS サーバーの内部 IP アドレス、この IP アドレスは、ADFS サーバーに静的に割り当てられるし、内部サブネット内の有効な ip アドレスである必要があります。 |
| WAP01NICIPAddress |最初の WAP サーバーの内部 IP アドレス、この IP アドレスは、WAP サーバーに静的に割り当てられるし、DMZ サブネット内で有効な ip アドレスである必要があります。 |
| WAP02NICIPAddress |2 番目の WAP サーバーの内部 IP アドレス、この IP アドレスは、WAP サーバーに静的に割り当てられるし、DMZ サブネット内で有効な ip アドレスである必要があります。 |
| ADFSLoadBalancerPrivateIPAddress |ADFS ロード バランサーの内部 IP アドレス、この IP アドレスはロード バランサーに静的に割り当てられるし、内部サブネット内の有効な ip アドレスである必要があります。 |
| ADDCVMNamePrefix |ドメイン コント ローラーの仮想マシン名のプレフィックス |
| ADFSVMNamePrefix |Ad FS サーバーの仮想マシン名のプレフィックス |
| WAPVMNamePrefix |WAP サーバーの仮想マシン名のプレフィックス |
| ADDCVMSize |ドメイン コント ローラーの vm サイズ |
| ADFSVMSize |Ad FS サーバーの vm サイズ |
| WAPVMSize |WAP サーバーの vm サイズ |
| AdminUserName |仮想マシンのローカル管理者の名前 |
| adminPassword |仮想マシンのローカル管理者アカウントのパスワード |

## <a name="additional-resources"></a>その他の資料
* [可用性セット](https://aka.ms/Azure/Availability) 
* [Azure Load Balancer](https://aka.ms/Azure/ILB)
* [内部ロード バランサー](https://aka.ms/Azure/ILB/Internal)
* [インターネット接続するロード バランサー](https://aka.ms/Azure/ILB/Internet)
* [ストレージ アカウント](https://aka.ms/Azure/Storage)
* [Azure 仮想ネットワーク](https://aka.ms/Azure/VNet)
* [AD FS と Web アプリケーション プロキシのリンク](https://aka.ms/ADFSLinks) 

## <a name="next-steps"></a>次のステップ
* [オンプレミス id と Azure Active Directory の統合](https://docs.microsoft.com/azure/active-directory/hybrid/whatis-hybrid-identity)
* [構成と Azure AD Connect を使用して、AD FS の管理](/azure/active-directory/hybrid/how-to-connect-fed-whatis)
* [Azure Traffic Manager での高可用性地域間 AD FS のデプロイ](active-directory-adfs-in-azure-with-azure-traffic-manager.md)
