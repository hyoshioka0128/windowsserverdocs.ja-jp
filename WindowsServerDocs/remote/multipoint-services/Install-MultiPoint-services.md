---
title: MultiPoint サービスをインストールします。
description: Windows Server 2016 で MultiPoint Services をインストールして構成する方法について説明します。
ms.date: 07/22/2016
ms.topic: article
ms.assetid: f6f8970b-de3f-4255-b2a1-5472a16ed02f
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: b1148c8261e97a5cb3c839337a64442520744827
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87970669"
---
# <a name="install-multipoint-services"></a>MultiPoint サービスをインストールします。
サーバーを最初からインストールする場合は、次の手順に従って MultiPoint Services をインストールします。

Windows Server 2016 をインストールした後、管理者として正常にサインインします。 サーバーマネージャーを使用して、MultiPoint Services を有効にすることができます。 サーバーマネージャーは起動時に自動的に開きます。 ダッシュボードで、[**役割と機能の追加**] を選択して MultiPoint Services を有効にし、ウィザードの指示に従います。

インストールの種類については、「」を参照してください。
- 役割ベースまたは機能ベースのインストールまたは
- リモート デスクトップ サービスのインストール

標準の MultiPoint サービスの展開では、[展開の種類] で MultiPoint Services の役割を選択できるように、リモートデスクトップサービスインストールを選択することをお勧めします。 ロールベースのインストールでは、ロールの一覧で**MultiPoint Services**を選択する必要があります。 インストールが正常に終了すると、サーバーが再起動します。

## <a name="configure-your-primary-station"></a>プライマリステーションの構成

1.  [ **MultiPoint Server ステーションの作成**] ページで、指定した文字をそのモニターのキーボードから入力します。 正しいキーエントリによって、そのステーションにキーボードとマウスが関連付けられます。
2.  管理者としてサインインします。