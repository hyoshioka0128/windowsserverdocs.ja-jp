---
title: コア ネットワーク必携ガイド
description: このトピックでは、Windows Server 2016 コア ネットワーク ガイドの必携ガイドの概要を示します
manager: brianlic
ms.technology: networking
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: d57af0bd-9301-4f62-9888-f528cd10451d
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b757e1914ee263a041f39e9767d3cb8af38403dc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816803"
---
# <a name="core-network-companion-guidance"></a>コア ネットワーク必携ガイド

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

Windows Server 2016 の while[コア ネットワーク ガイド](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide)は新しい Active Directory をデプロイする方法について説明&reg;フォレスト ルート ドメインを新しいと、サポートするネットワーク インフラストラクチャ、必携ガイドを提供します。ネットワークに機能を追加することができます。

各必携ガイドにより、コア ネットワークの展開後に特定の目標を達成することができます。 場合によっては複数の必携ガイドが存在することもあります。これらを正しい順序で一緒に展開することで、非常に複雑な目標を、正確に定められた、コスト効果の高い合理的な方法で達成することができます。

コア ネットワーク ガイドを入手する前に Active Directory ドメインとコア ネットワークを展開した場合でも、必携ガイドを使用してネットワークに機能を追加できます。 コア ネットワーク ガイドを単に前提条件の一覧として使用し、必携ガイドで追加機能を展開する場合、ネットワークがコア ネットワーク ガイドで指定されている前提条件を満たしている必要があります。

## <a name="core-network-companion-guide-deploy-server-certificates-for-8021x-wired-and-wireless-deployments"></a>コア ネットワーク必携ガイド:802.1 X 有線および無線展開のサーバー証明書を展開する 

この必携ガイドは、ネットワーク ポリシー サーバーを実行しているコンピューターのサーバー証明書をデプロイして、コア ネットワークを構築する方法を説明します。 \(NPS\)、リモート アクセス サービス\(RAS\)、またはその両方です。

拡張認証プロトコルでの証明書ベースの認証方法を展開するときにサーバー証明書が必要な\(EAP\)と保護された EAP \(PEAP\)ネットワーク アクセスの認証。 Active Directory 証明書サービスのサーバー証明書の展開\(AD CS\) EAP および PEAP 証明書ベースの認証メソッドは、次の利点を提供します。

- 秘密キーへの NPS または RAS サーバーの id のバインド
- ドメイン メンバーの NPS と RAS サーバーに証明書を自動的に登録するためのコスト効率の高い、セキュリティで保護されたメソッド
- 証明書および証明機関の効率的な管理
- 証明書ベースの認証によるセキュリティ
- 追加の目的のための、証明書の用途拡張
  
サーバー証明書を展開する方法については、次を参照してください。 [802.1 X ワイヤードおよびワイヤレス展開用のサーバー証明書の展開](server-certs/Deploy-Server-Certificates-for-802.1X-Wired-and-Wireless-Deployments.md)します。  
## <a name="core-network-companion-guide-deploy-password-based-8021x-authenticated-wireless-access"></a>コア ネットワーク必携ガイド:パスワード ベース 802.1X 認証ワイヤレス アクセスの展開

この必携ガイド Institute の Electrical and Electronics Engineers をデプロイする方法に関する指示を提供することで、コア ネットワークを構築する方法を説明する\(IEEE\) 802.1 X\-IEEE 802.11 ワイヤレス認証保護されている拡張可能な認証 Protocol\ – Microsoft チャレンジ ハンドシェイク認証プロトコル バージョン 2 を使用してアクセス\(PEAP\-MS\-CHAP v2\)します。

PEAP の認証方法\-MS\-CHAP v2 では、その認証が必要ですネットワーク ポリシー サーバーを実行しているサーバー \(NPS\)ワイヤレス クライアントに、NPS の id を証明するためにサーバー証明書を提示します。クライアント - 証明書を使用してユーザー認証が実行されませんが、代わりに、ユーザー提供、ドメイン ユーザー名とパスワード。

ため、PEAP\-MS\-CHAP v2 は、ユーザー、認証プロセス中の証明書ではなくパスワード ベースの資格情報の提供を通常簡単かつ安価に EAP よりもデプロイが必要です\-TLS または PEAP。\-TLS です。

このガイドを使用して、PEAP を使用したワイヤレス アクセスを展開する前に\-MS\-CHAP v2 認証方法 で、次を実行する必要があります。

1. コア ネットワーク インフラストラクチャを展開する、コア ネットワーク ガイドで指示に従うか、既にがテクノロジ ガイドで紹介する、ネットワーク上に展開します。
2. 802.1 X ワイヤードおよびワイヤレス展開では、コア ネットワーク必携ガイド展開サーバーの証明書の手順に従います。 または既にがテクノロジ ガイドで紹介する、ネットワーク上に展開します。

PEAP とワイヤレス アクセスを展開する方法の詳細について\-MS\-CHAP v2 は、「[デプロイ パスワード ベース 802.1 X 認証ワイヤレス アクセス](wireless/a-deploy-8021X-wireless-access.md)します。

## <a name="core-network-companion-guide-deploy-branchcache-hosted-cache-mode"></a>コア ネットワーク必携ガイド:BranchCache ホスト型キャッシュ モードを展開する

この必携ガイドでは、1 つまたは複数のブランチ オフィスでホスト型キャッシュ モードで BranchCache を展開する方法について説明します。

BranchCache は、以前のバージョンの Windows および Windows Server、Windows Server 2016 および Windows 10 オペレーティング システムの一部のエディションに組み込まれているワイド エリア ネットワーク (WAN) 帯域幅最適化テクノロジです。

ホスト型キャッシュ モードで BranchCache を展開すると、ブランチ オフィスのコンテンツ キャッシュは 1 台以上のサーバー コンピューターでホストされます。このようなサーバー コンピューターは、ホスト型キャッシュ サーバーと呼ばれます。 ホスト型キャッシュ サーバーは、ブランチ オフィス内の複数の目的のサーバーを使用することができるキャッシュをホストしているだけでなくワークロードを実行できます。

BranchCache ホスト型キャッシュ モードは、最初に要求およびデータのキャッシュをクライアントがオフラインの場合でも、コンテンツが利用可能なために、キャッシュの効率を向上します。 ホスト型キャッシュ サーバーは常に利用できるため、より多くのコンテンツがキャッシュされます。その結果、より多くの WAN 帯域幅が節約され、BranchCache の効率が向上します。

ホスト型キャッシュ モードを展開するときに複数のサブネットのブランチ オフィス内のすべてのクライアントは、クライアントが異なるサブネット上にある場合でも、ホスト型キャッシュ サーバーに格納されている 1 つのキャッシュにアクセスできます。

ホスト型キャッシュ モードで BranchCache を展開する方法の詳細については、次を参照してください。 [BranchCache ホスト型キャッシュ モードの展開](bc-hcm/1-Deploy-Bc-Hcm.md)します。
