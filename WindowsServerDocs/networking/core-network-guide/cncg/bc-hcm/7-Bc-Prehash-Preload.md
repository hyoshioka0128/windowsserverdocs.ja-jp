---
title: プリハッシュし、プリロード (オプション) ホスト型キャッシュ サーバー上のコンテンツ
description: このガイドでは、Windows Server 2016 および Windows 10 を実行するコンピューターでホスト型キャッシュ モードで BranchCache を展開するの説明
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: 7e79c66a-8555-4d8e-8691-d6c37377aab4
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0e7ffaac4e427222d5539195ecef91768f61c4a3
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="prehash-and-preload-content-on-the-hosted-cache-server-optional"></a>ハッシュし、コンテンツを事前読み込みで、ホスト型キャッシュ サーバー \(Optional\)

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このセクションの手順を使用するには、コンテンツ サーバーでコンテンツを prehash、データのパッケージにコンテンツを追加して、ホスト型キャッシュ サーバーでコンテンツをプリロードします。 

必要があるためしないコンテンツを prehash しプリロードする、ホスト型キャッシュ サーバーで、これらの手順は省略できます。 

コンテンツをあらかじめロードする場合データが、ホスト型キャッシュを自動的に追加ようにクライアントが WAN 接続経由でダウンロードします。

>[!IMPORTANT]
>これらの手順をまとめてオプションですが、コンテンツを prehash しプリロードする、ホスト型キャッシュ サーバーを選択する場合は、両方の手順を実行するが必要です。

- [Web およびファイルの内容 (&) #40; のコンテンツ サーバー データ パッケージを作成するオプション (& a) #41 です。](8-Bc-Data-Packages.md)
  
- [ホスト型キャッシュ サーバー (&) #40; でデータ パッケージをインポートするオプション (& a) #41 です。](9-Bc-Import-Data.md)

このガイドでは、続行するのを参照してください。[作成用のコンテンツ サーバー データ パッケージ Web およびファイルのコンテンツ (&) #40";"オプション"&"#41 です。](8-Bc-Data-Packages.md).