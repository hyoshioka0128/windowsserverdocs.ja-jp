---
ms.assetid: f0464182-56a2-4bfa-a8c8-7e39c1bd62d3
title: WID とプロキシを使用するフェデレーション サーバー ファーム
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: a906876c25fea62e20abfebf2268af977e6b3ad3
ms.sourcegitcommit: de8fea497201d8f3d995e733dfec1d13a16cb8fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87864043"
---
# <a name="legacy-ad-fs-federation-server-farm-using-wid-and-proxies"></a>WID とプロキシを使用する従来の AD FS フェデレーションサーバーファーム

この Active Directory フェデレーションサービス (AD FS) の展開トポロジ (AD FS) は、Windows Internal Database (WID) トポロジを使用するフェデレーションサーバーファームと同じですが、外部ユーザーをサポートするために、プロキシコンピューターが境界ネットワークに追加されます。 これらのプロキシは、企業ネットワークの外部からのクライアント認証要求をフェデレーションサーバーファームにリダイレクトします。 以前のバージョンの AD FS では、これらのプロキシはフェデレーションサーバープロキシと呼ばれていました。

> [!IMPORTANT]
> Windows Server 2012 R2 の Active Directory フェデレーションサービス (AD FS) (AD FS) では、フェデレーションサーバープロキシの役割は、Web アプリケーションプロキシと呼ばれる新しいリモートアクセス役割サービスによって処理されます。 AD FS が企業ネットワークの外部からアクセスできるようにします。これは、Windows Server 2012 の AD FS 2.0 や AD FS など、AD FS のレガシバージョンでフェデレーションサーバープロキシを展開するためのものであり、Windows Server 2012 R2 で AD FS 用に1つ以上の web アプリケーションプロキシを展開することができます。
>
> AD FS のコンテキストでは、Web アプリケーションプロキシは AD FS フェデレーションサーバープロキシとして機能します。 さらに、Web アプリケーション プロキシには、企業ネットワーク内部の Web アプリケーション用のリバース プロキシ機能があり、ユーザーは任意のデバイスで企業ネットワーク外部から Web アプリケーションにアクセスできます。 Web アプリケーション プロキシの役割サービスの詳細については、「Web アプリケーション プロキシの概要」を参照してください。
>
> Web アプリケーション プロキシの展開を計画するには、次のトピックの情報を確認できます。
>
> - [Web アプリケーションプロキシインフラストラクチャ (WAP) を計画する](/previous-versions/orphan-topics/ws.11/dn383648(v=ws.11))
> - [Web アプリケーション プロキシ サーバーを計画する](/previous-versions/orphan-topics/ws.11/dn383647(v=ws.11))

## <a name="deployment-considerations"></a>デプロイに関する考慮事項
このセクションでは、この展開トポロジに関連する対象ユーザー、利点、および制限事項に関するさまざまな考慮事項について説明します。

### <a name="who-should-use-this-topology"></a>このトポロジを使用する必要がありますか。

- 100以下の信頼関係がある組織。内部ユーザーと外部ユーザーの両方を提供する必要があります (企業ネットワークの外部にあるコンピューターにログオンしている場合)。フェデレーションアプリケーションまたはサービスへのシングルサインオン (SSO) アクセスを使用します。

- 内部ユーザーと外部ユーザーの両方に Microsoft Office 365 への SSO アクセスを提供する必要がある組織

- 外部ユーザーを持ち、冗長でスケーラブルなサービスを必要とする小規模の組織

### <a name="what-are-the-benefits-of-using-this-topology"></a>このトポロジを使用する利点とは

- [WID トポロジを使用するフェデレーションサーバーファーム](Federation-Server-Farm-Using-WID.md)と同じ利点に加えて、外部ユーザーに追加のアクセスを提供する利点もあります。

### <a name="what-are-the-limitations-of-using-this-topology"></a>このトポロジを使用する場合の制限事項を挙げてください。

- [WID トポロジを使用したフェデレーションサーバーファーム](Federation-Server-Farm-Using-WID.md)の一覧と同じ制限事項

    | 1-100 個の RP 信頼 | 100 個を超える RP 信頼 |
    |--|--|
    | **1-30 個の AD FS ノード:** WID サポート対象 | **1-30 個の AD FS ノード:** WID の使用はサポート対象外 - SQL が必要 |
    | **30 個を超える AD FS ノード:** WID の使用はサポート対象外 - SQL が必要 | **30 個を超える AD FS ノード:** WID の使用はサポート対象外 - SQL が必要 |

## <a name="server-placement-and-network-layout-recommendations"></a>サーバーの配置とネットワークレイアウトに関する推奨事項
このトポロジを展開するには、2つの web アプリケーションプロキシを追加するだけでなく、境界ネットワークがドメインネームシステム (DNS) サーバーおよび2番目のネットワーク負荷分散 (NLB) ホストにもアクセスできるようにする必要があります。 2番目の NLB ホストは、インターネットからアクセス可能なクラスター IP アドレスを使用する NLB クラスターを使用して構成する必要があります。また、企業ネットワーク (fs.fabrikam.com) で構成した前の NLB クラスターと同じクラスター DNS 名設定を使用する必要があります。 Web アプリケーションプロキシは、インターネットからアクセス可能な IP アドレスを使用して構成する必要もあります。

次の図は、既に説明した WID トポロジを持つ既存のフェデレーションサーバーファームと、架空の Fabrikam, Inc. が境界 DNS サーバーへのアクセスを提供し、同じクラスター DNS 名 (fs.fabrikam.com) を持つ2つ目の NLB ホストを追加し、境界ネットワークに2つの web アプリケーションプロキシ (wap1 と wap2) を追加する方法を示します。

![WID ファームとプロキシ](media/WIDFarmADFSBlue.gif)

フェデレーションサーバーまたは web アプリケーションプロキシで使用するためのネットワーク環境を構成する方法の詳細については、「AD FS の[要件](AD-FS-Requirements.md)」の「名前解決の要件」セクションを参照して、 [Web アプリケーションプロキシインフラストラクチャ (WAP) を計画](/previous-versions/orphan-topics/ws.11/dn383648(v=ws.11))してください。

## <a name="see-also"></a>参照
[AD FS の展開トポロジ](Plan-Your-AD-FS-Deployment-Topology.md) 
 を計画する[Windows Server 2012 R2 の AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)

