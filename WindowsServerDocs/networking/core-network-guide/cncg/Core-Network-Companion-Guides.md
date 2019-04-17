---
title: コア ネットワーク必携ガイド
description: このトピックで説明する Windows Server 2016 コア ネットワーク ガイドの必携ガイドの概要
manager: brianlic
ms.technology: networking
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: d57af0bd-9301-4f62-9888-f528cd10451d
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3c272c51cc69017b75e50e79e58186c0ea7c6391
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="core-network-companion-guides"></a>コア ネットワーク必携ガイド

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

Windows Server 2016 の中に[コア ネットワーク ガイド](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide)新しい Active Directory を展開する方法を説明しています&reg;フォレスト ルート ドメインを新しいとサポートするネットワーク インフラストラクチャ、必携ガイドをネットワークに機能を追加することが提供します。

各必携ガイドでは、コア ネットワークを展開した後、特定の目標を達成することができます。 場合によっては、し、正しい順序で一緒に展開するときに、複数の必携ガイドがある使用する測定に基づく、コスト効果の高い、妥当な方法で非常に複雑な目標を達成できます。

コア ネットワーク ガイドを入手する前に、Active Directory ドメインとコア ネットワークを展開した場合でも、ネットワークに機能を追加する、必携ガイドを使用することができます。 前提条件のリストとして、コア ネットワーク ガイドを使用し、必携ガイドで追加機能を展開するネットワーク必要がありますを満たしている、コア ネットワーク ガイドが提供するための前提条件がわかっているだけです。

## <a name="core-network-companion-guide-deploy-server-certificates-for-8021x-wired-and-wireless-deployments"></a>コア ネットワーク必携ガイド: 802.1 X 有線および無線展開用のサーバー証明書を展開します。 

この必携ガイドでは、ネットワーク ポリシー サーバー \(NPS\)、リモート アクセス サービス \(RAS\)、またはその両方を実行しているコンピューターのサーバー証明書を展開することにより、コア ネットワーク上で構築する方法について説明します。

ネットワーク アクセスの認証 Extensible Authentication Protocol \(EAP\) と保護された EAP \(PEAP\) 証明書ベースの認証方法を展開するときに、サーバー証明書が必要です。 Active Directory 証明書サービスとサーバーの証明書の展開 \(AD CS\) EAP および PEAP 証明書ベースの認証方法については、次の利点を提供します。

- 秘密キーに、NPS または RAS サーバーの id をバインドします。
- ドメイン メンバーの NPS と RAS サーバーに証明書を自動的に登録するためのコスト効率に優れ、セキュリティで保護されたメソッド
- 証明書と証明機関を管理するため、効率的な方法
- 証明書ベースの認証で提供されるセキュリティ
- 他の目的で証明書の使用を拡張する機能
  
サーバー証明書を展開する方法に関する手順については、次を参照してください。 [802.1 X ワイヤードおよびワイヤレス展開用のサーバー証明書の展開](server-certs/Deploy-Server-Certificates-for-802.1X-Wired-and-Wireless-Deployments.md)します。  
## <a name="core-network-companion-guide-deploy-password-based-8021x-authenticated-wireless-access"></a>コア ネットワーク必携ガイド: パスワード ベース 802.1 X 認証ワイヤレス アクセスの展開します。

この必携ガイド Institute の Electrical and Electronics Engineers \(IEEE\) 802.1X\ を展開する方法についての指示を提供することにより、コア ネットワーク上で構築する方法について説明-Protected Extensible Authentication Protocol\ – Microsoft チャレンジ ハンドシェイク認証プロトコル バージョン 2 を使用して IEEE 802.11 ワイヤレス アクセスの認証 \ (PEAP\ MS\-CHAP v2\)。

PEAP\-MS\--ms-chap V 2 の認証方法には、サーバーを実行しているネットワーク ポリシー サーバー \(NPS\) 存在ワイヤレス クライアントをクライアントに NPS サーバーの id を証明するためにサーバー証明書の認証、ただし、証明書を使用してユーザーの認証は実行されません - ユーザーが自分のドメイン ユーザー名とパスワードを提供する代わりに、必要があります。

PEAP\-MS\--ms-chap V 2 は、ユーザーが認証プロセス中に、証明書ではなく、パスワード ベースの資格情報を提供することを必要とするため、通常より簡単かつ EAP\ TLS または PEAP\ TLS よりも展開する安価です。

このガイドを使用して PEAP\ MS\-CHAP v2 認証方法とワイヤレス アクセスを展開する前に、次の操作を行う必要があります。

1. コア ネットワークのインフラストラクチャを展開する、コア ネットワーク ガイドで指示に従うか、既にがテクノロジ ガイドで説明する、ネットワーク上に展開します。
2. 指示に従って、コア ネットワーク必携ガイド展開サーバーの証明書での 802.1 X ワイヤードおよびワイヤレス展開では、または既にがテクノロジ ガイドで説明する、ネットワーク上に展開します。

CHAP MS\ PEAP\ v2 のワイヤレス アクセスを展開する方法に関する手順については、次を参照してください。[展開パスワード ベース 802.1 X 認証ワイヤレス アクセス](wireless/a-deploy-8021X-wireless-access.md)します。

## <a name="core-network-companion-guide-deploy-branchcache-hosted-cache-mode"></a>コア ネットワーク必携ガイド: BranchCache ホスト型キャッシュ モードを展開します。

この必携ガイドでは、1 つまたは複数のブランチ オフィスにホスト型キャッシュ モードで BranchCache を展開する方法について説明します。

BranchCache は、一部のエディション、Windows Server 2016 および Windows 10 オペレーティング システム、および以前のバージョンの Windows および Windows Server に含まれているワイド エリア ネットワーク (WAN) 帯域幅最適化テクノロジです。

ホスト型キャッシュ モードで BranchCache を展開するときに、ブランチ オフィスのコンテンツ キャッシュがいずれかでホストされているかと呼ばれる、複数のサーバー コンピューターにホスト型キャッシュ サーバー。 ホスト型キャッシュ サーバーは、キャッシュは、ブランチ オフィス内の複数の目的で、サーバーを使用することができますをホストしているだけでなく、ワークロードを実行できます。

BranchCache ホスト型キャッシュ モードは、最初に要求およびデータをキャッシュするクライアントがオフラインの場合でも、コンテンツが利用可能なために、キャッシュの効率を向上します。 ホスト型キャッシュ サーバーにため、常に利用可能なより多くのコンテンツがキャッシュされ、WAN 帯域幅を大幅に削減するには、提供して、BranchCache の効率が向上します。

ホスト型キャッシュ モードを展開するときに、複数のサブネットのブランチ オフィス内のすべてのクライアントは、クライアントが異なるサブネット上にある場合でも、ホスト型キャッシュ サーバーに格納されている 1 つのキャッシュにアクセスできます。

ホスト型キャッシュ モードで BranchCache を展開する方法に関する手順については、次を参照してください。 [BranchCache ホスト型キャッシュ モードの展開](bc-hcm/1-Deploy-Bc-Hcm.md)します。
