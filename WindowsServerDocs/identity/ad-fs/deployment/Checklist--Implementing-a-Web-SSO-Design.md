---
ms.assetid: 30657638-5709-48c5-87aa-98f688e07b4c
title: Web SSO 設計の実装のチェックリスト
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: b2e09addbdc192bc6ce93a4402e6a6e61873ad56
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192364"
---
# <a name="checklist-implementing-a-web-sso-design"></a>チェックリスト:Web SSO 設計の実装

この上位チェックリストには、クロスが含まれています\-Web シングルに関する重要な概念へのリンクを参照\-サインオン\-で\(SSO\) Active Directory フェデレーション サービスの設計\(AD FS\). また、この設計を実装するのに必要なタスクの実行を支援する下位チェックリストへのリンクも含まれます。  
  
> [!NOTE]  
> このチェックリストのタスクは順番に実行してください。 参照リンクから概念トピックまたは下位チェックリストが表示される場合は、概念トピックを参照した後または下位チェックリストのタスクを実行した後でこのトピックに戻り、このチェックリストの残りのタスクを実行します。  
  
![web sso](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**チェックリスト。Web SSO 設計の実装**  
  
||タスク|リファレンス|  
|-|--------|-------------|  
|![web sso](media/icon_checkboxo.gif)|Web SSO 設計に関する重要な概念を確認し、組織のニーズに合わせて設計のカスタマイズに使用することができますが AD FS 展開目標を決定します。 **注:** |![web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Web SSO 設計](https://technet.microsoft.com/library/dd807033.aspx)<br /><br />![web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 展開目標の特定](https://technet.microsoft.com/library/dd807053.aspx)|  
|![web sso](media/icon_checkboxo.gif)|ハードウェア、ソフトウェア、証明書、ドメイン ネーム システムを確認して\(DNS\)、属性ストア、および、組織内の AD FS を展開するためのクライアント要件。|![web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[付録 a:AD FS 要件の確認](https://technet.microsoft.com/library/ff678034.aspx)|  
|![web sso](media/icon_checkboxo.gif)|設計計画に基づいて、企業ネットワークまたは境界ネットワーク内に 1 つまたは複数のフェデレーション サーバーをインストールします。 **注:** Web SSO 設計では、正常に機能する 1 つだけのフェデレーション サーバーが必要です。 1 つのフェデレーション サーバーは、要求プロバイダーの役割と証明書利用者のパーティのロールの両方で機能します。|![web sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト。フェデレーション サーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)|  
|![web sso](media/icon_checkboxo.gif)|\(省略可能な\)境界ネットワーク内のフェデレーション サーバー プロキシが組織に必要があるかどうかを判断します。|![web sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト。フェデレーション サーバー プロキシのセットアップ](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|  
|![web sso](media/icon_checkboxo.gif)|Web SSO 設計計画の内容およびその計画をどのように使用するかに応じて、適切な属性ストア、証明書利用者信頼、要求、および要求規則をフェデレーション サービスに追加します。|![web sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト。アカウント パートナー組織の構成](Checklist--Configuring-the-Account-Partner-Organization.md)|  
|![web sso](media/icon_checkboxo.gif)|リソース パートナー組織の管理者の場合は、要求\-Web ブラウザー アプリケーション、Web サービス アプリケーション、または WIF と、WIF SDK を使用して Microsoft® Office SharePoint® Server アプリケーションを有効にします。 **注:** |![web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation](https://go.microsoft.com/fwlink/?LinkId=122266)<br /><br />![web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation SDK](https://go.microsoft.com/fwlink/?LinkId=122266)| 
