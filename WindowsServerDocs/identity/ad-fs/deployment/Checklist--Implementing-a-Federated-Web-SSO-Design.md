---
ms.assetid: 6b49cde3-d2cb-4ece-b9b7-dc600e037495
title: "フェデレーション Web SSO 設計の実装のチェックリスト-"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 1122ee3814f656a7229dc2946d7441d525de5ae2
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="checklist-implementing-a-federated-web-sso-design"></a>チェックリスト: フェデレーション Web SSO 設計の実装

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

この上位チェックリストには、Active Directory フェデレーション サービス \(AD FS\) 用のフェデレーション Web Single\-Sign\-On \(SSO\) 設計に関する重要な概念へのクロス参照リンクが含まれます。 この設計を実装するために必要なタスクを完了するために役立つチェックリストを下位へのリンクも含まれます。  
  
> [!NOTE]  
> 順序でこのチェックリストのタスクを完了します。 参照リンクから概念トピックまたは下位チェックリスト、このトピックに戻り、概念トピックを確認するまたは下位チェックリストのタスクを完了するように、このチェックリストの残りのタスクを続行することができます。  
  
![フェデレーション Web sso](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**チェックリスト: フェデレーション Web SSO 設計の実装**  
  
||タスク|リファレンス|  
|-|--------|-------------|  
|![フェデレーション Web sso](media/icon_checkboxo.gif)|フェデレーション Web SSO 設計に関する重要概念を確認し、組織のニーズに合わせて設計のカスタマイズに使用することができますを AD FS 展開目標を決定します。|![フェデレーション Web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション Web SSO 設計](https://technet.microsoft.com/library/dd807050.aspx)<br /><br />![フェデレーション Web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 展開目標の特定](https://technet.microsoft.com/library/dd807053.aspx)<br /><br />![フェデレーション Web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[展開の計画](https://technet.microsoft.com/library/dd807083.aspx)|  
|![フェデレーション Web sso](media/icon_checkboxo.gif)|ハードウェア、ソフトウェア、証明書、ドメイン ネーム システム \(DNS\)、属性ストア、および組織内の AD FS を展開するためのクライアントの要件を確認します。|![フェデレーション Web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[付録 a: 確認 AD FS の要件](https://technet.microsoft.com/library/ff678034.aspx)|  
|![フェデレーション Web sso](media/icon_checkboxo.gif)|信頼性情報に関する重要概念を確認、両方のパートナー組織内の AD FS を展開する前に、ルール、属性ストア、および AD FS 構成データベースを要求します。|![フェデレーション Web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Understanding Key AD FS Concepts](../../ad-fs/technical-reference/Understanding-Key-AD-FS-Concepts.md)|  
|![フェデレーション Web sso](media/icon_checkboxo.gif)|設計計画に基づいて、各パートナー組織に 1 つまたは複数のフェデレーション サーバーをインストールします。 **注:**フェデレーション Web SSO 設計では、アカウント パートナー組織内の少なくとも 1 つのフェデレーション サーバーとリソース パートナー組織内の少なくとも 1 つのフェデレーション サーバーが必要です。|![フェデレーション Web sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト: フェデレーション サーバーの設定](Checklist--Setting-Up-a-Federation-Server.md)|  
|![フェデレーション Web sso](media/icon_checkboxo.gif)|\(Optional\) かを確認するかどうか、組織がフェデレーション サーバー プロキシ必要があります。 設計計画のプロキシの場合、各パートナー組織に 1 つまたは複数のフェデレーション サーバー プロキシをインストールできます。|![フェデレーション Web sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト:、フェデレーション サーバー プロキシのセットアップの設定](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|  
|![フェデレーション Web sso](media/icon_checkboxo.gif)|設計計画に基づいて証明書の共有、クライアントの構成およびフェデレーション信頼を介した通信できるようにする、両方のパートナー組織で信頼関係を構成します。|![フェデレーション Web sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト: アカウント パートナー組織の構成](Checklist--Configuring-the-Account-Partner-Organization.md)<br /><br />![フェデレーション Web sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト: リソース パートナー組織の構成](Checklist--Configuring-the-Resource-Partner-Organization.md)|  
|![フェデレーション Web sso](media/icon_checkboxo.gif)|場合は、リソース パートナー組織の管理者は claims\ を有効にする、Web ブラウザー アプリケーション、Web サービス アプリケーション、または Microsoft® Office SharePoint® Server アプリケーションを WIF および WIF SDK を使用します。|![フェデレーション Web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation](https://go.microsoft.com/fwlink/?LinkId=122266)<br /><br />![フェデレーション Web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation SDK](https://go.microsoft.com/fwlink/?LinkId=122266)|  
