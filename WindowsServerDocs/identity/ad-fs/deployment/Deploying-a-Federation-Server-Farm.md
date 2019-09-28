---
ms.assetid: bbb5b68f-00ad-4715-8176-0c2769b706c4
title: Windows Server 2012 R2 AD FS の展開ガイド
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: e5507cd567114d17c6500655ee210b70bd9ea1ec
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408413"
---
# <a name="deploying-a-federation-server-farm"></a>フェデレーション サーバー ファームの展開


フェデレーション サーバー ファームを展開するためには、このチェックリストのタスクをこの順番で行います。 参照リンクから概念トピックが表示される場合は、概念トピックを参照した後でこのチェックリストに戻り、チェックリストの残りのタスクを完了します。  
  
![deploying サーバーファームの展開 @ no__t-1Checklist リスト:フェデレーションサーバーファームの展開 @ no__t-0  
  
||タスク|参照|  
|-|--------|-------------|  
|![フェデレーションサーバーファームの展開](media/icon_checkboxo.gif)|Active Directory フェデレーションサービス (AD FS) \(AD FS @ no__t-1 を展開する準備として、重要な概念と考慮事項を確認します。 **注:**|@no__t](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS Windows server 2012 R2 の設計ガイド](../../ad-fs/design/AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)フェデレーションサーバーファームの展開<br /><br />@no__t、フェデレーションサーバーファームの展開の](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[主要な AD FS 概念につい](../../ad-fs/technical-reference/Understanding-Key-AD-FS-Concepts.md)て|  
||AD FS の構成ストアに Microsoft SQL Server を使用する場合は、SQL Server の機能するインスタンスを展開する。|[SQL Server](https://technet.microsoft.com/sqlserver) **警告:** Windows Server 2012 R2 では、AD FS ファームを作成し、SQL Server を使用して構成データを格納する場合は、SQL Server 2008 以降のバージョン (SQL Server 2012 を含みます) を使用できます。|  
|![フェデレーションサーバーファームの展開](media/icon_checkboxo.gif)|コンピューターを Active Directory ドメインに参加させる。|つのフェデレーションサーバーファーム](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[を展開するコンピューターをドメインに参加させる](Join-a-Computer-to-a-Domain.md)|  
|![フェデレーションサーバーファームの展開](media/icon_checkboxo.gif)|AD FS には、Secure Socket Layer \(SSL @ no__t 証明書を登録します。|![deploying サーバーファームを展開する](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[AD FS 用の SSL 証明書を登録する](Enroll-an-SSL-Certificate-for-AD-FS.md)|  
|![フェデレーションサーバーファームの展開](media/icon_checkboxo.gif)|AD FS 役割サービスをインストールする。|![deploying サーバーファーム](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[を展開する AD FS の役割サービスをインストールする](Install-the-AD-FS-Role-Service.md)|  
|![フェデレーションサーバーファームの展開](media/icon_checkboxo.gif)|フェデレーション サーバーを構成する。|![deploying サーバーファーム](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[の展開フェデレーションサーバーの構成](Configure-a-Federation-Server.md)|  
|![フェデレーションサーバーファームの展開](media/icon_checkboxo.gif)|省略可能な手順:デバイス登録サービスを使用してフェデレーションサーバーを構成する \(DRS @ no__t-1。|![deploying サーバーファーム](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[の展開デバイス登録サービスを使用してフェデレーションサーバーを構成する](Configure-a-federation-server-with-Device-Registration-Service.md)|  
|![フェデレーションサーバーファームの展開](media/icon_checkboxo.gif)|ホスト \(A @ no__t-1 と alias \(CNAME @ no__t リソースレコードを、フェデレーションサービスと DRS の企業ドメインネームシステム \(DNS @ no__t に追加します。|![deploying サーバーファーム](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[を展開するフェデレーションサービスと DRS の企業 DNS を構成する](Configure-Corporate-DNS-for-the-Federation-Service-and-DRS.md)|  
|![フェデレーションサーバーファームの展開](media/icon_checkboxo.gif)|フェデレーション サーバーが正常に動作することを確認する。|![deploying サーバーファームの展開](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーションサーバーが動作していることを確認する](Verify-That-a-Federation-Server-Is-Operational.md)|  
  

## <a name="see-also"></a>関連項目  
[AD FS 展開](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS 展開ガイド](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
  

