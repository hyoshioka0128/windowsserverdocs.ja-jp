---
title: ネットワークポリシーサーバーのユーザーデータコレクション
description: Windows Server 2016 のネットワークポリシーサーバーによってユーザーを認証するためにどのような情報が使用されます。
author: MicrosoftGuyJFlo
manager: mtillman
ms.author: joflore
ms.reviewer: richagi
ms.custom: it-pro
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.date: 05/01/2018
ms.openlocfilehash: def65c174ff608301f8d4f35ef1ce19818103e61
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859375"
---
# <a name="network-policy-server-user-data-collection"></a>ネットワークポリシーサーバーのユーザーデータコレクション

このドキュメントでは、ネットワークポリシーサーバー (NPS) によって収集されたユーザー情報を削除したい場合に、その情報を検索する方法について説明します。

>[!Note]
>個人データの表示や削除に関心がある場合は、「 [GDPR サイトの Windows データ主体の要求](https://docs.microsoft.com/microsoft-365/compliance/gdpr-dsr-windows)」に記載されているマイクロソフトのガイダンスを参照してください。 GDPR に関する一般情報をお探しの場合は、 [Service Trust portal の GDPR セクション](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted)を参照してください。

## <a name="information-collected-by-nps"></a>NPS によって収集された情報

- [タイムスタンプ]
- イベントのタイムスタンプ
- Username
- 完全修飾ユーザー名
- クライアント IP アドレス
- クライアント ベンダー
- クライアントのフレンドリ名
- [認証の種類]
- RADIUS プロトコルに関する他の多くのフィールド

## <a name="gather-data-from-nps"></a>NPS からデータを収集する

アカウンティングデータが有効で構成されている場合は、構成に応じて、SQL Server またはログファイルからユーザーの NPS 認証試行のレコードを取得できます。 

アカウンティングデータが SQL Server 用に構成されている場合は、User_Name = `'<username>'`れるすべてのレコードに対してクエリを実行します。

アカウンティングデータがログファイルに対して構成されている場合は、ログファイルで `<username>` を検索して、すべてのログエントリを検索します。

ネットワークポリシーとアクセスサービスのイベントログエントリは、アカウンティングデータにマルチ商法と見なされ、収集する必要はありません。

アカウンティングデータが有効になっていない場合は、ネットワークポリシーとアクセスサービスのイベントログから、`<username>`を検索することによって、ユーザーの NPS 認証試行のレコードを取得できます。
