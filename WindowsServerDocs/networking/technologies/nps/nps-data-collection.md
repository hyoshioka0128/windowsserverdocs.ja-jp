---
title: ネットワーク ポリシー サーバーのユーザー データの収集
description: どのような情報は、Windows Server 2016 でネットワーク ポリシー サーバーによってユーザーを認証するために使用されます。
author: MicrosoftGuyJFlo
manager: mtillman
ms.author: joflore
ms.reviewer: richagi
ms.custom: it-pro
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: ''
ms.date: 05/01/2018
ms.openlocfilehash: 5bddd22c9c2f954435cc6ce37347d18c76ee7de3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888743"
---
# <a name="network-policy-server-user-data-collection"></a>ネットワーク ポリシー サーバーのユーザー データの収集

このドキュメントでは、それを削除するには、イベントによって、ネットワーク ポリシー サーバー (NPS) が収集されるユーザー情報を検索する方法について説明します。

>[!Note]
>表示または個人データの削除で知りたい場合は、Microsoft のガイダンスを確認してください、 [Windows gdpr データ主体の要求](https://docs.microsoft.com/microsoft-365/compliance/gdpr-dsr-windows)サイト。 GDPR に関する一般的な情報を探している場合を参照してください、 [Service Trust portal の GDPR セクション](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted)します。

## <a name="information-collected-by-nps"></a>NPS で収集される情報

- Timestamp
- イベントのタイムスタンプ
- Username
- 完全修飾されたユーザー名
- クライアントの IP アドレス
- クライアント ベンダー
- クライアントのフレンドリ名
- [認証の種類]
- RADIUS プロトコルに関するその他の多数のフィールド

## <a name="gather-data-from-nps"></a>NPS からデータを収集します。

アカウンティング データが有効にし、構成、ユーザーの NPS の認証試行のレコードは SQL Server または構成によってログ ファイルから取得できます。 

すべてのクエリが、User_Name をレコードでアカウンティング データを SQL Server を構成すると、場合 =`'<username>'`します。

アカウンティング データは、ログ ファイルで構成された場合は、ログ ファイルを検索し、`<username>`すべてのログ エントリを検索します。

ネットワーク ポリシーとアクセス サービスのイベント ログ エントリは、アカウンティング データ商法と見なされます、収集する必要はありません。

アカウンティング データが有効でないかどうかは、ユーザーの NPS の認証試行のレコードは、検索することによって、ネットワーク ポリシーとアクセス サービス イベント ログから取得できます、`<username>`します。
