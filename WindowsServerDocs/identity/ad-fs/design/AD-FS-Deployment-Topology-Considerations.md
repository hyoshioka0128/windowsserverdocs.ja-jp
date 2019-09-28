---
ms.assetid: 4ef052f0-61a9-4912-b780-5c96187c850f
title: AD FS 展開トポロジに関する考慮事項
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 260d86c0feae0179620ece09e06f12729691b5a3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359221"
---
# <a name="ad-fs-deployment-topology-considerations"></a>AD FS 展開トポロジに関する考慮事項

このトピックでは、運用環境で使用する @no__t 0 AD FS @ no__t の展開トポロジを計画および Active Directory フェデレーションサービス (AD FS) 設計する際に役立つ重要な考慮事項について説明します。 このトピックでは、AD FS を展開した後に使用可能になる機能に影響する考慮事項を確認および評価するための出発点について説明します。 たとえば、AD FS 構成データベースを格納するために選択するデータベースの種類によっては、SQL Server を必要とする特定の Security Assertion Markup Language \(SAML @ no__t 機能を実装できるかどうかが決まります。  

## <a name="determining-which-type-of-ad-fs-configuration-database-to-use"></a>使用する AD FS 構成データベースの種類の決定  
AD FS は、データベースを使用して構成を格納し、場合によっては、フェデレーションサービスに関連するトランザクションデータを格納します。 AD FS ソフトウェアを使用すると、フェデレーションサービスにデータを格納するために、Windows Internal Database でビルドされた @ no__t-0in-1WID @ no__t、または Microsoft SQL Server 2005 以降のいずれかを選択できます。  

ほとんどの場合は、この 2 つのデータベース タイプはほぼ等価です。 ただし、AD FS で使用できるさまざまな展開トポロジについて理解を開始する前に、いくつかの点に注意する必要があります。 次の表では、WID データベースと SQL Server データベースの間でサポートされる機能の違いについて説明します。  

AD FS 機能  

|機能|WID でのサポート|SQL Server でのサポート|この機能についての詳しい情報|  
|-----------|---------------------|----------------------------|---------------------------------------|  
|フェデレーション サーバー ファーム展開|はい (ファームごとにフェデレーションサーバーを30個まで制限)|可能。 1 つのファーム内に展開できるフェデレーション サーバーの数について制限はありません。|[AD FS 展開トポロジの決定](Determine-Your-AD-FS-Deployment-Topology.md)|  
|SAML アーティファクト解決に関する**注意:** この機能は、Microsoft Online Services、Microsoft Office 365、Microsoft Exchange、Microsoft Office SharePoint のシナリオには不要です。|いいえ|はい|[AD FS 構成データベースの役割](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<br /><br />[AD FS のセキュリティを考慮した設計と展開のベスト プラクティス](Best-Practices-for-Secure-Planning-and-Deployment-of-AD-FS.md)|  
|SAML\/WS\-フェデレーション トークン リプレイ検出|いいえ|はい|[AD FS 構成データベースの役割](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<br /><br />[AD FS のセキュリティを考慮した設計と展開のベスト プラクティス](Best-Practices-for-Secure-Planning-and-Deployment-of-AD-FS.md)|  

データベースの機能  

|機能|WID でのサポート|SQL Server でのサポート|この機能についての詳しい情報|  
|-----------|---------------------|----------------------------|---------------------------------------|  
|プルレプリケーションを使用した基本的なデータベース冗長化。データベースの読み取り @ no__t-0only コピーをホストしている1つ以上のサーバーで、読み取り @ no__t-1write の書き込みコピーをホストするソースサーバー上で行われた変更を要求します。|はい|いいえ|[AD FS 構成データベースの役割](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)|  
|フェールオーバークラスタリングやミラーリングなどの高 @ no__t 可用性ソリューションを使用したデータベースの冗長性は、データベース層でのみ @ no__t に @no__t**ます。** すべての AD FS 展開トポロジは、AD FS サービス層でのクラスタリングをサポートします。|いいえ|はい|[AD FS 構成データベースの役割](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<br /><br />[高可用性ソリューションの概要](https://go.microsoft.com/fwlink/?LinkId=179853)|  

### <a name="sql-server-considerations"></a>SQL Server に関する考慮事項  
AD FS デプロイの構成データベースとして [SQL Server] を選択した場合は、次の展開のファクトを考慮する必要があります。  

-   **SAML の機能と、その機能がデータベース サイズやデータ量増大に及ぼす影響**。 SAML アーティファクト解決機能または SAML トークンリプレイ検出機能が有効になっている場合、AD FS は、発行された各 AD FS トークンの情報を SQL Server 構成データベースに格納します。 このアクティビティの結果として SQL Server データベースの増加は重要ではないと見なされ、構成済みのトークン再生保有期間によって異なります。 各アーティファクトレコードのサイズは約 30 kb \(KB @ no__t-1 です。  

-   **実際の展開に必要なサーバーの数**。 SQL Server インスタンスの専用ホストとして機能する AD FS インフラストラクチャ @ no__t を展開するために必要なサーバーの総数には、少なくとも1つの追加サーバー \(to 追加する必要があります。 フェールオーバークラスタリングまたはミラーリングを使用して SQL Server 構成データベースのフォールトトレランスとスケーラビリティを実現する予定がある場合は、少なくとも2つの SQL server が必要です。  

### <a name="how-the-configuration-database-type-you-select-may-impact-hardware-resources"></a>選択した構成データベースのタイプがハードウェア リソースに及ぼす影響  
SQL Server データベースを使用しているファームに展開されているフェデレーションサーバーとは対照的に、WID を使用してファームに展開されているフェデレーションサーバー上のハードウェアリソースへの影響は、重要ではありません。 ただし、WID をファームに使用する場合は、そのファーム内の各フェデレーションサーバーが、AD FS 構成データベースのローカルコピーに対してレプリケーションの変更を保存、管理、および維持しながら、通常の処理を継続して行う必要があることを考慮することが重要です。フェデレーションサービスが必要とする操作。  

一方、SQL Server データベースを使用するファームに配置されているフェデレーションサーバーには、AD FS 構成データベースのローカルインスタンスが含まれているとは限りません。 したがって、必要なハードウェア リソースの量はかなり少なくなる可能性があります。  

## <a name="verifying-that-your-production-environment-can-support-an-ad-fs-deployment"></a>実際の運用環境で AD FS 展開をサポートできることを確認する  
展開するフェデレーションサーバーに加えて、既存の運用環境のセットアップ方法によっては、新しい AD FS の展開をサポートするために必要なインフラストラクチャを提供するために、次の追加サーバーが必要になる場合があります。  

-   Active Directory ドメイン コントローラー  

-   証明機関 \(CA @ no__t  

-   フェデレーション メタデータをホストする Web サーバー  

-   ネットワーク負荷分散 \(NLB @ no__t  

## <a name="see-also"></a>関連項目
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
