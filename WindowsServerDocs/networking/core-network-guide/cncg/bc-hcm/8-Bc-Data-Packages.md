---
title: Web およびファイル コンテンツのコンテンツ サーバー データ パッケージを作成する (省略可能)
description: このガイドでは、Windows Server 2016 および Windows 10 を実行するコンピューターでホスト型キャッシュ モードで BranchCache の展開の説明
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: 31e8428f-a482-4734-be1b-213912e34825
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4b8cd284a83736d17859968947f381af171fd6bc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817173"
---
# <a name="create-content-server-data-packages-for-web-and-file-content-optional"></a>Web およびファイル コンテンツのコンテンツ サーバー データ パッケージを作成する (省略可能)

>適用対象:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

この手順を使用して、Web サービスとファイルのサーバー上のコンテンツを prehash し、ホスト型キャッシュ サーバーにインポートするデータのパッケージを作成できます。 

この手順はないため、コンテンツを prehash しプリロードするために必要で、ホスト型キャッシュ サーバー省略可能です。 コンテンツをあらかじめロードする場合データ ホスト型キャッシュを自動的に追加されますクライアントが WAN 接続経由でダウンロードするとします。

この手順では、ファイル サーバーと Web サーバーの両方でコンテンツを事前ハッシュについて説明します。 コンテンツ サーバーのこれらの型があるない場合は、そのサーバーのコンテンツの種類の手順を実行するはありません。

>[!IMPORTANT]
>この手順を実行する前に、インストールして、コンテンツ サーバーで BranchCache を構成する必要があります。 さらに、コンテンツ サーバー上にあるサーバー シークレットを変更する場合、する前に行って事前\-コンテンツのハッシュ – サーバー シークレットを変更することが以前に無効化\-ハッシュを生成します。

この手順を実行するには、Administrators グループのメンバである必要があります。

## <a name="to-create-content-server-data-packages"></a>コンテンツ サーバーにデータ パッケージを作成するには

1. 各コンテンツのサーバー フォルダーと prehash し、データ パッケージを追加するファイルを見つけます。 識別するか、この手順の後半で、データ パッケージを保存するフォルダーを作成します。

2. サーバー コンピューターには、管理者特権で Windows PowerShell を開きます。

3. 必要のあるコンテンツ サーバーの種類に応じて、次のいずれかの操作を行います。

    > [!NOTE]
    > 値: パスのパラメーターは、コンテンツが配置されているフォルダーです。 ファイルサーバーをパッケージに追加するデータを格納するコンテンツ サーバーで有効なフォルダーの場所を使用では、次のコマンド例の値を置き換える必要があります。
  
    - コンテンツを prehash したいが、ファイル サーバー上にある場合は、次のコマンドを入力し、ENTER キーを押します。

        ```  
        Publish-BCFileContent -Path D:\share -StageData
        ```  

    -   コンテンツを prehash したいが、Web サーバー上にある場合は、次のコマンドを入力し、ENTER キーを押します。

        ```  
        Publish-BCWebContent –Path D:\inetpub\wwwroot -StageData
        ```  

4. 各コンテンツ サーバーで、次のコマンドを実行して、データ パッケージを作成します。 例の値を置き換えます\(d:\\temp\)の識別またはこの手順の先頭で作成した場所と – Destination パラメーター。

    ```  
    Export-BCDataPackage –Destination D:\temp
    ```  

5. コンテンツのサーバーからコンテンツをプリロードする、ホスト型キャッシュ サーバー上の共有にアクセスし、データ パッケージをホスト型キャッシュ サーバー上の共有にコピーします。

このガイドを続行する、次を参照してください。[ホスト型キャッシュ サーバーにデータ パッケージのインポート&#40;(省略可能)&#41;](9-Bc-Import-Data.md)します。

