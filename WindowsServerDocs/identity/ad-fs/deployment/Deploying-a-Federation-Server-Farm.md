---
ms.assetid: bbb5b68f-00ad-4715-8176-0c2769b706c4
title: Windows Server 2012 R2 AD FS の展開ガイド
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 114f0b13ec2ed556402b61217337de0f93d1fba9
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2020
ms.locfileid: "87520001"
---
# <a name="deploying-a-federation-server-farm"></a>フェデレーション サーバー ファームの展開

フェデレーション サーバー ファームを展開するためには、このチェックリストのタスクをこの順番で行います。 参照リンクをクリックして概要に関するトピックに移動した場合は、そのトピックを確認した後、このチェックリストに戻って、チェックリストの残りの作業に進んでください。

![フェデレーションサーバーファーム](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**の展開のチェックリスト: フェデレーションサーバーファームの展開**

|タスク|リファレンス|
|--------|-------------|
|Active Directory フェデレーションサービス (AD FS) AD FS の展開を準備する際の重要な概念と考慮事項を確認し \( \) ます。 **注:**|![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows server 2012 R2 の設計ガイド AD FS](../../ad-fs/design/AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)フェデレーションサーバーファームの展開<p>![フェデレーションサーバーファームの展開](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[キー AD FS の概念につい](../../ad-fs/technical-reference/Understanding-Key-AD-FS-Concepts.md)て|
||AD FS の構成ストアに Microsoft SQL Server を使用する場合は、SQL Server の機能するインスタンスを展開する。|[SQL Server](/sql/sql-server/?view=sql-server-ver15) **警告:** Windows Server 2012 R2 で AD FS ファームを作成し SQL Server を使用して構成データを格納する場合は、SQL Server 2012 を含む SQL Server 2008 以降のバージョンを使用できます。|
|コンピューターを Active Directory ドメインに参加させる。|![フェデレーションサーバーファームの展開](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[ドメインへのコンピューターの参加](Join-a-Computer-to-a-Domain.md)|
|\(AD FS 用の Secure Socket Layer SSL \) 証明書を登録します。|![フェデレーションサーバーファーム](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[の展開 AD FS 用の SSL 証明書を登録する](Enroll-an-SSL-Certificate-for-AD-FS.md)|
|AD FS 役割サービスをインストールする。|![フェデレーションサーバーファーム](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[の展開 AD FS の役割サービスをインストールする](Install-the-AD-FS-Role-Service.md)|
|フェデレーション サーバーを構成する。|![フェデレーションサーバーファーム](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[の展開フェデレーションサーバーを構成](Configure-a-Federation-Server.md)する|
|オプションの手順: デバイス登録サービス DRS を使用してフェデレーションサーバーを構成 \( \) します。|![フェデレーションサーバーファームの展開](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[デバイス登録サービスを使用してフェデレーションサーバーを構成する](Configure-a-federation-server-with-Device-Registration-Service.md)|
|ホスト \( a \) とエイリアス \( CNAME \) リソースレコードを、 \( \) フェデレーションサービスと DRS の企業ドメインネームシステム DNS に追加します。|![フェデレーションサーバーファーム](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[の展開フェデレーションサービスと DRS の企業 DNS を構成する](Configure-Corporate-DNS-for-the-Federation-Service-and-DRS.md)|
|フェデレーション サーバーが正常に動作することを確認する。|![フェデレーションサーバーファームの展開](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーションサーバーが動作していることを確認する](Verify-That-a-Federation-Server-Is-Operational.md)|


## <a name="see-also"></a>参照
[AD FS 展開](../../ad-fs/AD-FS-Deployment.md)

[Windows Server 2012 R2 AD FS の展開ガイド](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)

