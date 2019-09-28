---
title: ファイル共有を有効にします。
description: MultiPoint Services でのファイル共有について説明します。
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 508ad056-8e0c-4d59-a4fa-05775a54125d
author: evaseydl
ms.author: evas
manager: Scottman
ms.openlocfilehash: aff6501d129696fd78d58bdac52f5a4a9ef54c63
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71395454"
---
# <a name="enable-file-sharing-in-multipoint-services"></a>MultiPoint Services でファイル共有を有効にする
MultiPoint ステーションのユーザーがファイルを共有できるようにするには、次の2つの方法があります。  
  
-   **ネットワーク上にファイルサーバーがある場合は、** ファイルサーバー上に共有フォルダーを作成することをお勧めします。  
  
-   **専用のファイルサーバーを使用せずに、2-3 multipoint サーバーの小規模なネットワークを使用している場合**は、multipoint services を実行している残りのすべてのコンピューターのファイルサーバーとして、いずれかの multipoint サーバーを使用できます。 そのサーバー上に共有フォルダーを作成し、そのサーバー上のすべてのユーザーに対してローカルユーザーアカウントを作成します。 共有フォルダーは、元の内部ドライブに配置することも、コンピューターに内蔵または外部のドライブを追加することもできます。  
  
