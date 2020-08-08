---
title: サーバー証明書の展開の概要
description: このトピックでは、802.1 X ワイヤードおよびワイヤレス展開の証明書をサーバーのデプロイ ガイドの一部
manager: brianlic
ms.topic: article
ms.assetid: ca5c3e04-ae25-4590-97f3-0376a9c2a9a2
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 318bab675cc633034731e369b5da2bbb40d810b0
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87949416"
---
# <a name="server-certificate-deployment-overview"></a>サーバー証明書の展開の概要

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックは、次のセクションで構成されています。

-   [サーバー証明書展開コンポーネント](#bkmk_components)

-   [サーバー証明書の展開プロセスの概要](#bkmk_process)

## <a name="server-certificate-deployment-components"></a><a name="bkmk_components"></a>サーバー証明書展開コンポーネント
このガイドを使用すると、エンタープライズ ルート証明機関 (CA) として Active Directory 証明書サービス (AD CS) をインストールしてネットワーク ポリシー サーバー (NPS)、ルーティングとリモート アクセス サービス (RRAS)、または NPS および RRAS の両方を実行しているサーバーにサーバー証明書を登録することができます。


SDN 証明書ベースの認証を展開すると、サーバーがセキュリティで保護された通信をどのように達成できるように、他のサーバーに自分の身元を証明するためにサーバー証明書を使用する必要があります。

次の図は、SDN インフラストラクチャのサーバーにサーバー証明書を展開するために必要なコンポーネントを示しています。

![サーバー証明書の展開の必要なインフラストラクチャ](../../../media/Nps-Certs/Nps-Certs.jpg)

> [!NOTE]
> 上の図では、複数のサーバーの表示: DC1、CA1、WEB1、および多くの SDN サーバーです。 CA1 および WEB1 を展開および構成との DC1 に、このガイドでは、ネットワークに既にインストールするいると仮定の構成手順を説明します。 Active Directory ドメインをすでにインストールしない場合、これを行うを使用して、 [コア ネットワーク ガイド](https://technet.microsoft.com/library/mt604042.aspx) Windows Server 2016 用です。

上の図に示すように各項目の詳細については、次を参照してください。

-   [CA1](#bkmk_ca1)

-   [WEB1](#bkmk_web1)

-   [DC1](#bkmk_dc1)

-   [NPS1](#bkmk_nps1)

### <a name="ca1-running-the-ad-cs-server-role"></a><a name="bkmk_ca1"></a>CA1 AD CS サーバー役割を実行しています。
このシナリオでは、エンタープライズ ルート証明機関 (CA) と、発行元 CA ではまたです。 CA は、証明書を登録する適切なセキュリティ権限を持つサーバー コンピューターに証明書を発行します。 Active Directory 証明書サービス (AD CS) は、CA1 にインストールされます。

大規模なネットワークまたはセキュリティに関する注意事項が根拠は、ルート CA と発行元 CA の役割を分離し、ca は下位の Ca を展開できます。

最も安全な展開では、オフラインであり、物理的に安全なエンタープライズ ルート CA が少なくなります。

#### <a name="capolicyinf"></a>CAPolicy.inf
AD CS をインストールする前に、固有の設定で、展開の CAPolicy.inf ファイルを構成します。

#### <a name="copy-of-the-ras-and-ias-servers-certificate-template"></a>コピー、 **RAS および IAS サーバー** 証明書テンプレート
1 つのコピーを作成するサーバー証明書を展開するときに、 **RAS および IAS サーバー** 証明書のテンプレートと、このガイドで、要件と表示される指示に従って、テンプレートを構成します。

元のテンプレートではなく、テンプレートのコピーを利用するは、考えられる将来使用するため、元のテンプレートの構成が保持されるようにします。 コピーを構成する、 **RAS および IAS サーバー** テンプレート Active Directory ユーザーと指定したコンピューターのグループに作成するため、CA サーバーの証明書を発行します。

#### <a name="additional-ca1-configuration"></a>CA1 に追加の構成
CA は、識別の証拠としてそれらに提示される証明書が有効な証明書であることを確認し、失効していないコンピューターを確認する必要があります証明書失効リスト (CRL) を公開します。 コンピューターは、認証プロセス中に、CRL を検索する場所を知ることは、CRL の正しい場所を CA を構成する必要があります。

### <a name="web1-running-the-web-services-iis-server-role"></a><a name="bkmk_web1"></a>WEB1 Web サービス (IIS) サーバーの役割を実行しています。
WEB1 で、Web サーバー (IIS) サーバーの役割を実行しているコンピューターで CRL と AIA の場所として使用するため、Windows エクスプ ローラーでフォルダーを作成する必要があります。

#### <a name="virtual-directory-for-the-crl-and-aia"></a>CRL と AIA の仮想ディレクトリ
Windows エクスプ ローラーでフォルダーを作成した後は、インターネット インフォメーション サービス (IIS) マネージャーだけでなく、仮想ディレクトリのアクセス制御リストを構成するコンピューターを許可するようが公開された後、AIA と CRL にアクセスする仮想ディレクトリとしてフォルダーを構成する必要があります。

### <a name="dc1-running-the-ad-ds-and-dns-server-roles"></a><a name="bkmk_dc1"></a>DC1 AD DS および DNS サーバーの役割を実行しています。
DC1 は、ドメイン コント ローラーで、ネットワーク上の DNS サーバーです。

#### <a name="group-policy-default-domain-policy"></a>ポリシーの既定のドメイン ポリシーをグループ化します。
CA で証明書テンプレートを構成した後は、証明書は、NPS と RAS サーバーに登録できるように、グループ ポリシーの既定のドメイン ポリシーを構成できます。 グループ ポリシーは、DC1 のサーバーで AD DS で構成されます。

#### <a name="dns-alias-cname-resource-record"></a>DNS エイリアス (CNAME) リソース レコード
その他のコンピュータが、サーバーだけでなく、AIA と、サーバーに格納されている CRL を検出できることを確認する Web サーバーのエイリアス (CNAME) リソース レコードを作成する必要があります。 Web および FTP サイトをホストしているなどの他の目的の Web サーバーを使用できるように、柔軟性がさらに、提供エイリアス CNAME リソース レコードを使用します。

### <a name="nps1-running-the-network-policy-server-role-service-of-the-network-policy-and-access-services-server-role"></a><a name="bkmk_nps1"></a>NPS1 ネットワーク ポリシーとアクセス サービス サーバー ロールのネットワーク ポリシー サーバーの役割サービスを実行します。
NPS は、Windows Server 2016 コアネットワークガイドのタスクを実行するときにインストールされるため、このガイドのタスクを実行する前に、ネットワークに1つ以上の NPSs がインストールされている必要があります。

#### <a name="group-policy-applied-and-certificate-enrolled-to-servers"></a>グループ ポリシーが適用され、サーバーに証明書の登録
証明書テンプレートおよび自動登録を構成した後は、すべてのターゲット サーバーのグループ ポリシーを更新できます。 この時点では、サーバーは、CA1 からサーバー証明書を登録します。

### <a name="server-certificate-deployment-process-overview"></a><a name="bkmk_process"></a>サーバー証明書の展開プロセスの概要

> [!NOTE]
> 次の手順を実行する方法の詳細については、セクションで説明します。 [サーバー証明書の展開](../../../core-network-guide/cncg/server-certs/Server-Certificate-Deployment.md)します。

サーバー証明書の登録を構成するプロセスは、これらの各段階で発生します。

1.  WEB1 で、Web サーバー (IIS) の役割をインストールします。

2.  DC1 で、WEB1、Web サーバーのエイリアス (CNAME) レコードを作成します。

3.  CA、CRL をホストし、CRL を公開し、エンタープライズ ルート CA 証明書を新しい仮想ディレクトリにコピーするように Web サーバーを構成します。

4.  AD CS のインストールを計画しているコンピューターで、コンピュータに静的 IP アドレスを割り当てます、コンピューターの名前、コンピューターをドメインに参加し、Domain Admins と Enterprise Admins グループのメンバーであるユーザー アカウントでコンピューターにログオンします。

5.  AD CS のインストールを計画しているコンピューターで、展開に固有の設定で CAPolicy.inf ファイルを構成します。

6.  AD CS サーバー役割をインストールし、CA の追加の構成を実行します。

7.  CA1 から CRL と CA 証明書を WEB1 Web サーバー上の共有にコピーします。

8.  Ca で、RAS および IAS サーバー証明書テンプレートのコピーを構成します。 CA は、CA が証明書を発行する前に、サーバー証明書テンプレートを構成する必要がありますので、証明書テンプレートに基づいて証明書を発行します。

9.  グループ ポリシーでは、サーバー証明書の自動登録を構成します。 自動登録を構成するときに、自動的に Active Directory グループのメンバーシップを持つ指定したすべてのサーバーは、各サーバー上のグループ ポリシーが更新されたときにサーバー証明書を受信します。 後でより多くのサーバーを追加する場合は自動的に付けサーバーの証明書すぎます。

10. サーバーのグループ ポリシーを更新します。 グループ ポリシーが更新されたときに、サーバーは、前の手順で構成されているテンプレートに基づくサーバー証明書を受信します。 この証明書は、認証プロセス中にクライアント コンピューターに身元を証明するために、サーバーとその他のサーバーで使用されます。

    > [!NOTE]
    > すべてのドメイン メンバー コンピューターは、自動登録の構成を使用せず、エンタープライズ ルート CA の証明書を自動的に受け取ります。 この証明書は、サーバー証明書を構成し、自動登録を使用して、配布よりも異なります。 この CA によって発行される証明書は信頼できるように、すべてのドメイン メンバー コンピューターの信頼されたルート証明機関の証明書ストアに CA の証明書が自動的にインストールします。

10. すべてのサーバーが有効なサーバー証明書を登録したことを確認します。



