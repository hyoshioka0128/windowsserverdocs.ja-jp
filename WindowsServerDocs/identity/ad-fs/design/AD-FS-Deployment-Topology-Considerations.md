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
ms.openlocfilehash: c5a3c85d40baee137ecdf7a1a5507b25361cac6d
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191773"
---
# <a name="ad-fs-deployment-topology-considerations"></a>AD FS 展開トポロジに関する考慮事項

このトピックでは、計画、およびどの Active Directory フェデレーション サービスの設計に役立つ重要な考慮事項を説明します\(AD FS\)実稼働環境で使用するトポロジをデプロイします。 このトピックでは、確認し、どのような機能または機能を使用可能にできるようになります AD FS を展開した後に影響する考慮事項を評価するための開始点です。 たとえば、どのデータベースに応じて、AD FS 構成データベースを格納する型は最終的に決定かどうかは、特定の Security Assertion Markup Language を実装することができます\(SAML\) SQL を必要とする機能サーバー。  
  
## <a name="determining-which-type-of-adfs-configuration-database-to-use"></a>どのタイプの AD FS 構成データベースを使用するかを決定する  
AD FS 構成を格納するデータベースを使用して、場合によっては — トランザクション データは、フェデレーション サービスに関連します。 AD FS ソフトウェアを使用するには、ビルドを選択する\-Windows Internal database \(WID\)またはフェデレーション サービスでデータを格納する Microsoft SQL Server 2005 以降。  
  
ほとんどの場合は、この 2 つのデータベース タイプはほぼ等価です。 ただし、読み取りの詳細については、AD FS で使用できるさまざまな展開トポロジを開始する前に、注意するいくつかの違いがあります。 次の表は、WID データベースと SQL Server データベースでサポートされる機能の違いの説明をまとめたものです。  
  
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
SQL Server を AD FS 展開の構成データベースとして選ぶ場合は、次の事項を考慮してください。  
  
-   **SAML の機能と、その機能がデータベース サイズやデータ量増大に及ぼす影響**。 SAML アーティファクト解決や SAML トークン リプレイ検出の機能が有効化されているときは、発行された AD FS トークンそれぞれの情報が SQL Server 構成データベースに格納されます。 この結果として、SQL Server データベースのデータ量はそれほど増大しないと考えられていますが、増大する量はトークン リプレイ保持期間の設定によって異なります。 成果物の各レコードが、サイズが約 30 キロバイト\(KB\)します。  
  
-   **実際の展開に必要なサーバーの数**。 少なくとも 1 つの追加サーバーを追加する必要があります\(、AD FS インフラストラクチャをデプロイするために必要なサーバーの総数を\)は、SQL Server インスタンスの専用のホストとして機能します。 SQL Server 構成データベースに耐障害性と拡張性を持たせるためにフェールオーバー クラスタリングやミラーリングを使用する場合は、最低でも 2 つの SQL サーバーが必要です。  
  
### <a name="how-the-configuration-database-type-you-select-may-impact-hardware-resources"></a>選択した構成データベースのタイプがハードウェア リソースに及ぼす影響  
ファーム内に展開されるフェデレーション サーバーのハードウェア リソースに及ぶ影響は、WID を使用する場合でも SQL Server データベースを使用する場合でも、大きな違いはありません。 ただし、WID をファームに使用するときの重要な考慮事項が 1 つあります。それは、ファーム内の各フェデレーション サーバーが AD FS 構成データベースのローカル コピーを保持してレプリケーション変更の保存、管理、保守を行う必要があり、これと並行してフェデレーション サービスに必要な通常の動作も継続する必要があるということです。  
  
対照的に、フェデレーション サーバーが展開されているファームで SQL Server データベースを使用する場合は、AD FS 構成データベースのローカル インスタンスが各フェデレーション サーバーに存在していなくてもかまいません。 したがって、必要なハードウェア リソースの量はかなり少なくなる可能性があります。  
  
## <a name="verifying-that-your-production-environment-can-support-an-ad-fs-deployment"></a>実際の運用環境で AD FS 展開をサポートできることを確認する  
を展開するフェデレーション サーバーに加えてと、既存の運用環境のセットアップ方法に応じて、次の追加のサーバーは、新しい AD FS デプロイをサポートするために必要なインフラストラクチャを提供する必要があります。  
  
-   Active Directory ドメイン コントローラー  
  
-   証明機関\(CA\)  
  
-   フェデレーション メタデータをホストする Web サーバー  
  
-   ネットワーク負荷分散\(NLB\)  
  
## <a name="see-also"></a>関連項目
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
