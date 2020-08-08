---
title: 802.1 X 有線および無線展開のサーバー証明書を展開する
description: このトピックでは、802.1 X ワイヤードおよびワイヤレス展開の証明書をサーバーのデプロイ ガイドの一部
manager: brianlic
ms.topic: article
ms.assetid: 0a39ecae-39cc-4f26-bd6f-b71ed02fc4ad
ms.author: lizross
author: eross-msft
ms.openlocfilehash: fd5c9ea9954053fd21f6ab46ff0b6d2f8da5245f
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87995567"
---
# <a name="deploy-server-certificates-for-8021x-wired-and-wireless-deployments"></a>802.1 X 有線および無線展開のサーバー証明書を展開する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このガイドを使用して、リモートアクセスおよびネットワークポリシーサーバー (NPS) インフラストラクチャサーバーにサーバー証明書を展開することができます。

このガイドは次のセクションで構成されます。

-   [このガイドを使用するための前提条件](#bkmk_pre)

-   [このガイドで説明されていないもの](#bkmk_not)

-   [テクノロジの概要](#bkmk_tech)

-   [サーバー証明書の展開の概要](Server-Certificate-Deployment-Overview.md)

-   [サーバー証明書の展開計画](Server-Certificate-Deployment-Planning.md)

-   [サーバー証明書の展開](Server-Certificate-Deployment.md)

### <a name="digital-server-certificates"></a>**デジタルサーバー証明書**
このガイドでは、Active Directory 証明書サービス (AD CS) を使用して、リモートアクセスおよび NPS インフラストラクチャサーバーに証明書を自動的に登録する方法について説明します。 AD CS を使用すると、公開キー基盤 (PKI) を構築し、公開キーの暗号化、デジタル証明書、およびデジタル署名機能を組織に提供できます。

ネットワーク上のコンピューター間の認証にデジタルサーバー証明書を使用すると、証明書によって次のことが実現されます。

1. 暗号化による機密性
2. デジタル署名による整合性。
3. コンピューターネットワーク上のコンピューター、ユーザー、またはデバイスアカウントに証明書キーを関連付けることによる認証。

### <a name="server-types"></a>**サーバーの種類**
このガイドを使用すると、次の種類のサーバーにサーバー証明書を展開できます。
- リモートアクセスサービスを実行しているサーバー。 DirectAccess または標準の仮想プライベートネットワーク (VPN) サーバーで、 **RAS および IAS サーバー**グループのメンバーである。
- **RAS および IAS サーバー**グループのメンバーであるネットワークポリシーサーバー (NPS) サービスを実行しているサーバー。

### <a name="advantages-of-certificate-autoenrollment"></a>**証明書の自動登録の利点**
サーバー証明書の自動登録 (自動登録とも呼ばれます) には、次のような利点があります。

- AD CS 証明機関 (CA) は、すべての NPS およびリモートアクセスサーバーにサーバー証明書を自動的に登録します。
- ドメイン内のすべてのコンピューターは、すべてのドメインメンバーコンピューターの信頼されたルート証明機関ストアにインストールされている CA 証明書を自動的に受信します。 このため、ドメイン内のすべてのコンピューターは、CA によって発行された証明書を信頼します。 この信頼により、認証サーバーは、相互に id を証明し、セキュリティで保護された通信を行うことができます。
- グループポリシーの更新以外に、すべてのサーバーを手動で再構成する必要はありません。
- すべてのサーバー証明書には、サーバー認証の目的と、拡張キー使用法 (EKU) の拡張機能でのクライアント認証の目的が含まれています。
- スケーラビリティ。 このガイドを使用してエンタープライズルート CA を展開した後、エンタープライズの下位 Ca を追加することで公開キー基盤 (PKI) を拡張できます。
- 管理の容易さ。 Ad cs を管理するには、AD CS コンソールを使用するか、Windows PowerShell のコマンドとスクリプトを使用します。
- 簡単さ。 Active Directory グループアカウントとグループメンバーシップを使用して、サーバー証明書を登録するサーバーを指定します。
- サーバー証明書を展開する場合、証明書は、このガイドの手順に従って構成したテンプレートに基づいています。 つまり、特定の種類のサーバーに対して異なる証明書テンプレートをカスタマイズすることも、発行するすべてのサーバー証明書に同じテンプレートを使用することもできます。

## <a name="prerequisites-for-using-this-guide"></a><a name="bkmk_pre"></a>このガイドを使用するための前提条件

このガイドでは、Windows Server 2016 で AD CS と Web サーバー (IIS) サーバーの役割を使用してサーバー証明書を展開する方法について説明します。 このガイドの手順を実行するための前提条件を次に示します。

- コアネットワークは、Windows Server 2016 コアネットワークガイドを使用して展開する必要があります。または、コアネットワークガイドで提供されているテクノロジがネットワーク上に正しくインストールされ、機能している必要があります。 これらのテクノロジには、TCP/IP v4、DHCP、Active Directory Domain Services (AD DS)、DNS、NPS などがあります。
  >[!NOTE]
  >Windows Server 2016 コアネットワークガイドは、Windows Server 2016 テクニカルライブラリから入手できます。 詳細については、「[コアネットワークガイド](../../../core-network-guide/Core-Network-Guide.md)」を参照してください。

- 展開を実行する前に、このガイドの「計画」セクションを読んで、この展開の準備ができていることを確認する必要があります。
- このガイドの手順は、表示されている順序で実行する必要があります。 サーバーを展開する手順を実行せずに CA を展開したり、展開が失敗したりすることはありません。
- ネットワーク上に2台の新しいサーバーを展開する必要があります。1台はエンタープライズルート CA として AD CS をインストールし、もう1台は Web サーバー (IIS) をインストールするサーバーで、CA が証明書失効リスト (CRL) を Web サーバーに発行できるようにするためです。

>[!NOTE]
>このガイドでデプロイする Web および AD CS サーバーに静的 IP アドレスを割り当てる準備ができています。また、組織の名前付け規則に従ってコンピューターの名前を指定することもできます。 さらに、コンピューターをドメインに参加させる必要があります。

## <a name="what-this-guide-does-not-provide"></a><a name="bkmk_not"></a>このガイドで説明されていないもの
このガイドでは、AD CS を使用して公開キー基盤 (PKI) を設計および展開するための包括的な手順については説明しません。 このガイドでは、テクノロジを展開する前に、AD CS のドキュメントと PKI の設計に関するドキュメントを参照することをお勧めします。

## <a name="technology-overviews"></a><a name="bkmk_tech"></a>テクノロジの概要
AD CS と Web サーバー (IIS) のテクノロジの概要を次に示します。

### <a name="active-directory-certificate-services"></a>Active Directory 証明書サービス
Windows Server 2016 の AD CS は、公開キーテクノロジを採用するソフトウェアセキュリティシステムで使用される x.509 証明書を作成および管理するためのカスタマイズ可能なサービスを提供します。 組織は、AD CS を使用して、個人、デバイス、またはサービスの id を対応する公開キーにバインドすることにより、セキュリティを強化することができます。 AD CS には、さまざまなスケーラブルな環境で証明書の登録と失効を管理できる機能も含まれています。

詳細については、「 [Active Directory 証明書サービスの概要](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831740(v=ws.11))」および「[公開キー基盤の設計ガイダンス](https://techcommunity.microsoft.com/t5/ask-the-directory-services-team/designing-and-implementing-a-pki-part-i-design-and-planning/ba-p/396953)」を参照してください。

### <a name="web-server-iis"></a>Web サーバー (IIS)

Windows Server 2016 の Web サーバー (IIS) の役割は、web サイト、サービス、およびアプリケーションを確実にホストするための、セキュリティで保護された、管理しやすい、モジュール型の拡張可能なプラットフォームを提供します。 IIS では、インターネット、イントラネットまたはエクストラネット上のユーザーと情報を共有できます。 IIS は、IIS、ASP.NET、FTP サービス、PHP、および Windows Communication Foundation (WCF) を一体化した統合 web プラットフォームです。

詳細については、「 [Web サーバー (IIS) の概要](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831725(v=ws.11))」を参照してください。