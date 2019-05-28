---
ms.assetid: 6b49cde3-d2cb-4ece-b9b7-dc600e037495
title: フェデレーション Web SSO 設計の実装のチェックリスト
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 1f7a65687ac07c9f7d9a814b50c4090c70817b4f
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192368"
---
# <a name="checklist-implementing-a-federated-web-sso-design"></a>チェックリスト:フェデレーション Web SSO 設計の実装

この上位チェックリストには、クロスが含まれています\-フェデレーション Web シングルに関する重要な概念へのリンクを参照\-サインオン\-で\(SSO\) Active Directory フェデレーション サービスデザイン\(AD FS\)します。 また、この設計を実装するのに必要なタスクの実行を支援する下位チェックリストへのリンクも含まれます。  
  
> [!NOTE]  
> このチェックリストのタスクは順番に実行してください。 参照リンクから概念トピックまたは下位チェックリストが表示される場合は、概念トピックを参照した後または下位チェックリストのタスクを実行した後でこのトピックに戻り、このチェックリストの残りのタスクを実行します。  
  
![フェデレーション web sso](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**チェックリスト。フェデレーション Web SSO 設計の実装**  
  
||タスク|リファレンス|  
|-|--------|-------------|  
|![フェデレーション web sso](media/icon_checkboxo.gif)|フェデレーション Web SSO 設計に関する重要な概念を確認し、組織のニーズに合わせて設計のカスタマイズに使用することができますが AD FS 展開目標を決定します。|![フェデレーション web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション Web SSO 設計](https://technet.microsoft.com/library/dd807050.aspx)<br /><br />![フェデレーション web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 展開目標の特定](https://technet.microsoft.com/library/dd807053.aspx)<br /><br />![フェデレーション web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[展開の計画](https://technet.microsoft.com/library/dd807083.aspx)|  
|![フェデレーション web sso](media/icon_checkboxo.gif)|ハードウェア、ソフトウェア、証明書、ドメイン ネーム システムを確認して\(DNS\)、属性ストア、および、組織内の AD FS を展開するためのクライアント要件。|![フェデレーション web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[付録 a:AD FS 要件の確認](https://technet.microsoft.com/library/ff678034.aspx)|  
|![フェデレーション web sso](media/icon_checkboxo.gif)|要求に関する重要な概念を確認して、両方のパートナー組織で AD FS を展開する前に、ルール、属性ストア、および AD FS 構成データベースを要求します。|![フェデレーション web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Understanding Key AD FS Concepts](../../ad-fs/technical-reference/Understanding-Key-AD-FS-Concepts.md)|  
|![フェデレーション web sso](media/icon_checkboxo.gif)|設計計画に基づいて、各パートナー組織の 1 つまたは複数のフェデレーション サーバーをインストールします。 **注:** フェデレーション Web SSO 設計には、アカウント パートナー組織内の少なくとも 1 つのフェデレーション サーバーとリソース パートナー組織内の少なくとも 1 つのフェデレーション サーバーが必要です。|![フェデレーション web sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト。フェデレーション サーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)|  
|![フェデレーション web sso](media/icon_checkboxo.gif)|\(省略可能な\)組織がフェデレーション サーバー プロキシが必要かどうかを判断します。 プロキシの場合、設計計画は、各パートナー組織に 1 つまたは複数のフェデレーション サーバー プロキシをインストールできます。|![フェデレーション web sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト。フェデレーション サーバー プロキシのセットアップ](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|  
|![フェデレーション web sso](media/icon_checkboxo.gif)|設計計画に基づいて、両方のパートナー組織で証明書の共有、クライアントの構成、および信頼関係の構成を行います。これによって、組織間でフェデレーション信頼を介したコミュニケーションが可能になります。|![フェデレーション web sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト。アカウント パートナー組織の構成](Checklist--Configuring-the-Account-Partner-Organization.md)<br /><br />![フェデレーション web sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト。リソース パートナー組織の構成](Checklist--Configuring-the-Resource-Partner-Organization.md)|  
|![フェデレーション web sso](media/icon_checkboxo.gif)|リソース パートナー組織の管理者の場合は、要求\-Web ブラウザー アプリケーション、Web サービス アプリケーション、または WIF と、WIF SDK を使用して Microsoft® Office SharePoint® Server アプリケーションを有効にします。|![フェデレーション web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation](https://go.microsoft.com/fwlink/?LinkId=122266)<br /><br />![フェデレーション web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation SDK](https://go.microsoft.com/fwlink/?LinkId=122266)|  
