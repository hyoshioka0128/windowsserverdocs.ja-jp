---
title: "手順 4: Destination Server for Windows Server Essentials 移行の設定とデータを移動します。"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e143df43-e227-4629-a4ab-9f70d9bf6e84
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: db1169a5415039498718a7988c711d068945b4b7
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="step-4-move-settings-and-data-to-the-destination-server-for-windows-server-essentials-migration"></a>手順 4: Destination Server for Windows Server Essentials 移行の設定とデータを移動します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

このセクションでは、移行元サーバーから移行するデータと設定に関する情報を提供します。 設定とデータを移動、移行先サーバーには、次のように。  
  
-   [移行先サーバーにデータをコピーします。](Step-4--Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_CopyData)  
  
-   [ネットワークを構成します。](Step-4--Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_Network)  
  
-   [許可されるコンピューターをユーザー アカウントにマップします。](Step-4--Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_MapPermittedComputers)  
  
##  <a name="BKMK_CopyData"></a>移行先サーバーにデータをコピーします。  
 移行元サーバーから移行先サーバーにデータをコピーする前に、次のタスクを実行します。  
  
-   各フォルダーに対するアクセス許可など、移行元サーバー上の共有フォルダーの一覧を確認します。 作成するか、移行元サーバーから移行するフォルダー構造を一致するように、移行先サーバー上のフォルダーをカスタマイズします。  
  
-   各フォルダーのサイズを確認し、移行先サーバーに十分な記憶域スペースがあることを確認します。  
  
-   移行元サーバー上の共有フォルダー Read-only すべてのユーザーの書き込みは行われませんしながら、ハード ドライブにできるようにファイル コピーしている移行先サーバーにします。  
  
-   **クライアント コンピューターのバックアップ**フォルダーは移行先サーバーに移行できません。 サーバーの移行前にすべてのクライアント コンピューターが正常であるになっていることを確認します。 サーバーの移行後、構成して、すべての重要なクライアント コンピューターのバックアップは、データを確認するクライアント コンピューターのバックアップを開始することをお勧めします。  
  
-   **File History Backups**フォルダーは Windows Server Essentials でのフォルダー構造とバックアップ メタデータの変更のため、移行先サーバーに直接移行できません。 ただし、移行することは、**File History Backups**特定のコンピューターで特定のユーザーのフォルダーです。 ためには、検索する必要があります、**データ**内のフォルダー、**File History Backups**そのユーザーとコンピューターのフォルダーをコピーし、**データ**フォルダーを**File History Backups**、移行先サーバー上のフォルダーです。  
  
#### <a name="to-copy-data-from-the-source-server-to-the-destination-server"></a>移行元サーバーから移行先サーバーにデータをコピーするには  
  
1.  ドメイン管理者は、移行先サーバーにログインし、コマンド プロンプト ウィンドウまたは Windows PowerShell コマンド プロンプトを開きます。  
  
2.  コマンド プロンプト ウィンドウを使用する場合、次のコマンドを入力し、Enter キーを押します。  
  
    `robocopy \\<SourceServerName>\<SharedSourceFolderName> "<PathOfTheDestination>\<SharedDestinationFolderName>" /E /B /COPY:DATSOU /LOG:C:\Copyresults.txt`
  
     どこ：  
  
    -   \ < SourceServerName\ > は、移行元サーバーの名前  
  
    -   \ < SharedSourceFolderName\ > は、移行元サーバー上の共有フォルダーの名前  
  
    -   \ < PathOfTheDestination\ > は、フォルダーを移動する場所の絶対パス  
  
    -   \ < SharedDestinationFolderName\ > は、データがコピー先となる移行先サーバー上のフォルダー  
  
     たとえば、`robocopy \\sourceserver\MyData "d:\ServerFolders\MyData" /E /B /COPY:DATSOU /LOG:C:\Copyresults.txt`します。  
  
3.  Windows PowerShell を使用して、次のコマンドを入力し、Enter キーを押します。  
  
     `Add-Wssfolder  Path \ -Name  -KeepPermission`  
  
4.  共有フォルダーごとに、移行元サーバーから移行するには、このプロセスを繰り返します。  
  
##  <a name="BKMK_Network"></a>ネットワークを構成します。  
  
#### <a name="to-configure-the-network"></a>ネットワークの構成  
  
1.  移行先サーバーで、ダッシュ ボードを開きます。  
  
2.  ダッシュ ボードで**ホーム**] ページで [**セットアップ**、] をクリックして**Anywhere Access のセットアップ**を選び、**Anywhere Access を構成する] をクリックします。**オプション。  
  
3.  Anywhere Access のウィザードの設定が表示されます。 ルーターとドメイン名を構成するのには、ウィザードの指示を完了します。  
  
 ルーターが UPnP フレームワークをサポートしていない場合、または UPnP フレームワークが無効にした場合は、ルーター名の横に黄色の警告アイコンがあります。 次のポートが開かれていることと、移行先サーバーの IP アドレスにリダイレクトされた場合のことを確認します。  
  
-   ポート 80: HTTP Web トラフィック  
  
-   ポート 443: HTTPS Web トラフィック  
  
> [!NOTE]
>  移行先サーバーで、パブリック ドメイン名を構成する場合の動的 DNS 更新競合を回避するように移行元サーバーからドメイン名を解放する必要があります。  
  
##  <a name="BKMK_MapPermittedComputers"></a>許可されるコンピューターをユーザー アカウントにマップします。  
 以前のバージョンの Windows Small Business Server または Windows Server Essentials から移行する各ユーザー アカウントは、1 つまたは複数のコンピューターにマップする必要があります。  
  
#### <a name="to-map-user-accounts-to-computers"></a>コンピューターにユーザー アカウントにマップするには  
  
1.  Windows Server Essentials ダッシュ ボードを開きます。  
  
2.  ナビゲーション バーで、クリックして**ユーザー**します。  
  
3.  ユーザー アカウントの一覧でユーザー アカウントを右クリックし、をクリックして**アカウント プロパティの表示**します。  
  
4.  をクリックして、**Anywhere Access**タブをクリックし、をクリックして**リモート Web アクセスを許可し、Web サービス アプリケーションにアクセスする**します。  
  
5.  をクリックして**共有フォルダー**、] をクリックして**コンピューター**、] をクリックして**ホームページのリンク**、] をクリックし、**適用**します。  
  
6.  をクリックして、**コンピューター アクセス**タブ、およびアクセスを許可するコンピューターの名前をクリックします。  
  
7.  ユーザー アカウントごとに、手順 3、4、5、6 を繰り返します。  
  
> [!NOTE]
>  クライアント コンピューターの構成を変更する必要はありません。 自動的に構成されます。  
  
> [!NOTE]
>  完了したら、移行、移行先サーバー上の最初の新しいユーザー アカウントを作成するときに問題が発生した場合、追加したユーザー アカウントを削除し、再度作成します。  
  
## <a name="next-steps"></a>次の手順  
 設定とデータを移行先サーバーに移動しました。 移動できるようになりました[手順 5: Windows Server Essentials の移行先サーバーの移行でフォルダー リダイレクトを有効にする](Step-5--Enable-folder-redirection-on-the-Destination-Server-for-Windows-Server-Essentials-migration.md)します。  
  

すべての手順を参照してください[Windows Server Essentials への移行](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)します。

