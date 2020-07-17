---
title: ファイル共有を有効にします。
description: MultiPoint Services でのファイル共有について説明します。
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: 508ad056-8e0c-4d59-a4fa-05775a54125d
author: evaseydl
ms.author: evas
manager: Scottman
ms.openlocfilehash: 73f89700228d912ac029a97dc3951be21a01e45a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859265"
---
# <a name="enable-file-sharing-in-multipoint-services"></a>MultiPoint Services でファイル共有を有効にする
MultiPoint ステーションのユーザーがファイルを共有できるようにするには、次の2つの方法があります。  
  
-   **ネットワーク上にファイルサーバーがある場合は、** ファイルサーバー上に共有フォルダーを作成することをお勧めします。  
  
-   **専用のファイルサーバーを使用せずに、2-3 multipoint サーバーの小規模なネットワークを使用している場合**は、multipoint services を実行している残りのすべてのコンピューターのファイルサーバーとして、いずれかの multipoint サーバーを使用できます。 そのサーバー上に共有フォルダーを作成し、そのサーバー上のすべてのユーザーに対してローカルユーザーアカウントを作成します。 共有フォルダーは、元の内部ドライブに配置することも、コンピューターに内蔵または外部のドライブを追加することもできます。  
  
