---
ms.assetid: 4ef052f0-61a9-4912-b780-5c96187c850f
title: "AD FS 展開トポロジに関する考慮事項"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: eee14ee7bb50e1a82f35caf9fbacda0b86d3a1ad
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="ad-fs-deployment-topology-considerations"></a>AD FS 展開トポロジに関する考慮事項

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックでは、計画し、実稼働環境で使用するにはどの Active Directory フェデレーション サービス \(AD FS\) 展開トポロジの設計に役立つ重要な考慮事項について説明します。 このトピックでは開始点を確認し、どのような機能ができるかをご確認いただける AD FS を展開した後に影響する考慮事項を評価します。 たとえば、によってどのデータベース タイプの AD FS 構成データベースを格納するが最終的に決まるかどうかは、SQL Server を必要とする特定の Security Assertion Markup Language \(SAML\) 機能を実装することができます。  
  
## <a name="determining-which-type-of-ad-fs-configuration-database-to-use"></a>使用する AD FS 構成データベースの種類の決定  
AD FS 構成を保存するデータベースを使用して: 場合によっては — トランザクション データは、フェデレーション サービスに関連します。 AD FS ソフトウェアを使用すると、組み込みの Windows Internal Database \(WID\) または Microsoft SQL Server 2005 以降では、フェデレーション サービス データを格納するのに] を選択します。  
  
ほとんどの場合、2 つのデータベース タイプはほぼ等価です。 ただし、これには注意すべきの詳細については、AD FS で使用できるさまざまな展開トポロジの検討を始める前にいくつかの違いがあります。 次の表では、WID データベースと SQL Server データベースの間でサポートされる機能の相違点について説明します。  
  
AD FS 機能  
  
|機能|WID でのサポート|SQL Server でサポートされているか。|この機能の詳細について|  
|-----------|---------------------|----------------------------|---------------------------------------|  
|フェデレーション サーバー ファーム展開|はい、5 台のフェデレーション サーバー ファームごとの制限|うん。 1 つのファームに展開するフェデレーション サーバーの数の制限はありません。|[AD FS 展開トポロジを決定します。](Determine-Your-AD-FS-Deployment-Topology.md)|  
|SAML アーティファクト解決**注:**この機能は Microsoft Online Services、Microsoft Office 365、Microsoft Exchange、または Microsoft Office SharePoint のシナリオに必要なできません。|違います|うん|[AD FS 構成データベースの役割](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<br /><br />[セキュリティで保護の計画と AD FS の展開のベスト プラクティス](Best-Practices-for-Secure-Planning-and-Deployment-of-AD-FS.md)|  
|フェデレーション WS\ SAML\/トークン リプレイ検出|違います|うん|[AD FS 構成データベースの役割](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<br /><br />[セキュリティで保護の計画と AD FS の展開のベスト プラクティス](Best-Practices-for-Secure-Planning-and-Deployment-of-AD-FS.md)|  
  
データベースの機能  
  
|機能|WID でのサポート|SQL Server でサポートされているか。|この機能の詳細について|  
|-----------|---------------------|----------------------------|---------------------------------------|  
|プル レプリケーションを移行元サーバーで行われた変更をデータベースで要求の読み取り専用のコピーをホストしている 1 つまたは複数のサーバーをホストするデータベースの読み取り/書き込みコピーを使用して基本的なデータベース冗長化|うん|違います|[AD FS 構成データベースの役割](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)|  
|フェールオーバー クラスタ リングやミラーリングなどの高可用性ソリューションを使用するデータベース冗長化 \ (データベース層 only\) で**注:**すべての AD FS 展開トポロジは、AD FS サービス層でのクラスタ リングをサポートします。|違います|うん|[AD FS 構成データベースの役割](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<br /><br />[高可用性ソリューションの概要](https://go.microsoft.com/fwlink/?LinkId=179853)|  
  
### <a name="sql-server-considerations"></a>SQL Server に関する考慮事項  
AD FS 展開の構成データベースとして SQL Server を選択した場合、次の事項を検討してください。  
  
-   **SAML の機能とデータベースのサイズと増大に及ぼす影響**します。 SAML アーティファクト解決や SAML トークン リプレイ検出の機能のいずれかが有効な場合、AD FS は、発行される AD FS トークンそれぞれの SQL Server 構成データベースの情報を格納します。 このアクティビティの結果として SQL Server データベースの拡張は重要であるとは見なされませんし、構成済みのトークン リプレイ保持期間に依存します。 各アーティファクト レコードは、約 30 キロバイト \(KB\) のサイズを持っています。  
  
-   **展開に必要なサーバー数**します。 少なくとも 1 つの追加サーバーを追加する必要があります \ (、AD FS infrastructure\ を展開するのに必要なサーバーの合計数) を SQL Server インスタンス専用のホストとして機能することです。 フェールオーバー クラスタ リングやミラーリングを使用して SQL Server 構成データベースのフォールト トレランスとスケーラビリティを提供する場合は、次の 2 つの SQL サーバーの最小値が必要です。  
  
### <a name="how-the-configuration-database-type-you-select-may-impact-hardware-resources"></a>構成データベースのタイプを選択する方法がハードウェア リソースに影響を与える  
SQL Server データベースを使用してファームに展開されているフェデレーション サーバーではなく、WID を使用してファームに展開されているフェデレーション サーバー上のハードウェア リソースへの影響は大きな違いはありません。 ただし、重要なこと、ファームで WID を使用するときにそのファーム内の各フェデレーション サーバー必要がありますを保存、管理、およびも継続するフェデレーション サービスに必要な通常の操作中に、AD FS 構成データベースのローカル コピーのレプリケーションの変更を維持考慮事項です。  
  
比較では、SQL Server データベースを使用しているファームに展開されているフェデレーション サーバーには必ずしもが含まれていない、AD FS 構成データベースのローカル インスタンスには。 そのため、ハードウェア リソースの量はかなり少なくをなる可能性があります。  
  
## <a name="verifying-that-your-production-environment-can-support-an-ad-fs-deployment"></a>実稼働環境で AD FS の展開をサポートできることを確認します。  
フェデレーション サーバーを展開することに加えて、既存の運用環境のセットアップ方法によっては、次の追加のサーバーを新しい AD FS の展開をサポートするために必要なインフラストラクチャを提供する必要があります。  
  
-   Active Directory ドメイン コントローラー  
  
-   証明機関 \(CA\)  
  
-   フェデレーション メタデータをホストする Web サーバー  
  
-   ネットワーク負荷分散 \(NLB\)  
  
## <a name="see-also"></a>参照してください。
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)
