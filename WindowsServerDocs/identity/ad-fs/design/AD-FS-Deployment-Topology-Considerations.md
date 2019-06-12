---
ms.assetid: 4ef052f0-61a9-4912-b780-5c96187c850f
title: AD FS 展開トポロジに関する考慮事項
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: cf646dedef85add8607c7940275e3c3fae90a661
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445343"
---
# <a name="ad-fs-deployment-topology-considerations"></a>AD FS 展開トポロジに関する考慮事項

このトピックでは、計画、およびどの Active Directory フェデレーション サービスの設計に役立つ重要な考慮事項を説明します\(AD FS\)実稼働環境で使用するトポロジをデプロイします。 このトピックでは、確認し、どのような機能または機能を使用可能にできるようになります AD FS を展開した後に影響する考慮事項を評価するための開始点です。 たとえば、どのデータベースに応じて、AD FS 構成データベースを格納する型は最終的に決定かどうかは、特定の Security Assertion Markup Language を実装することができます\(SAML\) SQL を必要とする機能サーバー。  

## <a name="determining-which-type-of-ad-fs-configuration-database-to-use"></a>使用する AD FS 構成データベースの種類の決定  
AD FS 構成を格納するデータベースを使用して、場合によっては — トランザクション データは、フェデレーション サービスに関連します。 AD FS ソフトウェアを使用するには、ビルドを選択する\-Windows Internal database \(WID\)またはフェデレーション サービスでデータを格納する Microsoft SQL Server 2005 以降。  

ほとんどの場合は、この 2 つのデータベース タイプはほぼ等価です。 ただし、読み取りの詳細については、AD FS で使用できるさまざまな展開トポロジを開始する前に、注意するいくつかの違いがあります。 次の表では、WID データベースと SQL Server データベースの間は、サポートされている機能の違いについて説明します。  

AD FS の機能  

|機能|WID でのサポート|SQL Server でのサポート|この機能についての詳しい情報|  
|-----------|---------------------|----------------------------|---------------------------------------|  
|フェデレーション サーバー ファーム展開|はい、30 台のフェデレーション サーバー ファームごとの制限|[はい]。 1 つのファーム内に展開できるフェデレーション サーバーの数について制限はありません。|[AD FS 展開トポロジの決定](Determine-Your-AD-FS-Deployment-Topology.md)|  
|SAML アーティファクト解決**に注意してください。** この機能は、Microsoft Online Services、Microsoft Office 365、Microsoft Exchange、Microsoft Office SharePoint のシナリオには不要です。|X|〇|[AD FS 構成データベースの役割](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<br /><br />[AD FS のセキュリティを考慮した設計と展開のベスト プラクティス](Best-Practices-for-Secure-Planning-and-Deployment-of-AD-FS.md)|  
|SAML\/WS\-フェデレーション トークン リプレイ検出|X|〇|[AD FS 構成データベースの役割](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<br /><br />[AD FS のセキュリティを考慮した設計と展開のベスト プラクティス](Best-Practices-for-Secure-Planning-and-Deployment-of-AD-FS.md)|  

データベースの機能  

|機能|WID でのサポート|SQL Server でのサポート|この機能についての詳しい情報|  
|-----------|---------------------|----------------------------|---------------------------------------|  
|1 または読み取りをホストするサーバーをレプリケーションでは、基本的なデータベースの冗長性を使用してプル\-読み取りをホストしている移行元サーバーで行われた変更をデータベースで要求の唯一のコピー\/データベースのコピーを作成|〇|X|[AD FS 構成データベースの役割](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)|  
|高を使用してデータベースの冗長性\-フェールオーバー クラスタ リングやミラーリングなどの可用性ソリューション\(データベース層のみ\)**に注意してください。** すべての AD FS 展開トポロジは、AD FS サービス層でのクラスタ リングをサポートします。|X|〇|[AD FS 構成データベースの役割](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<br /><br />[高可用性ソリューションの概要](https://go.microsoft.com/fwlink/?LinkId=179853)|  

### <a name="sql-server-considerations"></a>SQL Server に関する考慮事項  
AD FS の展開の構成データベースとして SQL Server を選択した場合は、次の事項を検討してください。  

-   **SAML の機能と、その機能がデータベース サイズやデータ量増大に及ぼす影響**。 SAML アーティファクト解決や SAML トークン リプレイ検出の機能のいずれかが有効な場合、AD FS では、発行される AD FS トークンそれぞれの SQL Server 構成データベース内の情報が格納されます。 このアクティビティの結果として、SQL Server データベースの増加が重要であると見なされませんし、構成済みのトークン リプレイ保持期間に依存します。 成果物の各レコードが、サイズが約 30 キロバイト\(KB\)します。  

-   **実際の展開に必要なサーバーの数**。 少なくとも 1 つの追加サーバーを追加する必要があります\(、AD FS インフラストラクチャをデプロイするために必要なサーバーの総数を\)は、SQL Server インスタンスの専用のホストとして機能します。 フェールオーバー クラスタ リングやミラーリングを使用して、SQL Server 構成データベースのフォールト トレランスやスケーラビリティを提供する場合は、2 つの SQL サーバーの最小値が必要です。  

### <a name="how-the-configuration-database-type-you-select-may-impact-hardware-resources"></a>選択した構成データベースのタイプがハードウェア リソースに及ぼす影響  
SQL Server データベースを使用してファームに展開されているフェデレーション サーバーではなく、WID を使用してファームに展開されているフェデレーション サーバー上のハードウェア リソースへの影響は大きくありません。 ただし、することが重要際の考慮事項、WID を使用して、ファームの各フェデレーション サーバー ファームの必要がありますを格納、管理、法線も継続して、AD FS 構成データベースのローカル コピーのレプリケーションの変更を維持フェデレーション サービスに必要な操作です。  

比較では、SQL Server データベースを使用しているファームに展開されているフェデレーション サーバーは必ずしもありません、AD FS 構成データベースのローカル インスタンス。 したがって、必要なハードウェア リソースの量はかなり少なくなる可能性があります。  

## <a name="verifying-that-your-production-environment-can-support-an-ad-fs-deployment"></a>実際の運用環境で AD FS 展開をサポートできることを確認する  
を展開するフェデレーション サーバーに加えてと、既存の運用環境のセットアップ方法に応じて、次の追加のサーバーは、新しい AD FS デプロイをサポートするために必要なインフラストラクチャを提供する必要があります。  

-   Active Directory ドメイン コントローラー  

-   証明機関\(CA\)  

-   フェデレーション メタデータをホストする Web サーバー  

-   ネットワーク負荷分散\(NLB\)  

## <a name="see-also"></a>関連項目
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
