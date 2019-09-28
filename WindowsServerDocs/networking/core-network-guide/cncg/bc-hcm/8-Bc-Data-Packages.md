---
title: Web およびファイル コンテンツのコンテンツ サーバー データ パッケージを作成する (省略可能)
description: このガイドでは、Windows Server 2016 と Windows 10 を実行するコンピューターに、ホスト型キャッシュモードで BranchCache を展開する手順について説明します。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: article
ms.assetid: 31e8428f-a482-4734-be1b-213912e34825
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 104e3cfd0525c43857bb37d781f6b2475978238e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406390"
---
# <a name="create-content-server-data-packages-for-web-and-file-content-optional"></a>Web およびファイル コンテンツのコンテンツ サーバー データ パッケージを作成する (省略可能)

>適用対象:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

この手順を使用すると、Web サーバーおよびファイルサーバー上のコンテンツを事前にハッシュし、ホスト型キャッシュサーバーにインポートするデータパッケージを作成できます。 

ホスト型キャッシュサーバーにコンテンツを事前にハッシュし、事前に読み込む必要がないため、この手順は省略できます。 コンテンツを事前に読み込んでいない場合、データは WAN 接続を介してクライアントがダウンロードするときに、自動的にホスト型キャッシュに追加されます。

この手順では、ファイルサーバーと Web サーバーの両方でコンテンツを事前にハッシュする方法について説明します。 これらの種類のコンテンツサーバーが1つもない場合は、そのコンテンツサーバーの種類に関する手順を実行する必要はありません。

>[!IMPORTANT]
>この手順を実行する前に、コンテンツサーバーに BranchCache をインストールして構成する必要があります。 また、コンテンツサーバーのサーバーシークレットを変更する場合は、事前に @ no__t-0hashing コンテンツを変更する必要があります。サーバーシークレットを変更すると、以前の @ no__t で生成されたハッシュが無効になります。

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

4. 各コンテンツサーバーで次のコマンドを実行して、データパッケージを作成します。 – Destination パラメーターの \(D: \\temp @ no__t-2 の例の値を、この手順の最初に指定または作成した場所に置き換えます。

    ```  
    Export-BCDataPackage –Destination D:\temp
    ```  

5. コンテンツサーバーから、コンテンツをプリロードするホスト型キャッシュサーバー上の共有にアクセスし、データパッケージをホスト型キャッシュサーバー上の共有にコピーします。

このガイドを使用するには、「[ホスト型キャッシュサーバー &#40;にデータパッケージ&#41;をインポートする (オプション)](9-Bc-Import-Data.md)」を参照してください。

