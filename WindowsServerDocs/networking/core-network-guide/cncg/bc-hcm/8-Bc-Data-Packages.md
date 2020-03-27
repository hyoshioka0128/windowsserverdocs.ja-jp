---
title: Web およびファイル コンテンツのコンテンツ サーバー データ パッケージを作成する (省略可能)
description: このガイドでは、Windows Server 2016 と Windows 10 を実行するコンピューターに、ホスト型キャッシュモードで BranchCache を展開する手順について説明します。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: article
ms.assetid: 31e8428f-a482-4734-be1b-213912e34825
ms.author: lizross
author: eross-msft
ms.openlocfilehash: a02741b163aafe12c52bf0afb4c235aa9436347a
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80318444"
---
# <a name="create-content-server-data-packages-for-web-and-file-content-optional"></a>Web およびファイル コンテンツのコンテンツ サーバー データ パッケージを作成する (省略可能)

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

この手順を使用すると、Web サーバーおよびファイルサーバー上のコンテンツを事前にハッシュし、ホスト型キャッシュサーバーにインポートするデータパッケージを作成できます。 

ホスト型キャッシュサーバーにコンテンツを事前にハッシュし、事前に読み込む必要がないため、この手順は省略できます。 コンテンツを事前に読み込んでいない場合、データは WAN 接続を介してクライアントがダウンロードするときに、自動的にホスト型キャッシュに追加されます。

この手順では、ファイルサーバーと Web サーバーの両方でコンテンツを事前にハッシュする方法について説明します。 これらの種類のコンテンツサーバーが1つもない場合は、そのコンテンツサーバーの種類に関する手順を実行する必要はありません。

>[!IMPORTANT]
>この手順を実行する前に、コンテンツサーバーに BranchCache をインストールして構成する必要があります。 さらに、コンテンツサーバーのサーバーシークレットを変更する場合は、事前にコンテンツをハッシュする前に\-します。サーバーシークレットを変更すると、以前に\-生成されたハッシュが無効になります。

この手順を実行するには、Administrators グループのメンバである必要があります。

## <a name="to-create-content-server-data-packages"></a>コンテンツサーバーのデータパッケージを作成するには

1. 各コンテンツサーバーで、事前ハッシュしてデータパッケージに追加するフォルダーとファイルを見つけます。 この手順の後半で、データパッケージを保存するフォルダーを特定または作成します。

2. サーバーコンピューターで、管理者特権を使用して Windows PowerShell を開きます。

3. 使用しているコンテンツサーバーの種類に応じて、次のいずれかまたは両方の操作を行います。

    > [!NOTE]
    > – Path パラメーターの値は、コンテンツが配置されているフォルダーです。 次のコマンドの例の値は、事前ハッシュしてパッケージに追加するデータが含まれているコンテンツサーバー上の有効なフォルダーの場所に置き換える必要があります。
  
    - 事前ハッシュするコンテンツがファイルサーバー上にある場合は、次のコマンドを入力し、enter キーを押します。

        ```  
        Publish-BCFileContent -Path D:\share -StageData
        ```  

    -   事前ハッシュするコンテンツが Web サーバー上にある場合は、次のコマンドを入力し、enter キーを押します。

        ```  
        Publish-BCWebContent –Path D:\inetpub\wwwroot -StageData
        ```  

4. 各コンテンツサーバーで次のコマンドを実行して、データパッケージを作成します。 – Destination パラメーターの \(D:\\temp\) の例の値を、この手順の先頭で特定または作成した場所に置き換えます。

    ```  
    Export-BCDataPackage –Destination D:\temp
    ```  

5. コンテンツサーバーから、コンテンツをプリロードするホスト型キャッシュサーバー上の共有にアクセスし、データパッケージをホスト型キャッシュサーバー上の共有にコピーします。

このガイドを使用するには、「[ホスト型キャッシュサーバー &#40;にデータパッケージ&#41;をインポートする (オプション)](9-Bc-Import-Data.md)」を参照してください。

