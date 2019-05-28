---
ms.assetid: bbb5b68f-00ad-4715-8176-0c2769b706c4
title: Windows Server 2012 R2 AD FS の展開ガイド
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: c0f8dca425f644952c36a289ec72651f6383e846
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192186"
---
# <a name="deploying-a-federation-server-farm"></a>フェデレーション サーバー ファームの展開


フェデレーション サーバー ファームを展開するためには、このチェックリストのタスクをこの順番で行います。 参照リンクから概念トピックが表示される場合は、概念トピックを参照した後でこのチェックリストに戻り、チェックリストの残りのタスクを完了します。  
  
![フェデレーション サーバー ファームを展開する](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**チェックリスト。フェデレーション サーバー ファームのデプロイ**  
  
||タスク|リファレンス|  
|-|--------|-------------|  
|![フェデレーション サーバー ファームを展開します。](media/icon_checkboxo.gif)|Active Directory フェデレーション サービスの展開を準備するときに、重要な概念と考慮事項を確認\(AD FS\)します。 **注:** |![フェデレーション サーバー ファームを展開する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Server 2012 R2 で AD FS 設計ガイド](../../ad-fs/design/AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)<br /><br />![フェデレーション サーバー ファームを展開する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Understanding Key AD FS Concepts](../../ad-fs/technical-reference/Understanding-Key-AD-FS-Concepts.md)|  
||AD FS の構成ストアに Microsoft SQL Server を使用する場合は、SQL Server の機能するインスタンスを展開する。|[SQL Server](https://technet.microsoft.com/sqlserver) **警告。** Windows Server 2012 R2 では、AD FS ファームを作成し、SQL Server を使用して構成データを格納する場合は、SQL Server 2008 以降のバージョン (SQL Server 2012 を含みます) を使用できます。|  
|![フェデレーション サーバー ファームを展開します。](media/icon_checkboxo.gif)|コンピューターを Active Directory ドメインに参加させる。|![フェデレーション サーバー ファームを展開する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[コンピューターをドメインに参加させる](Join-a-Computer-to-a-Domain.md)|  
|![フェデレーション サーバー ファームを展開します。](media/icon_checkboxo.gif)|Secure Socket Layer を登録\(SSL\) AD FS 用の証明書。|![フェデレーション サーバー ファームを展開する](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[for AD FS の SSL 証明書の登録](Enroll-an-SSL-Certificate-for-AD-FS.md)|  
|![フェデレーション サーバー ファームを展開します。](media/icon_checkboxo.gif)|AD FS 役割サービスをインストールする。|![フェデレーション サーバー ファームを展開する](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[AD FS 役割サービスのインストール](Install-the-AD-FS-Role-Service.md)|  
|![フェデレーション サーバー ファームを展開します。](media/icon_checkboxo.gif)|フェデレーション サーバーを構成する。|![フェデレーション サーバー ファームを展開する](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[フェデレーション サーバーを構成します。](Configure-a-Federation-Server.md)|  
|![フェデレーション サーバー ファームを展開します。](media/icon_checkboxo.gif)|省略可能な手順:デバイス登録サービスでフェデレーション サーバーを構成\(DRS\)します。|![フェデレーション サーバー ファームを展開する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[with Device Registration Service をフェデレーション サーバーを構成します。](Configure-a-federation-server-with-Device-Registration-Service.md)|  
|![フェデレーション サーバー ファームを展開します。](media/icon_checkboxo.gif)|ホストの追加\(A\)とエイリアス\(CNAME\)リソース レコードを会社のドメイン ネーム システムに\(DNS\)フェデレーション サービスおよび DRS 用です。|![フェデレーション サーバー ファームを展開する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション サービスおよび DRS 企業 DNS を構成します。](Configure-Corporate-DNS-for-the-Federation-Service-and-DRS.md)|  
|![フェデレーション サーバー ファームを展開します。](media/icon_checkboxo.gif)|フェデレーション サーバーが正常に動作することを確認する。|![フェデレーション サーバー ファームを展開する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[いることを確認、フェデレーション サーバーが正常に動作](Verify-That-a-Federation-Server-Is-Operational.md)|  
  

## <a name="see-also"></a>関連項目  
[AD FS 展開](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS 展開ガイドします。](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
  

