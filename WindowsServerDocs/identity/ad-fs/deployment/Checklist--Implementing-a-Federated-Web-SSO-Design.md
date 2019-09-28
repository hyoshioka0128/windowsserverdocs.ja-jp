---
ms.assetid: 6b49cde3-d2cb-4ece-b9b7-dc600e037495
title: チェックリスト-フェデレーション Web SSO 設計の実装
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 165471fd06031a68343a54d019357afee782d082
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359951"
---
# <a name="checklist-implementing-a-federated-web-sso-design"></a>チェックリスト:フェデレーション Web SSO 設計の実装

この親チェックリストには、クロス @ no__t-0reference に関する重要な概念へのリンクが含まれています。これは、Active Directory フェデレーションサービス (AD FS) \(AD FS @ no__t-6 のフェデレーション Web @no__t Single @ no__t の設計に関する重要な概念に関するものです。 また、この設計を実装するのに必要なタスクの実行を支援する下位チェックリストへのリンクも含まれます。  
  
> [!NOTE]  
> このチェックリストのタスクは順番に実行してください。 参照リンクから概念トピックまたは下位チェックリストが表示される場合は、概念トピックを参照した後または下位チェックリストのタスクを実行した後でこのトピックに戻り、このチェックリストの残りのタスクを実行します。  
  
![federated web sso @ no__t-1Checklist リスト:フェデレーション Web SSO 設計の実装**  
  
||タスク|参照|  
|-|--------|-------------|  
|![フェデレーション web sso](media/icon_checkboxo.gif)|フェデレーション Web SSO 設計に関する重要な概念を確認し、組織のニーズに合わせてこの設計をカスタマイズするために使用できる AD FS 展開の目標を決定します。|@no__t 0federated web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション WEB Sso 設計](https://technet.microsoft.com/library/dd807050.aspx)<br /><br />](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS の展開目標を特定する](https://technet.microsoft.com/library/dd807053.aspx)@no__t 0federated web sso<br /><br />![federated web sso の](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[展開の計画](https://technet.microsoft.com/library/dd807083.aspx)|  
|![フェデレーション web sso](media/icon_checkboxo.gif)|組織で AD FS を展開するための、ハードウェア、ソフトウェア、証明書、ドメインネームシステム \(DNS @ no__t、属性ストア、およびクライアントの要件を確認します。|![federated web sso @ no__t-1Appendix A:AD FS 要件の確認](https://technet.microsoft.com/library/ff678034.aspx)|  
|![フェデレーション web sso](media/icon_checkboxo.gif)|両方のパートナー組織に AD FS を展開する前に、要求、要求規則、属性ストア、および AD FS 構成データベースに関する重要な概念を確認します。|@no__t 0federated web sso に関する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[重要な AD FS 概念につい](../../ad-fs/technical-reference/Understanding-Key-AD-FS-Concepts.md)て|  
|![フェデレーション web sso](media/icon_checkboxo.gif)|設計計画に従って、各パートナー組織に1つ以上のフェデレーションサーバーをインストールします。 **注:** フェデレーション Web SSO 設計では、アカウントパートナー組織に少なくとも1つのフェデレーションサーバーと、リソースパートナー組織内に少なくとも1つのフェデレーションサーバーが必要です。|![federated web sso @ no__t-1Checklist リスト:フェデレーション サーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)|  
|![フェデレーション web sso](media/icon_checkboxo.gif)|\(Optional @ no__t-1 組織にフェデレーションサーバープロキシが必要かどうかを決定します。 設計計画でプロキシを呼び出す場合は、各パートナー組織に1つ以上のフェデレーションサーバープロキシをインストールできます。|![federated web sso @ no__t-1Checklist リスト:フェデレーション サーバー プロキシのセットアップ](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|  
|![フェデレーション web sso](media/icon_checkboxo.gif)|設計計画に基づいて、両方のパートナー組織で証明書の共有、クライアントの構成、および信頼関係の構成を行います。これによって、組織間でフェデレーション信頼を介したコミュニケーションが可能になります。|![federated web sso @ no__t-1Checklist リスト:アカウントパートナー組織の構成 @ no__t-0<br /><br />![federated web sso @ no__t-1Checklist リスト:リソースパートナー組織の構成 @ no__t-0|  
|![フェデレーション web sso](media/icon_checkboxo.gif)|リソースパートナー組織の管理者は、WIF と WIF SDK を使用して、Web ブラウザーアプリケーション、Web サービスアプリケーション、または Microsoft® Office SharePoint® Server アプリケーションを有効にします。|![federated web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation](https://go.microsoft.com/fwlink/?LinkId=122266)<br /><br />![federated web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity FOUNDATION SDK](https://go.microsoft.com/fwlink/?LinkId=122266)|  
