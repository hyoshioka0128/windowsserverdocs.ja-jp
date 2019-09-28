---
title: コア ネットワーク必携ガイド
description: このトピックでは、Windows Server 2016 コアネットワークガイドの概要について説明します。
manager: brianlic
ms.technology: networking
ms.prod: windows-server
ms.topic: article
ms.assetid: d57af0bd-9301-4f62-9888-f528cd10451d
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c0895cfd62d462ef6d158dc39ef59a9ee10a7c98
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406309"
---
# <a name="core-network-companion-guidance"></a>コア ネットワーク必携ガイド

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

Windows Server 2016[コアネットワークガイド](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide)では、新しいルートドメインとサポートするネットワークインフラストラクチャを使用して新しい Active Directory @ no__t フォレストを展開する方法について説明していますが、必携ガイドでは、ネットワークの機能。

各必携ガイドにより、コア ネットワークの展開後に特定の目標を達成することができます。 場合によっては複数の必携ガイドが存在することもあります。これらを正しい順序で一緒に展開することで、非常に複雑な目標を、正確に定められた、コスト効果の高い合理的な方法で達成することができます。

コア ネットワーク ガイドを入手する前に Active Directory ドメインとコア ネットワークを展開した場合でも、必携ガイドを使用してネットワークに機能を追加できます。 コア ネットワーク ガイドを単に前提条件の一覧として使用し、必携ガイドで追加機能を展開する場合、ネットワークがコア ネットワーク ガイドで指定されている前提条件を満たしている必要があります。

## <a name="core-network-companion-guide-deploy-server-certificates-for-8021x-wired-and-wireless-deployments"></a>コア ネットワーク必携ガイド:802.1 X 有線および無線展開のサーバー証明書を展開する 

この必携ガイドでは、ネットワークポリシーサーバーを実行しているコンピューターのサーバー証明書を展開することによってコアネットワーク上で構築する方法について説明します \(NPS @ no__t、リモートアクセスサービス \(RAS @ no__t、またはその両方。

サーバー証明書は、拡張認証プロトコルを使用して証明書ベースの認証方法を展開する場合に必要です。これには、ネットワークアクセス認証用の拡張認証プロトコル @no__t 0EAP @ no__t と保護された EAP \(PEAP @ no__t-3 が必要です。 Active Directory 証明書サービスを使用してサーバー証明書を展開する \(AD CS @ no__t-1 EAP と PEAP 証明書ベースの認証方法には、次の利点があります。

- NPS または RAS サーバーの id を秘密キーにバインドする
- ドメインメンバー NPS と RAS サーバーに証明書を自動的に登録するための、コスト効率に優れた安全な方法
- 証明書および証明機関の効率的な管理
- 証明書ベースの認証によるセキュリティ
- 追加の目的のための、証明書の用途拡張
  
サーバー証明書を展開する方法の手順については、「 [802.1 x ワイヤード (有線) およびワイヤレス展開用のサーバー証明書の展開](server-certs/Deploy-Server-Certificates-for-802.1X-Wired-and-Wireless-Deployments.md)」を参照してください。  
## <a name="core-network-companion-guide-deploy-password-based-8021x-authenticated-wireless-access"></a>コア ネットワーク必携ガイド:パスワード ベース 802.1X 認証ワイヤレス アクセスの展開

この必携ガイドでは、@no__t 国立 IEEE @ no__t-1 802.1 X @ no__t-2authenticated を使用して IEEE 802.11 ワイヤレスアクセスを保護する方法について説明し、コアネットワーク上で構築する方法について説明します。拡張認証プロトコル \ – Microsoft チャレンジハンドシェイク認証プロトコルバージョン 2 \(PEAP @ no__t-4MS @ no__t-5CHAP v2 @ no__t-6。

認証方法 PEAP @ no__t-0MS @ no__t-1CHAP v2 では、ネットワークポリシー @no__t サーバーを実行しているサーバーを認証する必要があります。-2NPS @ no__t は、クライアントに対して NPS id を証明するために、サーバー証明書を持つワイヤレスクライアントを提供します。認証は証明書を使用して実行されません。代わりに、ユーザーはドメインユーザー名とパスワードを入力します。

PEAP @ no__t-0MS @ no__t-1CHAP v2 では、認証プロセス中にユーザーが証明書ではなくパスワードベースの資格情報を提供する必要があるため、通常、EAP @ no__t-2TLS または PEAP @ no__t-3TLS よりも簡単かつ低コストで展開できます。

このガイドを使用して、PEAP @ no__t-0MS @ no__t-1CHAP v2 の認証方法を使用してワイヤレスアクセスを展開する前に、次の操作を行う必要があります。

1. コアネットワークガイドに記載されている手順に従って、コアネットワークインフラストラクチャを展開するか、またはそのガイドに示されているテクノロジをネットワーク上に展開します。
2. コアネットワークコンパニオンガイドの手順に従って、802.1 X ワイヤードおよびワイヤレス展開用のサーバー証明書を展開します。または、このガイドに示されているテクノロジをネットワークに展開済みであることを示します。

PEAP @ no__t-0MS @ no__t-1CHAP v2 を使用してワイヤレスアクセスを展開する方法については、「[パスワードベースの 802.1 x で認証](wireless/a-deploy-8021X-wireless-access.md)されたワイヤレスアクセスを展開する」を参照してください。

## <a name="core-network-companion-guide-deploy-branchcache-hosted-cache-mode"></a>コア ネットワーク必携ガイド:BranchCache ホスト型キャッシュ モードを展開する

この必携ガイドでは、BranchCache をホスト型キャッシュモードで1つまたは複数のブランチオフィスに展開する方法について説明します。

BranchCache は、Windows Server 2016 および Windows 10 オペレーティングシステムの一部のエディション、および以前のバージョンの Windows および Windows Server に含まれているワイドエリアネットワーク (WAN) 帯域幅最適化テクノロジです。

ホスト型キャッシュ モードで BranchCache を展開すると、ブランチ オフィスのコンテンツ キャッシュは 1 台以上のサーバー コンピューターでホストされます。このようなサーバー コンピューターは、ホスト型キャッシュ サーバーと呼ばれます。 ホスト型キャッシュサーバーは、キャッシュをホストするだけでなく、ブランチオフィスで複数の目的でサーバーを使用できるようにすることで、ワークロードを実行できます。

BranchCache ホスト型キャッシュモードでは、データを最初に要求およびキャッシュしたクライアントがオフラインであってもコンテンツを利用できるため、キャッシュ効率が向上します。 ホスト型キャッシュ サーバーは常に利用できるため、より多くのコンテンツがキャッシュされます。その結果、より多くの WAN 帯域幅が節約され、BranchCache の効率が向上します。

ホスト型キャッシュモードを展開すると、複数サブネットのブランチオフィスにあるすべてのクライアントが1つのキャッシュにアクセスできます。このキャッシュは、クライアントが異なるサブネットにある場合でも、ホスト型キャッシュサーバーに格納されます。

ホスト型キャッシュモードで BranchCache を展開する方法については、「 [Branchcache ホスト型キャッシュモードの展開](bc-hcm/1-Deploy-Bc-Hcm.md)」を参照してください。
