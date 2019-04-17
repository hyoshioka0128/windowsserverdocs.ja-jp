---
title: コンテンツの作成の Web サービスとファイル サーバー データ パッケージ コンテンツ (省略可能)
description: このガイドでは、Windows Server 2016 および Windows 10 を実行するコンピューターでホスト型キャッシュ モードで BranchCache を展開するの説明
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: 31e8428f-a482-4734-be1b-213912e34825
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8f814bbac5c74081259d8eef6deda79d914bfec7
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="create-content-server-data-packages-for-web-and-file-content-optional"></a>コンテンツの作成の Web サービスとファイル サーバー データ パッケージ コンテンツ (省略可能)

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

この手順を使用して Web サービスとファイルのサーバー上のコンテンツを prehash し、ホスト型キャッシュ サーバーにインポートするデータのパッケージを作成できます。 

必要はありません prehash およびプリロード コンテンツをホスト型キャッシュ サーバーでこの手順は省略可能です。 コンテンツをあらかじめロードする場合データが、ホスト型キャッシュを自動的に追加ようにクライアントが WAN 接続経由でダウンロードします。

この手順では、ファイル サーバーと Web サーバーの両方でコンテンツを事前ハッシュに沿って説明します。 これらの種類のコンテンツ サーバーのいずれかをいない場合は、そのコンテンツ サーバーの種類の手順を実行する必要はありません。

>[!IMPORTANT]
>この手順を実行する前に、インストールして、コンテンツ サーバーで BranchCache を構成する必要があります。 さらに、コンテンツ サーバー上にあるサーバー シークレットを変更する場合は、ようにファイル ハッシュする前にコンテンツ – previously\ で生成されたハッシュを無効に、サーバー シークレットを変更します。

この手順を実行するには、Administrators グループのメンバーがあります。

## <a name="to-create-content-server-data-packages"></a>コンテンツ サーバー データ パッケージを作成するには

1. 各コンテンツ サーバーで、フォルダーと事前ハッシュし、データ パッケージを追加するファイルを見つけます。 特定したり、この手順の後半でデータ パッケージを保存するフォルダーを作成します。

2. サーバーのコンピューターでは、管理者特権で Windows PowerShell を開きます。

3. いずれかまたは両方があるコンテンツ サーバーの種類に応じて、次の操作を行います。

    > [!NOTE]
    > 値: パスのパラメーターは、コンテンツが保存されているフォルダーです。 有効なフォルダーの場所にコンテンツの事前ハッシュし、パッケージを追加するデータが含まれるサーバーで以下のコマンドで値の例を置き換える必要があります。
  
    - コンテンツを prehash したいが、ファイル サーバー上にある場合は、次のコマンドを入力し、し、ENTER キーを押します。

        ```  
        Publish-BCFileContent -Path D:\share -StageData
        ```  

    -   Prehash しコンテンツは、Web サーバーでは、次のコマンドを入力し、ENTER キーを押します。

        ```  
        Publish-BCWebContent –Path D:\inetpub\wwwroot -StageData
        ```  

4. それぞれのコンテンツ サーバーで、次のコマンドを実行して、データ パッケージを作成します。 置換の例の値 \(D:\\temp\) 識別またはこの手順の開始時に作成する場所を指定して – Destination パラメーターのします。

    ```  
    Export-BCDataPackage –Destination D:\temp
    ```  

5. コンテンツ サーバーからコンテンツをプリロードする、ホスト型キャッシュ サーバー上の共有にアクセスし、データ パッケージをホスト型キャッシュ サーバー上の共有にコピーします。

このガイドでは、続行するのを参照してください[ホスト型キャッシュ サーバー (&) #40";"オプション"&"#41 です。 上のデータ パッケージのインポート。](9-Bc-Import-Data.md).

