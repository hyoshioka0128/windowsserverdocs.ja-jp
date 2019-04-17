---
title: "Windows SBS 2011 Essentials の設定とデータ Destination Server for Windows Server Essentials の移行を移動します。"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 47548994-9fa0-42e0-afa4-c2ccbd063acb
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 80ef8a196f70a77e149dc8defaacf20a82d576e7
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="move-windows-sbs-2011-essentials-settings-and-data-to-the-destination-server-for-windows-server-essentials-migration"></a>Windows SBS 2011 Essentials の設定とデータ Destination Server for Windows Server Essentials の移行を移動します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

設定とデータを移動、移行先サーバーには、次のように。  
  

1.  [移行先サーバーにデータをコピーします。](Move-Windows-SBS-2011-Essentials-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_CopyData)  
  
2.  [Active Directory ユーザー アカウントを Windows Server Essentials ダッシュ ボード (省略可能) にインポートします。](Move-Windows-SBS-2011-Essentials-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_ImportADaccounts)  
  
3.  [ネットワークを構成します。](Move-Windows-SBS-2011-Essentials-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_Network)  
  
4.  [許可されるコンピューターをユーザー アカウントにマップします。](Move-Windows-SBS-2011-Essentials-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_MapPermittedComputers)  
 
##  <a name="BKMK_CopyData"></a>移行先サーバーにデータをコピーします。  
 移行元サーバーから移行先サーバーにデータをコピーする前に、次のタスクを実行します。  
  
-   各フォルダーに対するアクセス許可など、移行元サーバー上の共有フォルダーの一覧を確認します。 作成するか、移行元サーバーから移行するフォルダー構造を一致するように、移行先サーバー上のフォルダーをカスタマイズします。  
  
-   各フォルダーのサイズを確認し、移行先サーバーに十分な記憶域スペースがあることを確認します。  
  
-   移行元サーバー上の共有フォルダー Read-only の移行先サーバーにファイルをコピーしているときに、手書きできます何もしないように、すべてのユーザーがドライブに配置します。  
  
#### <a name="to-copy-data-from-the-source-server-to-the-destination-server"></a>移行元サーバーから移行先サーバーにデータをコピーするには  
  
1.  ドメイン管理者は、移行先サーバーにログインし、コマンド ウィンドウを開きます。  
  
2.  コマンド プロンプトで、次のコマンドを入力し、Enter キーを押します。  
  
    `robocopy \\<SourceServerName> \<SharedSourceFolderName> \\<DestinationServerName> \<SharedDestinationFolderName> /E /B /COPY:DATSOU /LOG:C:\Copyresults.txt`  
  
     どこ：
     - \ < SourceServerName\ > は、移行元サーバーの名前
     - \ < SharedSourceFolderName\ > は、移行元サーバー上の共有フォルダーの名前
     - \ < DestinationServerName\ > は、移行先サーバーの名前
     - \ < SharedDestinationFolderName\ > は、データがコピー先となる移行先サーバー上の共有フォルダー。  
        
3.  移行元サーバーから移行する各共有フォルダーを前の手順を繰り返します。  
  
##  <a name="BKMK_ImportADaccounts"></a>Active Directory ユーザー アカウントを Windows Server Essentials ダッシュ ボード (省略可能) にインポートします。  
 既定では、移行元サーバーで作成されたすべてのユーザー アカウントは、Windows Server Essentials のダッシュ ボードに自動的に移行します。 ただし、すべてのプロパティが移行要件を満たしていない場合、Active Directory ユーザー アカウントの自動移行は失敗します。 次の Windows PowerShell コマンドレットを使用して、Active Directory ユーザーをインポートすることができます。  
  
#### <a name="to-import-an-active-directory-user-account-to-the-windows-server-essentials-dashboard"></a>Active Directory ユーザー アカウントを Windows Server Essentials ダッシュ ボードにインポートするには  
  
1.  ドメイン管理者として移行先サーバーにログオンします。  
  
2.  管理者として Windows PowerShell を開きます。  
  
3.  次のコマンドレットを実行場所`[AD username]`にインポートする Active Directory ユーザー アカウントの名前です。  
  
     `Import-WssUser  SamAccountName [AD username]`  
  
##  <a name="BKMK_Network"></a>ネットワークを構成します。  
  
#### <a name="to-configure-the-network"></a>ネットワークの構成  
  
1.  移行先サーバーで、ダッシュ ボードを開きます。  
  
2.  ダッシュ ボードで**ホーム**] ページで [**セットアップ**、] をクリックして**Anywhere Access のセットアップ**を選び、**Anywhere Access を構成する] をクリックします。**オプション。  
  
3.  ルーターとドメイン名を構成するのには、ウィザードの指示を完了します。  
  
 ルーターが UPnP フレームワークをサポートしていない場合、または UPnP フレームワークが無効にした場合は、ルーター名の横に黄色の警告アイコンがあります。 次のポートが開かれていることと、移行先サーバーの IP アドレスにリダイレクトされた場合のことを確認します。  
  
-   ポート 80: HTTP Web トラフィック  
  
-   ポート 443: HTTPS Web トラフィック  
  
##  <a name="BKMK_MapPermittedComputers"></a>許可されるコンピューターをユーザー アカウントにマップします。  
 Windows Small Business Server 2011 Essentials から移行する各ユーザー アカウントは、1 つまたは複数のコンピューターにマップする必要があります。  
  
#### <a name="to-map-user-accounts-to-computers"></a>コンピューターにユーザー アカウントにマップするには  
  
1.  Windows Server Essentials ダッシュ ボードを開きます。  
  
2.  ナビゲーション バーで、クリックして**ユーザー**します。  
  
3.  ユーザー アカウントの一覧でユーザー アカウントを右クリックし、をクリックして**アカウント プロパティの表示**します。  
  
4.  をクリックして、**Anywhere Access**タブをクリックし、をクリックして**リモート Web アクセスを許可し、Web サービス アプリケーションにアクセスする**します。  
  
5.  選択**共有フォルダー**を選択**コンピューター**を選択**ホームページのリンク**、] をクリックし、**適用**します。  
  
6.  をクリックして、**コンピューター アクセス**タブ、およびアクセスを許可するコンピューターの名前をクリックします。  
  
7.  ユーザー アカウントごとに、手順 3、4、5、6 を繰り返します。  
  
> [!NOTE]
>  クライアント コンピューターの構成を変更する必要はありません。 自動的に構成されます。  
  
> [!NOTE]
>  完了したら、移行、移行先サーバー上の最初の新しいユーザー アカウントを作成するときに問題が発生した場合、追加したユーザー アカウントを削除し、再度作成します。
