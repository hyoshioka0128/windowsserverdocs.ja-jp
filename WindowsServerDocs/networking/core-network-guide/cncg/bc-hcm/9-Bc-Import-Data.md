---
title: (省略可能) ホスト型キャッシュ サーバー上のデータ パッケージをインポートします。
description: このガイドでは、Windows Server 2016 および Windows 10 を実行するコンピューターでホスト型キャッシュ モードで BranchCache を展開するの説明
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: d6159e91-f77c-42ec-9180-14bbb230ad17
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e0bd8f12ab76c8e2bf03ba79ce46a4cbea2f4dc5
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="import-data-packages-on-the-hosted-cache-server-optional"></a>ホストされているデータ パッケージをインポート サーバー \(Optional\) のキャッシュ

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

この手順を使用するとデータのパッケージをインポートして、ホスト型キャッシュ サーバーでコンテンツをプリロードすることができます。

必要はありません prehash およびプリロード コンテンツをホスト型キャッシュ サーバーでこの手順は省略可能です。

ファイルの読み込みコンテンツではなくする場合は、データが、ホスト型キャッシュを自動的に追加ようにクライアントが WAN 接続経由でダウンロードします。

この手順を実行する管理者グループのメンバーがあります。

## <a name="to-import-data-packages-on-the-hosted-cache-server"></a>ホスト型キャッシュ サーバー上のデータ パッケージをインポートするには  

1. サーバーのコンピューターでは、管理者特権で Windows PowerShell を開きます。

2. 値を置換、次のコマンドを入力 – Path パラメーターに、フォルダーの場所、データ パッケージを保存し、ENTER キーを押します。

    ```  
    Import-BCCachePackage –Path D:\temp\PeerDistPackage.zip
    ```  

3. コンテンツをプリロードする 1 つ以上のホスト型キャッシュ サーバーがあれば、各ホスト型キャッシュ サーバーでこの手順を実行します。

このガイドでは、続行するのを参照してください。[構成クライアント自動ホストされるキャッシュの検出サービス接続ポイントによる](10-Bc-Client-By-Scp.md)します。
