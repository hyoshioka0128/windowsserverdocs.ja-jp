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

このトピックでは、運用環境で使用する\) 展開トポロジ AD FS \(Active Directory フェデレーションサービス (AD FS) を計画および設計する際に役立つ重要な考慮事項について説明します。 このトピックでは、AD FS を展開した後に使用可能になる機能に影響する考慮事項を確認および評価するための出発点について説明します。 たとえば、AD FS 構成データベースを格納するために選択するデータベースの種類によっては、SQL Server を必要とする SAML\) 機能 \(特定の Security Assertion Markup Language を実装できるかどうかが決まります。  

## <a name="determining-which-type-of-ad-fs-configuration-database-to-use"></a>使用する AD FS 構成データベースの種類の決定  
AD FS は、データベースを使用して構成を格納し、場合によっては、フェデレーションサービスに関連するトランザクションデータを格納します。 AD FS ソフトウェアを使用して、Windows Internal Database のビルドされた\-\(WID\) または Microsoft SQL Server 2005 以降フェデレーションサービスにデータを格納することができます。  

ほとんどの場合は、この 2 つのデータベース タイプはほぼ等価です。 ただし、AD FS で使用できるさまざまな展開トポロジについて理解を開始する前に、いくつかの点に注意する必要があります。 次の表では、WID データベースと SQL Server データベースの間でサポートされる機能の違いについて説明します。  

AD FS 機能  

|機能|WID でのサポート|SQL Server でのサポート|この機能についての詳しい情報|  
|-----------|---------------------|----------------------------|---------------------------------------|  
|フェデレーション サーバー ファーム展開|はい (ファームごとにフェデレーションサーバーを30個まで制限)|[はい]。 1 つのファーム内に展開できるフェデレーション サーバーの数について制限はありません。|[AD FS 展開トポロジの決定](Determine-Your-AD-FS-Deployment-Topology.md)|  
|SAML アーティファクトの解決に関する**注意:** この機能は、Microsoft Online Services、Microsoft Office 365、microsoft Exchange、または Microsoft Office SharePoint のシナリオには必要ありません。|X|〇|[AD FS 構成データベースの役割](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<br /><br />[AD FS のセキュリティを考慮した設計と展開のベスト プラクティス](Best-Practices-for-Secure-Planning-and-Deployment-of-AD-FS.md)|  
|SAML\/WS\-フェデレーション トークン リプレイ検出|X|〇|[AD FS 構成データベースの役割](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<br /><br />[AD FS のセキュリティを考慮した設計と展開のベスト プラクティス](Best-Practices-for-Secure-Planning-and-Deployment-of-AD-FS.md)|  

データベースの機能  

|機能|WID でのサポート|SQL Server でのサポート|この機能についての詳しい情報|  
|-----------|---------------------|----------------------------|---------------------------------------|  
|プルレプリケーションを使用した基本的なデータベースの冗長化。読み取りをホストしている1つ以上のサーバーが、データベースの読み取り\/書き込みコピーをホストするソースサーバーに対して行われた変更を\-、データベースのコピーのみをホストします。|〇|X|[AD FS 構成データベースの役割](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)|  
|データベース層でのフェールオーバークラスタリングやミラーリング \(など、高\-可用性ソリューションを使用したデータベースの冗長性\)**注:** すべての AD FS 配置トポロジは、AD FS サービス層でのクラスタリングをサポートしています。|X|〇|[AD FS 構成データベースの役割](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<br /><br />[高可用性ソリューションの概要](https://go.microsoft.com/fwlink/?LinkId=179853)|  

### <a name="sql-server-considerations"></a>SQL Server に関する考慮事項  
AD FS デプロイの構成データベースとして [SQL Server] を選択した場合は、次の展開のファクトを考慮する必要があります。  

-   **SAML の機能と、その機能がデータベース サイズやデータ量増大に及ぼす影響**。 SAML アーティファクト解決機能または SAML トークンリプレイ検出機能が有効になっている場合、AD FS は、発行された各 AD FS トークンの情報を SQL Server 構成データベースに格納します。 このアクティビティの結果として SQL Server データベースの増加は重要ではないと見なされ、構成済みのトークン再生保有期間によって異なります。 各アーティファクトレコードのサイズは約 30 kb \(KB\)です。  

-   **実際の展開に必要なサーバーの数**。 AD FS インフラストラクチャ\) を展開するために必要なサーバーの総数に、少なくとも1つの追加のサーバー \(を追加する必要があります。これは、SQL Server インスタンスの専用ホストとして機能します。 フェールオーバークラスタリングまたはミラーリングを使用して SQL Server 構成データベースのフォールトトレランスとスケーラビリティを実現する予定がある場合は、少なくとも2つの SQL server が必要です。  

### <a name="how-the-configuration-database-type-you-select-may-impact-hardware-resources"></a>選択した構成データベースのタイプがハードウェア リソースに及ぼす影響  
SQL Server データベースを使用しているファームに展開されているフェデレーションサーバーとは対照的に、WID を使用してファームに展開されているフェデレーションサーバー上のハードウェアリソースへの影響は、重要ではありません。 ただし、WID をファームに使用する場合は、そのファーム内の各フェデレーションサーバーが、AD FS 構成データベースのローカルコピーに対してレプリケーションの変更を保存、管理、および維持しながら、通常の処理を継続して行う必要があることを考慮することが重要です。フェデレーションサービスが必要とする操作。  

一方、SQL Server データベースを使用するファームに配置されているフェデレーションサーバーには、AD FS 構成データベースのローカルインスタンスが含まれているとは限りません。 したがって、必要なハードウェア リソースの量はかなり少なくなる可能性があります。  

## <a name="verifying-that-your-production-environment-can-support-an-ad-fs-deployment"></a>実際の運用環境で AD FS 展開をサポートできることを確認する  
展開するフェデレーションサーバーに加えて、既存の運用環境のセットアップ方法によっては、新しい AD FS の展開をサポートするために必要なインフラストラクチャを提供するために、次の追加サーバーが必要になる場合があります。  

-   Active Directory ドメイン コントローラー  

-   CA\) \(証明機関  

-   フェデレーション メタデータをホストする Web サーバー  

-   ネットワーク負荷分散 \(NLB\)  

## <a name="see-also"></a>参照
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
