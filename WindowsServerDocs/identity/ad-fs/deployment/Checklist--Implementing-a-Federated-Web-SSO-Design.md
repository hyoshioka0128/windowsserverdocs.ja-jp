---
ms.assetid: 6b49cde3-d2cb-4ece-b9b7-dc600e037495
title: チェックリスト-フェデレーション Web SSO 設計の実装
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: e3c9f94ee1ce1e1fef2429a12fdb77604987fdb8
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2020
ms.locfileid: "87520041"
---
# <a name="checklist-implementing-a-federated-web-sso-design"></a>チェックリスト: フェデレーション Web SSO 設計の実装

この親チェックリスト \- には、 \- \- \( \) Active Directory フェデレーションサービス (AD FS) AD FS 向けのフェデレーション Web シングルサインオン SSO 設計に \( 関する重要な概念への相互参照リンクが記載されてい \) ます。 また、この設計を実装するのに必要なタスクの実行を支援する下位チェックリストへのリンクも含まれます。

> [!NOTE]
> このチェックリストのタスクは順番に実行してください。 参照リンクから概念トピックまたは下位チェックリストが表示される場合は、概念トピックを参照した後または下位チェックリストのタスクを実行した後でこのトピックに戻り、このチェックリストの残りのタスクを実行します。

![フェデレーション web sso](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**のチェックリスト: フェデレーション WEB Sso 設計の実装**

|タスク|リファレンス|
|--------|-------------|
|フェデレーション Web SSO 設計に関する重要な概念を確認し、組織のニーズに合わせてこの設計をカスタマイズするために使用できる AD FS 展開の目標を決定します。|![フェデレーション web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション WEB sso の設計](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807050(v=ws.11))<p>![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS の展開目標を特定する](../design/identifying-your-ad-fs-deployment-goals.md)フェデレーション web sso<p>![フェデレーション web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[の展開の計画](../design/planning-your-deployment.md)|
|組織に AD FS を展開するための、ハードウェア、ソフトウェア、証明書、ドメインネームシステム \( DNS \) 、属性ストア、およびクライアントの要件を確認します。|![フェデレーション web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[付録 a: AD FS の要件の確認](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ff678034(v=ws.11))|
|両方のパートナー組織に AD FS を展開する前に、要求、要求規則、属性ストア、および AD FS 構成データベースに関する重要な概念を確認します。|![フェデレーション web sso に関する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[重要な AD FS の概念につい](../../ad-fs/technical-reference/Understanding-Key-AD-FS-Concepts.md)て|
|設計計画に従って、各パートナー組織に1つ以上のフェデレーションサーバーをインストールします。 **注:** フェデレーション Web SSO 設計では、アカウントパートナー組織に少なくとも1つのフェデレーションサーバーと、リソースパートナー組織内に少なくとも1つのフェデレーションサーバーが必要です。|![フェデレーション web sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト: フェデレーションサーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)|
|\(\)必要に応じて、組織にフェデレーションサーバープロキシが必要かどうかを決定します。 設計計画でプロキシを呼び出す場合は、各パートナー組織に1つ以上のフェデレーションサーバープロキシをインストールできます。|![フェデレーション web sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト: フェデレーションサーバープロキシの設定](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|
|設計計画に基づいて、両方のパートナー組織で証明書の共有、クライアントの構成、および信頼関係の構成を行います。これによって、組織間でフェデレーション信頼を介したコミュニケーションが可能になります。|![フェデレーション web sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト: アカウントパートナー組織の構成](Checklist--Configuring-the-Account-Partner-Organization.md)<p>![フェデレーション web sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト: リソースパートナー組織の構成](Checklist--Configuring-the-Resource-Partner-Organization.md)|
|リソースパートナー組織の管理者である場合は、 \- &reg; &reg; WIF と WIF SDK を使用して、web ブラウザーアプリケーション、web サービスアプリケーション、または Microsoft Office SharePoint Server アプリケーションを要求することができます。|![フェデレーション web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation](https://go.microsoft.com/fwlink/?LinkId=122266)<p>![フェデレーション web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity FOUNDATION SDK](https://go.microsoft.com/fwlink/?LinkId=122266)|
