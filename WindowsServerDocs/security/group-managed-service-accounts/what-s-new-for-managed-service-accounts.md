---
title: What's New for Managed Service Accounts
description: Windows Server のセキュリティ
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-gmsa
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2f2a8b6b-c152-4c40-b712-bfabff0e408b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: cac55d04a40c84ce160eb3883d6095a7db0ef3be
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872183"
---
# <a name="what39s-new-for-managed-service-accounts"></a>どのような&#39;s 管理されたサービス アカウントの新機能

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

IT プロフェッショナル向けのこのトピックで機能について説明します、変更管理されたサービス アカウント グループの Windows Server 2012 と Windows 8 では、管理されたサービス アカウント (gMSA) の導入に伴いします。

管理されたサービス アカウントは、Windows サービスや IIS アプリケーション プールなど、独自のドメイン アカウントを共有するサービスとタスクを提供できるように設計されたものです。管理者にとっては、これらのアカウントのパスワードを手動で管理する必要がなくなります。 管理されたサービス アカウントは、パスワードの自動管理が可能な管理されたドメイン アカウントです。

## <a name="versions"></a>Windows Server 2012 と Windows 8 における管理されたサービス アカウントは新機能
Windows Server 2012 および Windows 8 における msa の機能には、どのような変更が行われたを次に示します。

### <a name="group-managed-service-accounts"></a>グループ管理サービス アカウント
ドメイン アカウントがドメイン内のサーバーに対して構成されている場合、クライアント コンピューターは、そのサービスに対して認証を行い、接続できます。 これまでは、パスワードを管理しなくても ID が提供されたアカウントは 2 種類だけで、 次のような制限もありました。

-   コンピューター アカウントは、1 つのドメイン サーバーに制限され、パスワードはコンピューターによって管理される

-   管理されたサービス アカウントは、1 つのドメイン サーバーに制限され、パスワードはコンピューターによって管理される

これらのアカウントを複数のシステムで共有することはできません。 したがって、パスワードの有効期限が切れるのを防ぐために、各システムのサービスごとにアカウントを維持する作業が定期的に発生します。

**この変更の利点**

グループ管理サービス アカウントは、アカウントのパスワードが Windows Server 2012 ドメイン コント ローラーによって管理され、複数の Windows Server 2012 のシステムを取得できるため、この問題を解決します。 Windows でこれらのアカウントのパスワード管理を処理できるようになるため、サービス アカウントの管理にかかわるオーバーヘッドが最小限に抑えられます。

**動作の相違点**

コンピューターで Windows Server 2012 または Windows 8、MSA を作成および管理されるサービス コントロール マネージャーから、サービスの多数のインスタンスなど、サーバー ファーム経由で展開できるようにグループを実行してから管理できる 1 つのサーバー。 管理されたサービス アカウントの管理に使用していたツールとユーティリティ (IIS アプリケーション プール マネージャーなど) は、グループの管理されたサービス アカウントにも使用できます。 ドメイン管理者は、サービスの管理をサービス管理者に委任できます。サービス管理者は、管理されたサービス アカウントまたはグループの管理されたサービス アカウントのライフサイクル全体を管理できます。 既存のクライアント コンピューターは、認証先のサービス インスタンスを把握しなくても、こうしたサービスに対して認証を実行できるようになります。

### <a name="interoperability"></a>削除または非推奨の機能
Windows Server 2012 で、サーバーの管理されたサービス アカウントではなくグループ管理サービス アカウントを管理する Windows PowerShell コマンドレットの既定値。

## <a name="see-also"></a>関連項目

-   [グループ管理サービス アカウントの概要](group-managed-service-accounts-overview.md)

-   [Active Directory Domain Services の概要](active-directory-domain-services-overview.md)

-   [管理されたサービス アカウント。理解、実装、ベスト プラクティス、およびトラブルシューティング](http://blogs.technet.com/b/askds/archive/20../managed-service-accounts-understanding-implementing-best-practices-and-troubleshooting.aspx)


