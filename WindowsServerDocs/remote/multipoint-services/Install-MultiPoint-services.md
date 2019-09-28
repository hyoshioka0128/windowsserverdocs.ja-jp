---
title: MultiPoint Services をインストールする
description: Windows Server 2016 で MultiPoint Services をインストールして構成する方法について説明します。
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f6f8970b-de3f-4255-b2a1-5472a16ed02f
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 442699afe40ee67e4cd4f13572d1a482f675b84a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71395383"
---
# <a name="install-multipoint-services"></a>MultiPoint Services をインストールする
サーバーを最初からインストールする場合は、次の手順に従って MultiPoint Services をインストールします。  

Windows Server 2016 をインストールした後、管理者として正常にサインインします。 サーバーマネージャーを使用して、MultiPoint Services を有効にすることができます。 サーバーマネージャーは起動時に自動的に開きます。 ダッシュボードで、 **[役割と機能の追加]** を選択して MultiPoint Services を有効にし、ウィザードの指示に従います。

インストールの種類については、「」を参照してください。 
- 役割ベースまたは機能ベースのインストールまたは
- リモートデスクトップサービスのインストール

標準の MultiPoint サービスの展開では、[展開の種類] で MultiPoint Services の役割を選択できるように、リモートデスクトップサービスインストールを選択することをお勧めします。 ロールベースのインストールでは、ロールの一覧で**MultiPoint Services**を選択する必要があります。 インストールが正常に終了すると、サーバーが再起動します。  
  
## <a name="configure-your-primary-station"></a>プライマリステーションの構成  
  
1.  **[MultiPoint Server ステーションの作成]** ページで、指定した文字をそのモニターのキーボードから入力します。 正しいキーエントリによって、そのステーションにキーボードとマウスが関連付けられます。  
2.  管理者としてサインインします。  