---
title: Azure での Active Directory フェデレーションサービス (AD FS) |Microsoft Docs
description: このドキュメントでは、高可用性のために AD FS を Azure にデプロイする方法について説明します。
author: billmath
manager: mtillman
ms.assetid: 692a188c-badc-44aa-ba86-71c0e8074510
ms.topic: get-started-article
ms.date: 10/28/2018
ms.subservice: hybrid
ms.author: billmath
ms.openlocfilehash: 5701e7955a3baff248c0f7efc0b1de03088a8aa0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854955"
---
# <a name="deploying-active-directory-federation-services-in-azure"></a>Azure での Active Directory フェデレーションサービス (AD FS) のデプロイ
AD FS は、簡素化され、セキュリティで保護された id フェデレーションと Web シングルサインオン (SSO) 機能を提供します。 Azure AD または O365 とのフェデレーションにより、ユーザーはオンプレミスの資格情報を使用して認証を行い、クラウド内のすべてのリソースにアクセスできます。 その結果、オンプレミスとクラウドの両方のリソースにアクセスできるようにするために、高可用性 AD FS インフラストラクチャを確保することが重要になります。 Azure に AD FS をデプロイすると、最小限の労力で必要な高可用性を実現するのに役立ちます。
Azure に AD FS をデプロイすると、いくつかの利点があります。その一部を以下に示します。

* **高可用性**-Azure 可用性セットの機能により、可用性の高いインフラストラクチャを確保できます。
* **拡張性の**向上-より高いパフォーマンスが必要ですか? Azure で数回クリックするだけで、より強力なマシンに簡単に移行できます
* **Geo 冗長性**-Azure Geo 冗長性により、インフラストラクチャが世界中で高可用性を実現していることを保証できます。
* **管理が容易**– Azure portal での管理オプションが非常にシンプルになっているため、インフラストラクチャの管理は非常に簡単で労力が不要です。 

## <a name="design-principles"></a>設計原則
![配置の設計](./media/how-to-connect-fed-azure-adfs/deployment.png)

上の図は、Azure での AD FS インフラストラクチャのデプロイを開始するために推奨される基本的なトポロジを示しています。 トポロジのさまざまなコンポーネントの背後にある原則を次に示します。

* **DC/ADFS サーバー**: ユーザーが1000未満の場合は、AD FS の役割をドメインコントローラーにインストールするだけで済みます。 ドメインコントローラーのパフォーマンスに影響がない場合、または1000を超えるユーザーがいる場合は、AD FS を別のサーバーに展開します。
* **WAP サーバー** – Web アプリケーションプロキシサーバーを展開する必要があります。これにより、ユーザーが会社のネットワーク上にいないときに AD FS に接続できるようになります。
* **Dmz**: Web アプリケーションプロキシサーバーは dmz に配置され、dmz と内部サブネット間の TCP/443 アクセスのみが許可されます。
* **ロードバランサー**: AD FS と Web アプリケーションプロキシサーバーの高可用性を確保するために、AD FS サーバーには内部ロードバランサーを使用し、Web アプリケーションプロキシサーバーには Azure Load Balancer を使用することをお勧めします。
* **可用性セット**: AD FS のデプロイに冗長性を持たせるために、2つ以上の仮想マシンを、同じようなワークロードの可用性セットにグループ化することをお勧めします。 この構成により、計画済みまたは計画外のメンテナンスイベント中に、少なくとも1つの仮想マシンを使用できるようになります。
* **ストレージアカウント**: 2 つのストレージアカウントを用意することをお勧めします。 1つのストレージアカウントを持っていると、単一障害点の作成につながる可能性があります。ストレージアカウントがダウンした場合でも、デプロイが使用できなくなる可能性があります。 2つのストレージアカウントを使用すると、障害行ごとに1つのストレージアカウントを関連付けることができます。
* **ネットワークの分離**: Web アプリケーションプロキシサーバーは、別の DMZ ネットワークに展開する必要があります。 1つの仮想ネットワークを2つのサブネットに分割してから、分離されたサブネットに Web アプリケーションプロキシサーバーを展開することができます。 各サブネットに対してネットワークセキュリティグループの設定を構成し、2つのサブネット間で必要な通信のみを許可することができます。 詳細については、以下のデプロイシナリオごとに提供されます。

