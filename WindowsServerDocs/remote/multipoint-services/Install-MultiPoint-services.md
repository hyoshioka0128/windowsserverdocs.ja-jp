---
title: MultiPoint Services をインストールする
description: インストールして Windows Server 2016 で MultiPoint Services を構成する方法について説明します
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f6f8970b-de3f-4255-b2a1-5472a16ed02f
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 52a824bbca3e9f2e1c7823601f6208ae19ae50ef
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866223"
---
# <a name="install-multipoint-services"></a>MultiPoint Services をインストールする
最初からサーバーをインストールする場合は MultiPoint Services をインストールする手順に従います。  

Windows Server 2016 を正常にインストールした後、管理者としてサインインします。 MultiPoint Services を有効にした場所、サーバー マネージャーを使用します。 サーバー マネージャーは、起動時に自動的に開きます。 [ダッシュ ボードの選択]**役割と機能の追加**を MultiPoint Services を有効にし、ウィザードの指示に従います。

インストールの種類のセクションでいずれかで移動が、 
- 役割ベースまたは機能ベースのインストールまたは
- リモート デスクトップ サービスのインストール

MultiPoint サービスを配置する標準的な展開の種類 MultiPoint サービスの役割を簡単に選択できるリモート デスクトップ サービスのインストールを選択します。 はお勧めします。 役割に基づいたインストールを選択する必要があります**MultiPoint Services**でロールの一覧。 インストールの成功後、サーバーが再起動します。  
  
## <a name="configure-your-primary-station"></a>プライマリ ステーションを構成します。  
  
1.  **MultiPoint Server ステーションを作成**ページで、そのモニターのキーボードから指定した文字を入力します。 正しいキー エントリでは、そのステーションのマウスとキーボードを関連付けます。  
2.  管理者としてサインインします。  