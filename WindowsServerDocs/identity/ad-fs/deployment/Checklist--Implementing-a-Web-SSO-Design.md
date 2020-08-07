---
ms.assetid: 30657638-5709-48c5-87aa-98f688e07b4c
title: チェックリスト-Web SSO 設計の実装
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.author: billmath
ms.openlocfilehash: 965cadc9f1e9036c2d4023478e1a4ce82a4996c1
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87945529"
---
# <a name="checklist-implementing-a-web-sso-design"></a>チェックリスト:Web SSO 設計の実装

この親チェックリストには \- 、 \- \- \( \) Active Directory フェデレーションサービス (AD FS) AD FS 向けの Web シングルサインオン SSO 設計に \( 関する重要な概念への相互参照リンクが含まれてい \) ます。 また、この設計を実装するのに必要なタスクの実行を支援する下位チェックリストへのリンクも含まれます。

> [!NOTE]
> このチェックリストのタスクは順番に実行してください。 参照リンクから概念トピックまたは下位チェックリストが表示される場合は、概念トピックを参照した後または下位チェックリストのタスクを実行した後でこのトピックに戻り、このチェックリストの残りのタスクを実行します。

![web sso](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**のチェックリスト: WEB Sso 設計の実装**

|タスク|リファレンス|
|--------|-------------|
|Web SSO 設計に関する重要な概念を確認し、組織のニーズに合わせてこの設計をカスタマイズするために使用できる AD FS 展開の目標を決定します。 **注:**|![web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[web](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807033(v=ws.11)) Sso の設計<p>![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS のデプロイ目標を特定する](../design/identifying-your-ad-fs-deployment-goals.md)web sso|
|組織に AD FS を展開するための、ハードウェア、ソフトウェア、証明書、ドメインネームシステム \( DNS \) 、属性ストア、およびクライアントの要件を確認します。|![web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[付録 a: AD FS の要件の確認](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ff678034(v=ws.11))|
|設計計画に従って、企業ネットワークまたは境界ネットワークに1つ以上のフェデレーションサーバーをインストールします。 **注:** Web SSO の設計では、正常に機能するには1つのフェデレーションサーバーのみが必要です。 単一のフェデレーションサーバーは、要求プロバイダーの役割と証明書利用者の役割の両方で動作します。|![web sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト: フェデレーションサーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)|
|\((省略可能) \) 組織が境界ネットワークにフェデレーションサーバープロキシを必要とするかどうかを決定します。|![web sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト: フェデレーションサーバープロキシの設定](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|
|Web SSO 設計計画の内容およびその計画をどのように使用するかに応じて、適切な属性ストア、証明書利用者信頼、要求、および要求規則をフェデレーション サービスに追加します。|![web sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト: アカウントパートナー組織の構成](Checklist--Configuring-the-Account-Partner-Organization.md)|
|リソースパートナー組織の管理者である場合は、 \- &reg; &reg; WIF と WIF SDK を使用して、web ブラウザーアプリケーション、web サービスアプリケーション、または Microsoft Office SharePoint Server アプリケーションを要求することができます。 **注:**|![web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation](https://go.microsoft.com/fwlink/?LinkId=122266)<p>![web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity FOUNDATION SDK](https://go.microsoft.com/fwlink/?LinkId=122266)|