## <a name="steps-to-deploy-ad-fs-in-azure"></a>Azure で AD FS をデプロイする手順
このセクションで説明する手順では、以下の AD FS インフラストラクチャを Azure にデプロイするためのガイドの概要を示します。

### <a name="1-deploying-the-network"></a>1. ネットワークを展開する
既に説明したように、1つの仮想ネットワークに2つのサブネットを作成するか、まったく異なる2つの仮想ネットワーク (VNet) を作成することができます。 この記事では、単一の仮想ネットワークをデプロイし、それを2つのサブネットに分割する方法に焦点を当てます。 これは、2つの個別の Vnet が通信に VNet 間ゲートウェイを必要とするため、現在はより簡単な方法です。

**1.1 仮想ネットワークの作成**

![仮想ネットワークの作成](./media/how-to-connect-fed-azure-adfs/deploynetwork1.png)

Azure portal で 仮想ネットワーク を選択すると、1回のクリックで仮想ネットワークとサブネットをすぐにデプロイできます。 INT サブネットも定義され、Vm を追加する準備ができました。
次の手順では、ネットワークに別のサブネット (DMZ サブネットなど) を追加します。 DMZ サブネットを作成するには、単に

* 新しく作成したネットワークを選択します
* [プロパティ] で、[サブネット] を選択します。
* サブネットパネルで、[追加] ボタンをクリックします。
* サブネットを作成するためのサブネットの名前とアドレス空間の情報を指定します。

![［サブネット］](./media/how-to-connect-fed-azure-adfs/deploynetwork2.png)

![サブネット DMZ](./media/how-to-connect-fed-azure-adfs/deploynetwork3.png)

**1.2. ネットワークセキュリティグループを作成しています**

ネットワークセキュリティグループ (NSG) には、Virtual Network 内の VM インスタンスへのネットワークトラフィックを許可または拒否する Access Control リスト (ACL) 規則の一覧が含まれています。 NSGs は、サブネットまたはそのサブネット内の個々の VM インスタンスに関連付けることができます。 NSG がサブネットに関連付けられている場合、ACL ルールはそのサブネット内のすべての VM インスタンスに適用されます。
このガイダンスでは、内部ネットワークと DMZ 用にそれぞれ1つずつ、2つの NSGs を作成します。 これらのラベルは、それぞれ NSG_INT と NSG_DMZ として表示されます。

![NSG の作成](./media/how-to-connect-fed-azure-adfs/creatensg1.png)

NSG が作成されると、0個の受信と0の送信ルールが作成されます。 各サーバーの役割がインストールされ、機能したら、必要なセキュリティレベルに応じて受信および送信の規則を作成できます。

![NSG の初期化](./media/how-to-connect-fed-azure-adfs/nsgint1.png)

NSGs を作成した後、NSG_INT をサブネット INT に、NSG_DMZ をサブネット DMZ に関連付けます。 スクリーンショットの例を次に示します。

![NSG の構成](./media/how-to-connect-fed-azure-adfs/nsgconfigure1.png)

* [サブネット] をクリックして、サブネットのパネルを開きます。
* NSG に関連付けるサブネットを選択します 

構成後は、サブネットのパネルは次のようになります。

![NSG 後のサブネット](./media/how-to-connect-fed-azure-adfs/nsgconfigure2.png)

**1.3. オンプレミスへの接続を作成します**

Azure にドメインコントローラー (DC) をデプロイするには、オンプレミスに接続する必要があります。 Azure には、オンプレミスのインフラストラクチャを Azure インフラストラクチャに接続するためのさまざまな接続オプションが用意されています。

* ポイント対サイト
* サイト対サイトの Virtual Network
* ExpressRoute

