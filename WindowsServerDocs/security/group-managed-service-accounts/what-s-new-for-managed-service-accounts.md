---
title: "管理されたサービス アカウント向けの新機能"
description: "Windows Server のセキュリティ"
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
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# <a name="what39s-new-for-managed-service-accounts"></a>新; 管理されたサービス アカウントの新しい s

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

IT プロフェッショナル向けのこのトピックの変更について説明機能管理されたサービス アカウントのグループの Windows Server 2012 と Windows 8 における管理されたサービス アカウント (gMSA) の導入します。

管理されたサービス アカウントは、サービスと Windows サービスを手動でのこれらのアカウントのパスワードを管理する管理者の必要性を排除しながら、自分のドメイン アカウントを共有する IIS アプリケーション プールなどのタスクを提供するものです。 これは、パスワードの自動管理を提供する管理対象のドメイン アカウントです。

## <a name="versions"></a>Windows Server 2012 および Windows 8 で管理されたサービス アカウント向けの新機能
どのような機能が変更された Windows Server 2012 および Windows 8 で MSA を次に示します。

### <a name="group-managed-service-accounts"></a>グループ管理サービス アカウントします。
ドメイン内のサーバーのドメイン アカウントを構成する場合、クライアント コンピューターは認証し、そのサービスに接続します。 以前は、2 つだけのアカウントの種類 id が提供されたパスワードの管理を必要とせずします。 しかし、これらのアカウントの種類の制限があります。

-   コンピューター アカウントは 1 つのドメイン サーバーに制限され、パスワードはコンピューターによって管理されます。

-   管理されたサービス アカウントは 1 つのドメイン サーバーに制限し、パスワードはコンピューターによって管理されます。

これらのアカウントは、複数のシステムで共有することはできません。 したがって、望ましくないパスワードの有効期限を防ぐためには、各システム上の各サービスのアカウントを定期的に維持する必要があります。

**この変更はどのような値を追加しますか。**

グループの管理されたサービス アカウントはこの問題を解決ため、アカウントのパスワードは、Windows Server 2012 ドメイン コント ローラーによって管理され、複数の Windows Server 2012 システムして取得できます。 これにより、これらのアカウントのパスワード管理を処理する Windows サービス アカウントの管理オーバーヘッドが最小限に抑えます。

**動作の相違点**

コンピューターで Windows Server 2012 または Windows 8、MSA を作成し、サービス コントロール マネージャを通じてを管理できるように、サービスのさまざまなインスタンスに展開など、サーバー ファームのグループを実行していることができますから管理する 1 つのサーバー。 ツールと管理されたサービス アカウント、IIS アプリケーション プール マネージャーなどを管理するために使用するユーティリティは、グループ管理サービス アカウントで使用できます。 ドメイン管理者は、管理されたサービス アカウントまたはグループの管理されたサービス アカウントのライフ サイクル全体を管理できる、サービス管理者にサービスの管理に委任できます。 既存のクライアント コンピューターは、こうしたサービスへの認証は、どのサービス インスタンスを把握しなくても認証を受けることになります。

### <a name="interoperability"></a>削除されたまたは推奨されなくなった機能
Windows Server 2012、サーバーの管理されたサービス アカウントではなくグループ管理サービス アカウントを管理する Windows PowerShell コマンドレットの既定値です。

## <a name="see-also"></a>参照してください。

-   [グループの管理されたサービス アカウントの概要](group-managed-service-accounts-overview.md)

-   [Active Directory ドメイン サービスの概要](active-directory-domain-services-overview.md)

-   [管理されたサービス アカウント: 理解、実装、ベスト プラクティス、およびトラブルシューティング](http://blogs.technet.com/b/askds/archive/20../managed-service-accounts-understanding-implementing-best-practices-and-troubleshooting.aspx)


