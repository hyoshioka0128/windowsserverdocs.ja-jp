---
title: RDS - Azure サービスとの統合
description: RDS を Azure 展開に統合し、Azure を RDS 展開に統合する方法について説明します。
ms.author: elizapo
ms.date: 08/18/2017
ms.topic: article
author: lizap
ms.openlocfilehash: 410a08d5b222fe0888c77ca6eac061a302730619
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87948885"
---
# <a name="remote-desktop-services---integrating-with-azure-services"></a>リモート デスクトップ サービス - Azure サービスとの統合

Windows Server 2016 は、リモート デスクトップ サービスによるデスクトップとアプリケーションの強力なセキュリティで保護された配信と、Microsoft Azure が提供する柔軟でスケーラブルなサービスを組み合わせています。 Azure サービスを使用して RDS をデプロイすると、オンプレミス サーバーのインフラストラクチャ保守コストの削減、高可用性を確保するために Azure サービスによる安定性の向上、多要素認証によるセキュリティの向上、既存の ID を使用したユーザーのエクスペリエンス向上を図り、RDS のリソースにアクセスすることができます。

次の情報を使用して、Azure をリモート デスクトップ展開に統合します。

- [RDS で多要素認証を使用する方法について](/azure/multi-factor-authentication/nps-extension-remote-desktop-gateway)
- [RDS 展開と Azure AD Domain Services との統合](rds-azure-adds.md)
- [Azure AD アプリケーション プロキシを使用したリモート デスクトップの公開](/azure/active-directory/application-proxy-publish-remote-desktop)

これらのサービスを使用してリモート デスクトップ展開のアーキテクチャを簡略化する方法については、「[一意の Azure PaaS ロールを使用した RDS アーキテクチャ](desktop-hosting-logical-architecture.md#rds-architectures-with-unique-azure-paas-roles)」を参照してください。