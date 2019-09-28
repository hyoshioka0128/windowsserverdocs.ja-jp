---
title: What's New for Managed Service Accounts
description: Windows Server のセキュリティ
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: de4d64e3dbe4bc7c7cba32f066a696636632224d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403725"
---
# <a name="what39s-new-for-managed-service-accounts"></a>管理&#39;されたサービスアカウントの新機能

>適用先:Windows Server (半期チャネル)、Windows Server 2016

IT プロフェッショナル向けのこのトピックでは、Windows Server 2012 および Windows 8 でのグループの管理されたサービスアカウント (gMSA) の導入により、管理されたサービスアカウントの機能の変更について説明します。

管理されたサービス アカウントは、Windows サービスや IIS アプリケーション プールなど、独自のドメイン アカウントを共有するサービスとタスクを提供できるように設計されたものです。管理者にとっては、これらのアカウントのパスワードを手動で管理する必要がなくなります。 管理されたサービス アカウントは、パスワードの自動管理が可能な管理されたドメイン アカウントです。

## <a name="versions"></a>Windows Server 2012 および Windows 8 での管理されたサービスアカウントの新機能
ここでは、Windows Server 2012 および Windows 8 で MSA に加えられた機能の変更について説明します。

### <a name="group-managed-service-accounts"></a>グループ管理サービス アカウント
ドメイン アカウントがドメイン内のサーバーに対して構成されている場合、クライアント コンピューターは、そのサービスに対して認証を行い、接続できます。 これまでは、パスワードを管理しなくても ID が提供されたアカウントは 2 種類だけで、 次のような制限もありました。

-   コンピューター アカウントは、1 つのドメイン サーバーに制限され、パスワードはコンピューターによって管理される

-   管理されたサービス アカウントは、1 つのドメイン サーバーに制限され、パスワードはコンピューターによって管理される

これらのアカウントを複数のシステムで共有することはできません。 したがって、パスワードの有効期限が切れるのを防ぐために、各システムのサービスごとにアカウントを維持する作業が定期的に発生します。

**この変更の利点**

グループの管理されたサービスアカウントは、この問題を解決します。これは、アカウントのパスワードが Windows Server 2012 ドメインコントローラーによって管理され、複数の Windows Server 2012 システムで取得できるためです。 Windows でこれらのアカウントのパスワード管理を処理できるようになるため、サービス アカウントの管理にかかわるオーバーヘッドが最小限に抑えられます。

**動作の相違点**

Windows Server 2012 または Windows 8 を実行しているコンピューターでは、サービスコントロールマネージャーを使用して、グループの MSA を作成および管理できます。これにより、サーバーファームに展開されたサービスの多数のインスタンスを1つのサーバーから管理できます。 管理されたサービス アカウントの管理に使用していたツールとユーティリティ (IIS アプリケーション プール マネージャーなど) は、グループの管理されたサービス アカウントにも使用できます。 ドメイン管理者は、サービスの管理をサービス管理者に委任できます。サービス管理者は、管理されたサービス アカウントまたはグループの管理されたサービス アカウントのライフサイクル全体を管理できます。 既存のクライアント コンピューターは、認証先のサービス インスタンスを把握しなくても、こうしたサービスに対して認証を実行できるようになります。

### <a name="interoperability"></a>削除または非推奨の機能
Windows Server 2012 の場合、Windows PowerShell コマンドレットは、既定では、サーバーの管理されたサービスアカウントではなく、グループの管理されたサービスアカウントを管理します。

## <a name="see-also"></a>関連項目

-   [グループの管理されたサービスアカウントの概要](group-managed-service-accounts-overview.md)

-   [Active Directory Domain Services の概要](active-directory-domain-services-overview.md)

-   @no__t 0 で管理されるサービスアカウント:@ No__t の理解、実装、ベストプラクティス、およびトラブルシューティング


