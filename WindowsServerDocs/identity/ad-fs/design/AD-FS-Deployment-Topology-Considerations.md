---
ms.assetid: 4ef052f0-61a9-4912-b780-5c96187c850f
title: AD FS 展開トポロジに関する考慮事項
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 8e433083ce7f1bdcfa0d950b86692662044dd1ea
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87940439"
---
# <a name="ad-fs-deployment-topology-considerations"></a>AD FS 展開トポロジに関する考慮事項

このトピックでは、 \( \) 運用環境で使用する AD FS 配置トポロジ Active Directory フェデレーションサービス (AD FS) を計画および設計する際に役立つ重要な考慮事項について説明します。 このトピックでは、AD FS を展開した後に使用可能になる機能に影響する考慮事項を確認および評価するための出発点について説明します。 たとえば、AD FS 構成データベースを格納するために選択するデータベースの種類によっては、SQL Server を必要とする特定の Security Assertion Markup Language SAML 機能を実装できるかどうかが決まり \( \) ます。

## <a name="determining-which-type-of-ad-fs-configuration-database-to-use"></a>どのタイプの AD FS 構成データベースを使用するかを決定する
AD FS は、データベースを使用して構成を格納し、場合によっては、フェデレーションサービスに関連するトランザクションデータを格納します。 AD FS ソフトウェアを使用すると、 \- フェデレーションサービスにデータを格納するために、組み込みの Windows Internal Database \( WID \) または Microsoft SQL Server 2005 以降を選択できます。

ほとんどの場合は、この 2 つのデータベース タイプはほぼ等価です。 ただし、AD FS で使用できるさまざまな展開トポロジについて理解を開始する前に、いくつかの点に注意する必要があります。 次の表は、WID データベースと SQL Server データベースでサポートされる機能の違いの説明をまとめたものです。

AD FS 機能

|機能|WID でのサポート|SQL Server でのサポート|この機能についての詳しい情報|
|-----------|---------------------|----------------------------|---------------------------------------|
|フェデレーション サーバー ファーム展開|はい (ファームごとにフェデレーションサーバーを30個まで制限)|はい。 1 つのファーム内に展開できるフェデレーション サーバーの数について制限はありません。|[AD FS 展開トポロジの決定](Determine-Your-AD-FS-Deployment-Topology.md)|
|SAML アーティファクトの解決に関する**注意:** この機能は、Microsoft Online Services、Microsoft Office 365、microsoft Exchange、または Microsoft Office SharePoint のシナリオには必要ありません。|いいえ|はい|[AD FS 構成データベースの役割](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<p>[AD FS のセキュリティを考慮した設計と展開のベスト プラクティス](Best-Practices-for-Secure-Planning-and-Deployment-of-AD-FS.md)|
|SAML\/WS\-フェデレーション トークン リプレイ検出|いいえ|はい|[AD FS 構成データベースの役割](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<p>[AD FS のセキュリティを考慮した設計と展開のベスト プラクティス](Best-Practices-for-Secure-Planning-and-Deployment-of-AD-FS.md)|

Database の機能

|機能|WID でのサポート|SQL Server でのサポート|この機能についての詳しい情報|
|-----------|---------------------|----------------------------|---------------------------------------|
|プルレプリケーションを使用した基本的なデータベース冗長化。データベースの読み取り専用コピーをホストする1台以上のサーバーが、 \- \/ データベースの読み取り/書き込みコピーをホストするソースサーバーで行われた変更を要求します。|はい|いいえ|[AD FS 構成データベースの役割](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)|
|データベース層での \- フェールオーバークラスタリングやミラーリングなどの高可用性ソリューションを使用し \( たデータベースの冗長性 \) **:** すべての AD FS 配置トポロジは、AD FS サービス層でのクラスタリングをサポートします。|いいえ|はい|[AD FS 構成データベースの役割](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)<p>[高可用性ソリューションの概要](https://go.microsoft.com/fwlink/?LinkId=179853)|

### <a name="sql-server-considerations"></a>SQL Server に関する考慮事項
SQL Server を AD FS 展開の構成データベースとして選ぶ場合は、次の事項を考慮してください。

-   **SAML の機能と、その機能がデータベース サイズやデータ量増大に及ぼす影響**。 SAML アーティファクト解決や SAML トークン リプレイ検出の機能が有効化されているときは、発行された AD FS トークンそれぞれの情報が SQL Server 構成データベースに格納されます。 この結果として、SQL Server データベースのデータ量はそれほど増大しないと考えられていますが、増大する量はトークン リプレイ保持期間の設定によって異なります。 各アーティファクトレコードのサイズは約 30 \( kb \) です。

-   **実際の展開に必要なサーバーの数**。 \( \) SQL Server インスタンスの専用ホストとして機能する AD FS インフラストラクチャを展開するために必要なサーバーの総数に、少なくとも1つのサーバーを追加する必要があります。 SQL Server 構成データベースに耐障害性と拡張性を持たせるためにフェールオーバー クラスタリングやミラーリングを使用する場合は、最低でも 2 つの SQL サーバーが必要です。

### <a name="how-the-configuration-database-type-you-select-may-impact-hardware-resources"></a>選択した構成データベースのタイプがハードウェア リソースに及ぼす影響
ファーム内に展開されるフェデレーション サーバーのハードウェア リソースに及ぶ影響は、WID を使用する場合でも SQL Server データベースを使用する場合でも、大きな違いはありません。 ただし、WID をファームに使用するときの重要な考慮事項が 1 つあります。それは、ファーム内の各フェデレーション サーバーが AD FS 構成データベースのローカル コピーを保持してレプリケーション変更の保存、管理、保守を行う必要があり、これと並行してフェデレーション サービスに必要な通常の動作も継続する必要があるということです。

対照的に、フェデレーション サーバーが展開されているファームで SQL Server データベースを使用する場合は、AD FS 構成データベースのローカル インスタンスが各フェデレーション サーバーに存在していなくてもかまいません。 したがって、必要なハードウェア リソースの量はかなり少なくなる可能性があります。

## <a name="verifying-that-your-production-environment-can-support-an-ad-fs-deployment"></a>実際の運用環境で AD FS 展開をサポートできることを確認する
展開するフェデレーションサーバーに加えて、既存の運用環境のセットアップ方法によっては、新しい AD FS の展開をサポートするために必要なインフラストラクチャを提供するために、次の追加サーバーが必要になる場合があります。

-   Active Directory ドメイン コントローラー

-   証明機関の \( CA\)

-   フェデレーション メタデータをホストする Web サーバー

-   ネットワーク負荷分散 \( NLB\)

## <a name="see-also"></a>参照
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
