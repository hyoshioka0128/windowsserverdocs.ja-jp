---
ms.assetid: 30657638-5709-48c5-87aa-98f688e07b4c
title: チェックリスト-Web SSO 設計の実装
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 8488e0c9195930374aacd959e72d0eff34142ca7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408463"
---
# <a name="checklist-implementing-a-web-sso-design"></a>チェックリスト:Web SSO 設計の実装

この親チェックリストには、クロス @ no__t-0reference に関する重要な概念へのリンクが含まれています。これは、Active Directory フェデレーションサービス (AD FS) \(AD FS @ no__t-6 の Web 単一 @ no__t-1 Sign @ @no__t no__t の設計に関する重要な概念に関するものです。 また、この設計を実装するのに必要なタスクの実行を支援する下位チェックリストへのリンクも含まれます。  
  
> [!NOTE]  
> このチェックリストのタスクは順番に実行してください。 参照リンクから概念トピックまたは下位チェックリストが表示される場合は、概念トピックを参照した後または下位チェックリストのタスクを実行した後でこのトピックに戻り、このチェックリストの残りのタスクを実行します。  
  
![web sso @ no__t-1 チェックリスト:Web SSO 設計の実装**  
  
||タスク|参照|  
|-|--------|-------------|  
|![web sso](media/icon_checkboxo.gif)|Web SSO 設計に関する重要な概念を確認し、組織のニーズに合わせてこの設計をカスタマイズするために使用できる AD FS 展開の目標を決定します。 **注:**|@no__t 0web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[WEB sso の設計](https://technet.microsoft.com/library/dd807033.aspx)<br /><br />](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS の展開目標を特定する](https://technet.microsoft.com/library/dd807053.aspx)@no__t 0web sso|  
|![web sso](media/icon_checkboxo.gif)|組織で AD FS を展開するための、ハードウェア、ソフトウェア、証明書、ドメインネームシステム \(DNS @ no__t、属性ストア、およびクライアントの要件を確認します。|![web sso @ no__t-1Appendix A:AD FS 要件の確認](https://technet.microsoft.com/library/ff678034.aspx)|  
|![web sso](media/icon_checkboxo.gif)|設計計画に従って、企業ネットワークまたは境界ネットワークに1つ以上のフェデレーションサーバーをインストールします。 **注:** Web SSO の設計では、正常に機能するには1つのフェデレーションサーバーのみが必要です。 単一のフェデレーションサーバーは、要求プロバイダーの役割と証明書利用者の役割の両方で動作します。|![web sso @ no__t-1 チェックリスト:フェデレーション サーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)|  
|![web sso](media/icon_checkboxo.gif)|\(Optional @ no__t-1: 組織が境界ネットワークにフェデレーションサーバープロキシを必要とするかどうかを決定します。|![web sso @ no__t-1 チェックリスト:フェデレーション サーバー プロキシのセットアップ](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|  
|![web sso](media/icon_checkboxo.gif)|Web SSO 設計計画の内容およびその計画をどのように使用するかに応じて、適切な属性ストア、証明書利用者信頼、要求、および要求規則をフェデレーション サービスに追加します。|![web sso @ no__t-1 チェックリスト:アカウントパートナー組織の構成 @ no__t-0|  
|![web sso](media/icon_checkboxo.gif)|リソースパートナー組織の管理者は、WIF と WIF SDK を使用して、Web ブラウザーアプリケーション、Web サービスアプリケーション、または Microsoft® Office SharePoint® Server アプリケーションを有効にします。 **注:**|![web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation](https://go.microsoft.com/fwlink/?LinkId=122266)<br /><br />![web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity FOUNDATION SDK](https://go.microsoft.com/fwlink/?LinkId=122266)| 
