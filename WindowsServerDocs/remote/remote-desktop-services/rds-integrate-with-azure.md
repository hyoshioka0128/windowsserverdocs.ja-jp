---
title: RDS で Azure サービスとの統合
description: RDS のデプロイに、Azure のデプロイと Azure に RDS を統合する方法について説明します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 08/18/2017
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
ms.openlocfilehash: e582612496591356ed96b34522333d0e8bf34093
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879603"
---
# <a name="remote-desktop-services---integrating-with-azure-services"></a>リモート デスクトップ サービスの Azure サービスとの統合

Windows Server 2016 では、デスクトップと Microsoft Azure が提供する柔軟でスケーラブルなサービスでリモート デスクトップ サービスを使ったアプリの強力なセキュリティで保護された配信を結合します。 オンプレミス サーバーのインフラストラクチャのメンテナンス コストの削減、高可用性を確保、多要素認証を使用してセキュリティを強化する Azure サービスを使用して、安定性の向上を支援する Azure サービスを使用した RDS をデプロイし、強化できます、rds. でリソースにアクセスする既存の id を使用してユーザーのエクスペリエンス

リモート デスクトップのデプロイに Azure を統合するのにには、次の情報を使用します。

- [RDS での多要素認証を使用する方法について説明します](/azure/multi-factor-authentication/nps-extension-remote-desktop-gateway)
- [Azure AD Domain Services を RDS デプロイに統合します。](rds-azure-adds.md)
- [Azure AD アプリケーション プロキシを使用したリモート デスクトップを発行します。](/azure/active-directory/application-proxy-publish-remote-desktop)

これらのサービスがリモート デスクトップの展開のアーキテクチャを簡略化する方法については、チェック アウト[一意の Azure PaaS ロールを使用した RDS アーキテクチャ](desktop-hosting-logical-architecture.md#rds-architectures-with-unique-azure-paas-roles)します。