---
title: ホスト型キャッシュ サーバーでコンテンツの事前ハッシュと事前読み込みを行う (省略可能)
description: このガイドでは、Windows Server 2016 および Windows 10 を実行するコンピューターでホスト型キャッシュ モードで BranchCache の展開の説明
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: 7e79c66a-8555-4d8e-8691-d6c37377aab4
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b60a1f24b8988d6e394df0faf678467021e0c882
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839393"
---
# <a name="prehash-and-preload-content-on-the-hosted-cache-server-optional"></a>Prehash し、ホスト型キャッシュ サーバー上のコンテンツをプリロード\(オプション\)

>適用対象:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このセクションでは、プロシージャを使用するには、コンテンツ サーバーでコンテンツを prehash やデータ パッケージ、コンテンツを追加し、ホスト型キャッシュ サーバーにコンテンツをプリロードします。 

これらの手順はないため、コンテンツを prehash しプリロードするために必要で、ホスト型キャッシュ サーバー オプションです。 

コンテンツをあらかじめロードする場合データ ホスト型キャッシュを自動的に追加されますクライアントが WAN 接続経由でダウンロードするとします。

>[!IMPORTANT]
>これらの手順はまとめてオプションで、ホスト型キャッシュ サーバーでコンテンツを prehash しプリロードする場合は、両方の手順を実行するが必要です。

- [Web コンテンツ サーバーのデータ パッケージを作成し、ファイル コンテンツ&#40;オプション&#41;](8-Bc-Data-Packages.md)
  
- [ホスト型キャッシュ サーバー上のデータ パッケージをインポート&#40;オプション&#41;](9-Bc-Import-Data.md)

このガイドを続行する、次を参照してください。 [Web およびファイルのコンテンツのコンテンツ サーバー データのパッケージを作成&#40;(省略可能)&#41;](8-Bc-Data-Packages.md)します。