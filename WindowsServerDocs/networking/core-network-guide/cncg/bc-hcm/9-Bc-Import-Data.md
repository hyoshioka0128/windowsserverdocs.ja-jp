---
title: ホスト型キャッシュ サーバーでデータ パッケージをインポートする (省略可能)
description: このガイドでは、Windows Server 2016 および Windows 10 を実行するコンピューターでホスト型キャッシュ モードで BranchCache の展開の説明
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: d6159e91-f77c-42ec-9180-14bbb230ad17
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 440ef1e04143cba09213ffea634aa9d4fea51dab
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888003"
---
# <a name="import-data-packages-on-the-hosted-cache-server-optional"></a>ホスト型キャッシュ サーバー上のデータ パッケージをインポート\(オプション\)

>適用対象:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

データ パッケージをインポートし、ホスト型キャッシュ サーバーのコンテンツをプリロードするこの手順を使用することができます。

この手順はないため、コンテンツを prehash しプリロードするために必要で、ホスト型キャッシュ サーバー省略可能です。

前ではない操作を行う場合\-ロード コンテンツ、データは自動的にこのホスト型キャッシュに追加のクライアントが WAN 接続経由でダウンロードするとします。

この手順を実行する管理者グループのメンバーがあります。

## <a name="to-import-data-packages-on-the-hosted-cache-server"></a>ホスト型キャッシュ サーバー上のパッケージ データをインポートするには  

1. サーバー コンピューターには、管理者特権で Windows PowerShell を開きます。

2. 値を置き換えて、次のコマンドを入力: パス パラメーターには、フォルダーの場所で、データ パッケージが格納されているし、ENTER キーを押します。

    ```  
    Import-BCCachePackage –Path D:\temp\PeerDistPackage.zip
    ```  

3. コンテンツをプリロードする 1 つ以上のホスト型キャッシュ サーバーがあれば、各のホスト型キャッシュ サーバーでこの手順を実行します。

このガイドを続行する、次を参照してください。[構成クライアント自動ホストされるキャッシュの検出サービス接続ポイントによる](10-Bc-Client-By-Scp.md)します。
