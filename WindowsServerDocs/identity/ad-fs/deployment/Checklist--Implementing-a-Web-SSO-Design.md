---
ms.assetid: 30657638-5709-48c5-87aa-98f688e07b4c
title: "Web SSO 設計の実装のチェックリスト-"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 265daf3acb9632aa92f85962abc44a6a9ea8dfed
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="checklist-implementing-a-web-sso-design"></a>チェックリスト: Web SSO 設計の実装

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

この上位チェックリストには、Web の Active Directory フェデレーション サービス \(AD FS\) \(SSO\) シングル Sign\-の設計に関する重要な概念へのクロス参照リンクが含まれます。 この設計を実装するために必要なタスクを完了するために役立つチェックリストを下位へのリンクも含まれます。  
  
> [!NOTE]  
> 順序でこのチェックリストのタスクを完了します。 参照リンクから概念トピックまたは下位チェックリスト、このトピックに戻り後、概念トピックを参照するか、または下位チェックリストのタスクを完了できるように、このチェックリストの残りのタスクを続行することができます。  
  
![Web sso](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**チェックリスト: Web SSO 設計の実装**  
  
||タスク|リファレンス|  
|-|--------|-------------|  
|![Web sso](media/icon_checkboxo.gif)|Web SSO 設計に関する重要概念を確認し、組織のニーズに合わせて設計のカスタマイズに使用することができますを AD FS 展開目標を決定します。 **注:**|![Web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Web SSO 設計](https://technet.microsoft.com/library/dd807033.aspx)<br /><br />![Web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 展開目標の特定](https://technet.microsoft.com/library/dd807053.aspx)|  
|![Web sso](media/icon_checkboxo.gif)|ハードウェア、ソフトウェア、証明書、ドメイン ネーム システム \(DNS\)、属性ストア、および組織内の AD FS を展開するためのクライアントの要件を確認します。|![Web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[付録 a: 確認 AD FS の要件](https://technet.microsoft.com/library/ff678034.aspx)|  
|![Web sso](media/icon_checkboxo.gif)|設計計画に基づいて、企業ネットワークまたは境界ネットワーク内に 1 つまたは複数のフェデレーション サーバーをインストールします。 **注:** Web SSO 設計が正常に機能する 1 つだけのフェデレーション サーバーが必要です。 1 つのフェデレーション サーバーは、要求プロバイダーの役割と証明書利用者のパーティ役割の両方を受け持ちます。|![Web sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト: フェデレーション サーバーの設定](Checklist--Setting-Up-a-Federation-Server.md)|  
|![Web sso](media/icon_checkboxo.gif)|\(Optional\) かを確認するかどうか、組織は、境界ネットワーク内のフェデレーション サーバー プロキシを必要があります。|![Web sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト:、フェデレーション サーバー プロキシのセットアップの設定](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|  
|![Web sso](media/icon_checkboxo.gif)|Web SSO 設計計画とそれを使用する方法に応じて、適切な属性ストア、証明書利用者の信頼、信頼性情報を追加し、要求規則は、フェデレーション サービスにします。|![Web sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト: アカウント パートナー組織の構成](Checklist--Configuring-the-Account-Partner-Organization.md)|  
|![Web sso](media/icon_checkboxo.gif)|場合は、リソース パートナー組織の管理者は claims\ を有効にする、Web ブラウザー アプリケーション、Web サービス アプリケーション、または Microsoft® Office SharePoint® Server アプリケーションを WIF および WIF SDK を使用します。 **注:**|![Web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation](https://go.microsoft.com/fwlink/?LinkId=122266)<br /><br />![Web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation SDK](https://go.microsoft.com/fwlink/?LinkId=122266)| 