ExpressRoute を使用することをお勧めします。 ExpressRoute を使用すると、Azure データセンターと、お客様のオンプレミスまたはコロケーション環境にあるインフラストラクチャとの間にプライベート接続を作成できます。 ExpressRoute 接続は、パブリックインターネットを経由しません。 インターネット経由の一般的な接続よりも信頼性が高く、より高速で待機時間が少なく、セキュリティも強化されています。
ExpressRoute を使用することをお勧めしますが、組織に最適な任意の接続方法を選択できます。 Expressroute と、expressroute を使用したさまざまな接続オプションの詳細については、「 [expressroute の技術概要」](https://aka.ms/Azure/ExpressRoute)を参照してください。

### <a name="2-create-storage-accounts"></a>2. ストレージアカウントを作成する
高可用性を維持し、1つのストレージアカウントへの依存を回避するために、2つのストレージアカウントを作成できます。 各可用性セット内のマシンを2つのグループに分割し、各グループに個別のストレージアカウントを割り当てます。

![ストレージアカウントの作成](./media/how-to-connect-fed-azure-adfs/storageaccount1.png)

### <a name="3-create-availability-sets"></a>3. 可用性セットを作成する
各ロール (DC/AD FS と WAP) に対して、少なくとも2台のマシンを含む可用性セットを作成します。 これにより、各ロールの可用性を高めることができます。 可用性セットの作成時には、次のことを決定することが不可欠です。

* **障害ドメイン**: 同じ障害ドメイン内の仮想マシンは、同じ電源と物理ネットワークスイッチを共有します。 少なくとも2つの障害ドメインをお勧めします。 既定値は3で、この配置のためにそのままにすることができます。
* **更新ドメイン**: 同じ更新ドメインに属するマシンは、更新中に一緒に再起動されます。 少なくとも2つの更新ドメインが必要です。 既定値は5で、この配置のためにそのままにすることができます。

![可用性セット](./media/how-to-connect-fed-azure-adfs/availabilityset1.png)

次の可用性セットを作成します。

| 可用性セット | 役割 | 障害ドメイン | 更新ドメイン |
|:---:|:---:|:---:|:--- |
| contosodcset |DC/ADFS |3 |5 |
| contosowapset |［WAP］ |3 |5 |

### <a name="4-deploy-virtual-machines"></a>4. 仮想マシンを展開する
次の手順では、インフラストラクチャ内のさまざまな役割をホストする仮想マシンを展開します。 各可用性セットには、少なくとも2台のコンピューターを使用することをお勧めします。 基本的なデプロイ用に4つの仮想マシンを作成します。

| Machine | 役割 | ［サブネット］ | 可用性セット | ストレージアカウント | IP アドレス |
|:---:|:---:|:---:|:---:|:---:|:---:|
| contosodc1 |DC/ADFS |INT |contosodcset |contososac1 |静的 |
| contosodc2 |DC/ADFS |INT |contosodcset |contososac2 |静的 |
| contosowap1 |［WAP］ |DMZ |contosowapset |contososac1 |静的 |
| contosowap2 |［WAP］ |DMZ |contosowapset |contososac2 |静的 |

ご存知かもしれませんが、NSG は指定されていません。 これは、azure では、サブネットレベルで NSG を使用できるためです。 次に、サブネットまたは NIC オブジェクトに関連付けられた個々の NSG を使用して、マシンのネットワークトラフィックを制御できます。 詳細について[は、「ネットワークセキュリティグループ (NSG) とは](https://aka.ms/Azure/NSG)」を参照してください。
DNS を管理する場合は、静的 IP アドレスを使用することをお勧めします。 ドメインの DNS レコードでは、Azure DNS を使用できます。その場合は、Azure Fqdn で新しいマシンを参照してください。
デプロイの完了後、仮想マシンのウィンドウは次のようになります。

![Virtual Machines 展開済み](./media/how-to-connect-fed-azure-adfs/virtualmachinesdeployed_noadfs.png)

### <a name="5-configuring-the-domain-controller--ad-fs-servers"></a>5. ドメインコントローラー/AD FS サーバーを構成する
 受信要求を認証するには、AD FS がドメインコントローラーに接続する必要があります。 Azure からオンプレミスの DC に対する認証にかかるコストを削減するには、ドメインコントローラーのレプリカを Azure にデプロイすることをお勧めします。 高可用性を実現するために、少なくとも2つのドメインコントローラーの可用性セットを作成することをお勧めします。

| ドメイン コントローラー | 役割 | ストレージアカウント |
|:---:|:---:|:---:|
| contosodc1 |レプリカ |contososac1 |
| contosodc2 |レプリカ |contososac2 |

* 2つのサーバーをレプリカドメインコントローラーとして DNS に昇格する
* サーバーマネージャーを使用して AD FS の役割をインストールして、AD FS サーバーを構成します。

### <a name="6-deploying-internal-load-balancer-ilb"></a>6. 内部 Load Balancer (ILB) を展開する
**6.1. ILB を作成する**

ILB をデプロイするには、Azure portal で [ロードバランサー] を選択し、[追加] (+) をクリックします。

> [!NOTE]
> メニューに **[ロードバランサー]** が表示されない場合は、ポータルの左下にある **[参照]** をクリックし、 **[ロードバランサー]** が表示されるまでスクロールします。  次に、黄色い星をクリックしてメニューに追加します。 次に、[新しいロードバランサー] アイコンを選択してパネルを開き、ロードバランサーの構成を開始します。
> 
> 

![ロードバランサーの参照](./media/how-to-connect-fed-azure-adfs/browseloadbalancer.png)

* **名前**: ロードバランサーに適切な名前を付けます。
* **スキーム**: このロードバランサーは AD FS サーバーの前に配置され、内部ネットワーク接続のみを目的としているため、[内部] を選択します。
* **Virtual Network**: AD FS をデプロイする仮想ネットワークを選択します
* **[サブネット]** : ここで内部サブネットを選択します。
* **IP アドレスの割り当て**: 静的

![内部ロードバランサー](./media/how-to-connect-fed-azure-adfs/ilbdeployment1.png)

[作成] をクリックすると、ILB がデプロイされ、ロードバランサーの一覧に表示されます。

![ILB の後のロードバランサー](./media/how-to-connect-fed-azure-adfs/ilbdeployment2.png)

次の手順では、バックエンドプールとバックエンドプローブを構成します。

**6.2. ILB バックエンドプールを構成する**

[ロードバランサー] パネルで新しく作成した ILB を選択します。 [設定] パネルが開きます。 

1. [設定] パネルから [バックエンドプール] を選択します。
2. [バックエンドプールの追加] パネルで、[仮想マシンの追加] をクリックします。
3. [可用性セット] を選択できるパネルが表示されます。
4. AD FS 可用性セットの選択

![ILB バックエンドプールの構成](./media/how-to-connect-fed-azure-adfs/ilbdeployment3.png)

**6.3. プローブを構成しています**

ILB 設定パネルで、[正常性プローブ] を選択します。

1. [追加] をクリック
2. プローブ a の詳細を指定します。 **名前**: プローブ名 b。 **プロトコル**: HTTP c。 **ポート**:80 (HTTP) d。 **パス**:/adfs/probe e。 **間隔**: 5 (既定値) –これは、ilb がバックエンドプール f 内のマシンをプローブする間隔です。 [**異常しきい**値の制限]: 2 (既定値) –これはプローブの連続エラーのしきい値です。この値を超えると、ilb はバックエンドプール内のマシンを応答不能として宣言し、トラフィックの送信を停止します。

![ILB プローブの構成](./media/how-to-connect-fed-azure-adfs/ilbdeployment4.png)

AD FS 環境で正常性チェック用に明示的に作成された/adfs/probe エンドポイントを使用しています。このエンドポイントでは、完全な HTTPS パスチェックを実行できません。  これは、最新の AD FS 展開の状態を正確に反映していない、基本的なポート443のチェックよりも大幅に優れています。  詳細については、 https://blogs.technet.microsoft.com/applicationproxyblog/2014/10/17/hardware-load-balancer-health-checks-and-web-application-proxy-ad-fs-2012-r2/を参照してください。

**6.4. 負荷分散規則を作成する**

トラフィックのバランスを効果的に取るために、ILB に負荷分散規則を構成する必要があります。 負荷分散規則を作成するには、 

1. ILB の [設定] パネルで [負荷分散規則] を選択します。
2. [負荷分散規則] パネルの [追加] をクリックします。
3. [負荷分散規則の追加] パネルで、 **名前**: ルール b の名前を指定します。 **プロトコル**: [TCP c] を選択します。 **ポート**: 443 d。 **バックエンドポート**: 443 e。 **[バックエンドプール]** : AD FS クラスター用に作成したプールを選択します。 **プローブ**: AD FS サーバー用に作成されたプローブを選択します

![ILB の分散規則の構成](./media/how-to-connect-fed-azure-adfs/ilbdeployment5.png)

**6.5. ILB を使用して DNS を更新する**

DNS サーバーにアクセスし、ILB の CNAME を作成します。 CNAME は、ILB の IP アドレスを指す IP アドレスを持つフェデレーションサービス用である必要があります。 たとえば、ILB DIP アドレスが10.3.0.8 で、インストールされているフェデレーションサービスが fs.contoso.com の場合は、10.3.0.8 を指す fs.contoso.com の CNAME を作成します。
これにより、fs.contoso.com に関するすべての通信が ILB で終了し、適切にルーティングされるようになります。

### <a name="7-configuring-the-web-application-proxy-server"></a>7. Web アプリケーションプロキシサーバーを構成する
**7.1 AD FS サーバーに接続するように Web アプリケーションプロキシサーバーを構成する**

Web アプリケーションプロキシサーバーが ILB の背後にある AD FS サーバーに確実に接続できるようにするには、ILB の%systemroot%\system32\drivers\etc\hosts にレコードを作成します。 識別名 (DN) はフェデレーションサービス名であることに注意してください (例: fs.contoso.com)。 また、IP エントリは ILB の IP アドレス (例では 10.3.0.8) のものである必要があります。

**7.2. Web アプリケーションプロキシの役割をインストールしています**

Web アプリケーションプロキシサーバーが ILB の背後にある AD FS サーバーに接続できることを確認したら、次に Web アプリケーションプロキシサーバーをインストールできます。 Web アプリケーションプロキシサーバーはドメインに参加していない必要があります。 リモートアクセスの役割を選択して、2つの Web アプリケーションプロキシサーバーに Web アプリケーションプロキシの役割をインストールします。 サーバーマネージャーで、WAP のインストールを完了するように指示されます。
WAP をデプロイする方法の詳細については、「 [Web アプリケーションプロキシサーバーのインストールと構成](https://technet.microsoft.com/library/dn383662.aspx)」を参照してください。

### <a name="8--deploying-the-internet-facing-public-load-balancer"></a>8. インターネットに接続する (パブリック) Load Balancer を展開する
**8.1. インターネットに接続された (パブリック) Load Balancer を作成する**

Azure portal で、ロードバランサー を選択し、追加 をクリックします。 [ロードバランサーの作成] パネルで、次の情報を入力します。

1. **名前**: ロードバランサーの名前
2. **Scheme**: public-このオプションは、このロードバランサーにパブリックアドレスが必要であることを Azure に指示します。
3. **Ip アドレス**: 新しい ip アドレス (動的) を作成します。

![インターネットに接続するロードバランサー](./media/how-to-connect-fed-azure-adfs/elbdeployment1.png)

展開後、ロードバランサーが [ロードバランサー] の一覧に表示されます。

![ロードバランサーの一覧](./media/how-to-connect-fed-azure-adfs/elbdeployment2.png)

**8.2. パブリック IP に DNS ラベルを割り当てる**

[ロードバランサー] パネルで新しく作成したロードバランサーエントリをクリックして、構成のパネルを表示します。 パブリック IP の DNS ラベルを構成するには、次の手順に従います。

1. パブリック IP アドレスをクリックします。 パブリック IP とその設定のパネルが開きます。
2. [構成] をクリックします。
3. DNS ラベルを指定します。 これは、contosofs.westus.cloudapp.azure.com など、どこからでもアクセスできるパブリック DNS ラベルになります。 外部のロードバランサー (contosofs.westus.cloudapp.azure.com) の DNS ラベルに解決されるフェデレーションサービス (fs.contoso.com など) の外部 DNS にエントリを追加できます。

![インターネットに接続するロードバランサーを構成する](./media/how-to-connect-fed-azure-adfs/elbdeployment3.png) 

![インターネットに接続するロードバランサー (DNS) を構成する](./media/how-to-connect-fed-azure-adfs/elbdeployment4.png)

**8.3. インターネットに接続している (パブリック) Load Balancer のバックエンドプールを構成する** 

内部ロードバランサーの作成と同じ手順に従い、インターネットに接続する (パブリック) Load Balancer のバックエンドプールを WAP サーバーの可用性セットとして構成します。 たとえば、contosowapset のようになります。

![インターネットに接続している Load Balancer のバックエンドプールを構成する](./media/how-to-connect-fed-azure-adfs/elbdeployment5.png)

**8.4. プローブを構成する**

内部ロードバランサーの構成と同じ手順に従って、WAP サーバーのバックエンドプールのプローブを構成します。

![インターネットに接続する Load Balancer のプローブを構成する](./media/how-to-connect-fed-azure-adfs/elbdeployment6.png)

**8.5. 負荷分散規則を作成します**

ILB の場合と同じ手順に従って、TCP 443 の負荷分散規則を構成します。

![インターネットに接続する Load Balancer の分散規則を構成する](./media/how-to-connect-fed-azure-adfs/elbdeployment7.png)

### <a name="9-securing-the-network"></a>9. ネットワークをセキュリティで保護する
**9.1. 内部サブネットをセキュリティで保護する**

全体として、次の規則に従って内部サブネットを効率的にセキュリティで保護する必要があります (以下に記載されている順序で)。

| ルール | 説明 | [フロー] |
|:--- |:--- |:---:|
| AllowHTTPSFromDMZ |DMZ からの HTTPS 通信を許可する |受信 |
| DenyInternetOutbound |インターネットにアクセスできない |送信 |

![INT アクセスルール (受信)](./media/how-to-connect-fed-azure-adfs/nsg_int.png)

**9.2. DMZ サブネットをセキュリティで保護する**

| ルール | 説明 | [フロー] |
|:--- |:--- |:---:|
| AllowHTTPSFromInternet |インターネットから DMZ への HTTPS を許可する |受信 |
| DenyInternetOutbound |インターネットに対する HTTPS 以外のすべてがブロックされる |送信 |

![EXT アクセス規則 (受信)](./media/how-to-connect-fed-azure-adfs/nsg_dmz.png)

> [!NOTE]
> クライアントユーザー証明書認証 (X509 ユーザー証明書を使用した clientTLS 認証) が必要な場合、AD FS は、受信アクセスに対して TCP ポート49443を有効にする必要があります。
> 
> 

### <a name="10-test-the-ad-fs-sign-in"></a>10. AD FS サインインをテストする
最も簡単な方法は、IdpInitiatedSignon オン .aspx ページを使用して AD FS をテストすることです。 これを可能にするには、AD FS プロパティで IdpInitiatedSignOn オンを有効にする必要があります。 AD FS のセットアップを確認するには、次の手順に従います。

1. PowerShell を使用して、AD FS サーバーで次のコマンドレットを実行し、[有効] に設定します。
   Set-adfsproperties-EnableIdPInitiatedSignonPage $true 
2. 任意の外部コンピューターから、https:\//adfs-server.contoso.com/adfs/ls/IdpInitiatedSignon.aspx にアクセスします。  
3. 次のような AD FS ページが表示されます。

![ログインのテストページ](./media/how-to-connect-fed-azure-adfs/test1.png)

サインインに成功すると、次のように成功メッセージが表示されます。

![テストの成功](./media/how-to-connect-fed-azure-adfs/test2.png)

## <a name="template-for-deploying-ad-fs-in-azure"></a>Azure で AD FS をデプロイするためのテンプレート
このテンプレートでは、6つのコンピューターセットアップ (ドメインコントローラー、AD FS と WAP) が展開されます。

[Azure デプロイテンプレートでの AD FS](https://github.com/paulomarquesc/adfs-6vms-regular-template-based)

このテンプレートのデプロイ中に、既存の仮想ネットワークを使用することも、新しい VNET を作成することもできます。 デプロイのカスタマイズに使用できるさまざまなパラメーターを次に示します。デプロイプロセスでのパラメーターの使用方法について説明します。 

| パラメーター | 説明 |
|:--- |:--- |
| 場所 |リソースをデプロイするリージョン (例: 米国東部)。 |
| StorageAccountType |作成されたストレージアカウントの種類 |
| VirtualNetworkUsage |新しい仮想ネットワークを作成するか、既存のものを使用するかを示します |
| VirtualNetworkName |作成する Virtual Network の名前 (既存または新規の両方の仮想ネットワークの使用時に必須) |
| VirtualNetworkResourceGroupName |既存の仮想ネットワークが存在するリソースグループの名前を指定します。 既存の仮想ネットワークを使用する場合は、デプロイが既存の仮想ネットワークの ID を見つけることができるように、これは必須のパラメーターになります。 |
| VirtualNetworkAddressRange |新しい VNET のアドレス範囲 (新しい仮想ネットワークを作成する場合は必須) |
| Internalサブネット名 |内部サブネットの名前。仮想ネットワークの使用オプション (新規または既存) の両方で必須です。 |
| Internalサブネット Addressrange |ドメインコントローラーと ADFS サーバーを含む内部サブネットのアドレス範囲 (新しい仮想ネットワークを作成する場合は必須)。 |
| Dmzサブネットの Addressrange |Windows アプリケーションプロキシサーバーを含む dmz サブネットのアドレス範囲 (新しい仮想ネットワークを作成する場合は必須)。 |
| Dmzサブネット名 |内部サブネットの名前。仮想ネットワークの使用オプション (新規または既存) の両方で必須です。 |
| ADDC01NICIPAddress |最初のドメインコントローラーの内部 IP アドレス。この IP アドレスは、DC に静的に割り当てられ、内部サブネット内の有効な ip アドレスである必要があります。 |
| ADDC02NICIPAddress |2番目のドメインコントローラーの内部 IP アドレス。この IP アドレスは、DC に静的に割り当てられ、内部サブネット内の有効な ip アドレスである必要があります。 |
| ADFS01NICIPAddress |最初の ADFS サーバーの内部 IP アドレス。この IP アドレスは、ADFS サーバーに静的に割り当てられ、内部サブネット内の有効な ip アドレスである必要があります。 |
| ADFS02NICIPAddress |2番目の ADFS サーバーの内部 IP アドレス。この IP アドレスは、ADFS サーバーに静的に割り当てられ、内部サブネット内の有効な ip アドレスである必要があります。 |
| WAP01NICIPAddress |最初の WAP サーバーの内部 IP アドレス。この IP アドレスは、WAP サーバーに静的に割り当てられ、DMZ サブネット内の有効な ip アドレスである必要があります。 |
| WAP02NICIPAddress |2番目の WAP サーバーの内部 IP アドレス。この IP アドレスは、WAP サーバーに静的に割り当てられ、DMZ サブネット内の有効な ip アドレスである必要があります。 |
| ADFSLoadBalancerPrivateIPAddress |ADFS ロードバランサーの内部 IP アドレス。この IP アドレスは、ロードバランサーに静的に割り当てられ、内部サブネット内の有効な ip アドレスである必要があります。 |
| ADDCVMNamePrefix |ドメインコントローラーの仮想マシン名のプレフィックス |
| ADFSVMNamePrefix |ADFS サーバーの仮想マシン名のプレフィックス |
| WAPVMNamePrefix |WAP サーバーの仮想マシン名のプレフィックス |
| ADDCVMSize |ドメインコントローラーの vm サイズ |
| ADFSVMSize |ADFS サーバーの vm サイズ |
| WAPVMSize |WAP サーバーの vm サイズ |
| AdminUserName |仮想マシンのローカル管理者の名前 |
| AdminPassword |仮想マシンのローカル管理者アカウントのパスワード |

## <a name="additional-resources"></a>その他のリソース
* [可用性セット](https://aka.ms/Azure/Availability) 
* [Azure Load Balancer](https://aka.ms/Azure/ILB)
* [内部 Load Balancer](https://aka.ms/Azure/ILB/Internal)
* [インターネットに接続する Load Balancer](https://aka.ms/Azure/ILB/Internet)
* [ストレージアカウント](https://aka.ms/Azure/Storage)
* [Azure 仮想ネットワーク](https://aka.ms/Azure/VNet)
* [AD FS と Web アプリケーションプロキシのリンク](https://aka.ms/ADFSLinks) 

## <a name="next-steps"></a>次のステップ:
* [オンプレミス id と Azure Active Directory の統合](https://docs.microsoft.com/azure/active-directory/hybrid/whatis-hybrid-identity)
* [Azure AD Connect を使用した AD FS の構成と管理](/azure/active-directory/hybrid/how-to-connect-fed-whatis)
* [Azure Traffic Manager を使用した Azure への高可用性の地理的な AD FS デプロイ](active-directory-adfs-in-azure-with-azure-traffic-manager.md)
