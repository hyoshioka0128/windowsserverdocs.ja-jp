---
title: リモート デスクトップ サービスのアーキテクチャ
description: RDS のアーキテクチャの図
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 02/10/2017
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7f73bb0a-ce98-48a4-9d9f-cf7438936ca1
author: lizap
manager: dongill
ms.openlocfilehash: ba597318cdaf1d4659a72905eeb4e252c9020e49
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887873"
---
# <a name="remote-desktop-services-architecture"></a>リモート デスクトップ サービスのアーキテクチャ

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

Windows アプリをホストするリモート デスクトップ サービスとエンドユーザーのデスクトップを展開するためのさまざまな構成を以下に示します。

>[!NOTE]
> 次のアーキテクチャ図は、Azure での RDS の使用を示します。 ただし、オンプレミスでリモート デスクトップ サービスを展開して、他のクラウドにします。 これらの図は主に、RDS ロールの併置されているし、他のサービスを使用して説明するために対象としています。

## <a name="standard-rds-deployment-architectures"></a>標準の RDS デプロイ アーキテクチャ

リモート デスクトップ サービスでは、2 つの標準的なアーキテクチャがあります。
-   完全に有効な RDS 環境を作成するサーバーの最小数を含むこの基本的な展開。
-   RDS 環境内の最高のアップタイムを保証するために必要なすべてのコンポーネントを含むこの高可用性の展開。

### <a name="basic-deployment"></a>基本的な展開

![基本的な RDS の展開](./media/basic-rds.png)

### <a name="highly-available-deployment"></a>高可用性の展開

![高可用性 RDS のデプロイ](./media/ha-rds.png)

## <a name="rds-architectures-with-unique-azure-paas-roles"></a>一意の Azure PaaS ロールを使用した RDS アーキテクチャ

ただし、標準の RDS デプロイ アーキテクチャでは、ほとんどのシナリオに合わせて、顧客価値を高めるファースト パーティの PaaS ソリューションで投資を Azure が続行されます。 Rds. に組み込むことを示すいくつかのアーキテクチャを以下に示します

### <a name="rds-deployment-with-azure-ad-domain-services"></a>Azure AD Domain Services での RDS のデプロイ

上記の 2 つの標準的なアーキテクチャ図は、上、従来 Active Directory (AD) を Windows Server VM にデプロイに基づいています。 ただし、従来の ad し、のみ Azure AD テナントを設定しないかどうか、office 365 などのサービスによって — が RDS を利用する、使用することができます[Azure AD Domain Services](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-overview) Azure IaaS で完全に管理されたドメインを作成するにはAzure AD テナントに存在する同じユーザーを使用する環境。 これには、手動でユーザーを同期して、複数の仮想マシンの管理の複雑さが削除されます。 Azure AD Domain Services は、いずれかの配置で作業できます。 基本または高可用性。

![Azure AD と RDS の展開](./media/aadds-rds.png)

### <a name="rds-deployment-with-azure-ad-application-proxy"></a>Azure AD アプリケーション プロキシを使用した RDS デプロイ

上記の 2 つの標準的なアーキテクチャ図は、RDS システムにインターネットに接続するエントリ ポイントとして、RD Web とゲートウェイ サーバーを使用します。 一部の環境では、管理者によって、境界からそれぞれ独自のサーバーを削除し、リバース プロキシのテクノロジで追加のセキュリティを提供するテクノロジを使用して、代わりに優先されます。 [Azure AD アプリケーション プロキシ](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started)PaaS ロールは、このシナリオで適切に適合します。

サポートされている構成とセットアップを作成する方法は、次を参照してください。 方法[Azure AD アプリケーション プロキシでのリモート デスクトップを発行](/azure/active-directory/application-proxy-publish-remote-desktop)します。

![Azure AD アプリケーション プロキシを使用した RDS](./media/aadappproxy-rds.png)
