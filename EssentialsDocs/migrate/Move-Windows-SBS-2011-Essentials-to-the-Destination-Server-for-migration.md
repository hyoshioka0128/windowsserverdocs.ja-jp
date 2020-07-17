---
title: Windows SBS 2011 Essentials の設定とデータを Windows Server Essentials 移行の移行先サーバーに移動する
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 47548994-9fa0-42e0-afa4-c2ccbd063acb
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: efc479f4c84baf72b1656afb85eef22d9ca710d8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852465"
---
# <a name="move-windows-sbs-2011-essentials-settings-and-data-to-the-destination-server-for-windows-server-essentials-migration"></a>Windows SBS 2011 Essentials の設定とデータを Windows Server Essentials 移行の移行先サーバーに移動する

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

移行先サーバーへの設定とデータの移動は次のように行います。  
  

1.  [移行先サーバーにデータをコピーする](Move-Windows-SBS-2011-Essentials-to-the-Destination-Server-for-migration.md#BKMK_CopyData)  
  
2.  [Windows Server Essentials ダッシュボードに Active Directory ユーザーアカウントをインポートする (省略可能)](Move-Windows-SBS-2011-Essentials-to-the-Destination-Server-for-migration.md#BKMK_ImportADaccounts)  
  
3.  [ネットワークを構成する](Move-Windows-SBS-2011-Essentials-to-the-Destination-Server-for-migration.md#BKMK_Network)  
  
4.  [許可されたコンピューターをユーザーアカウントにマップする](Move-Windows-SBS-2011-Essentials-to-the-Destination-Server-for-migration.md#BKMK_MapPermittedComputers)  
 
##  <a name="copy-data-to-the-destination-server"></a><a name="BKMK_CopyData"></a>移行先サーバーにデータをコピーする  
 移行元サーバーから移行先サーバーにデータをコピーする前に、以下のタスクを実行します。  
  
-   移行元サーバーで共有フォルダーのリストを確認します。各フォルダーのアクセス許可も含まれます。 移行元サーバーから移行するフォルダー構造に合わせて、移行先サーバーのフォルダーを作成またはカスタマイズします。  
  
-   各フォルダーのサイズを調べて、移行先サーバーに十分な記憶域があることを確認します。  
  
-   移行先サーバーにファイルをコピーしている間にドライブで書き込みが発生しないように、移行元サーバーの共有フォルダーをすべてのユーザーに対して読み取り専用にします。  
  
#### <a name="to-copy-data-from-the-source-server-to-the-destination-server"></a>移行元サーバーから移行先サーバーにデータをコピーするには  
  
1.  移行先サーバーにドメイン管理者としてサインインし、コマンド ウィンドウを開きます。  
  
2.  コマンド プロンプトで、次のコマンドを入力して Enter キーを押します。  
  
    `robocopy \\<SourceServerName> \<SharedSourceFolderName> \\<DestinationServerName> \<SharedDestinationFolderName> /E /B /COPY:DATSOU /LOG:C:\Copyresults.txt`  
  
     各項目の意味は次のとおりです。
     - \<SourceServerName\> は、移行元サーバーの名前です。
     - \<共有 Dsourcefoldername\> は、移行元サーバー上の共有フォルダーの名前です。
     - \<DestinationServerName\> は、移行先サーバーの名前です。
     - \<SharedDestinationFolderName\> は、データがコピーされる移行先サーバー上の共有フォルダーです。  
        
3.  移行元サーバーから移行する共有フォルダーごとに前記の手順を繰り返します。  
  
##  <a name="import-active-directory-user-accounts-to-the-windows-server-essentials-dashboard-optional"></a><a name="BKMK_ImportADaccounts"></a>Windows Server Essentials ダッシュボードに Active Directory ユーザーアカウントをインポートする (省略可能)  
 既定では、移行元サーバーで作成されたすべてのユーザーアカウントは、Windows Server Essentials のダッシュボードに自動的に移行されます。 ただし、すべてのプロパティが移行要件を満たしていない場合、Active Directory ユーザー アカウントの自動移行は失敗します。 次の Windows PowerShell コマンドレットを使用して、Active Directory ユーザーをインポートできます。  
  
#### <a name="to-import-an-active-directory-user-account-to-the-windows-server-essentials-dashboard"></a>Active Directory ユーザーアカウントを Windows Server Essentials ダッシュボードにインポートするには  
  
1.  移行先サーバーにドメイン管理者としてログオンします。  
  
2.  管理者として Windows PowerShell を開きます。  
  
3.  次のコマンドレットを実行します。 `[AD username]` は、インポートする Active Directory ユーザー アカウントの名前です。  
  
     `Import-WssUser  SamAccountName [AD username]`  
  
##  <a name="configure-the-network"></a><a name="BKMK_Network"></a>ネットワークを構成する  
  
#### <a name="to-configure-the-network"></a>ネットワークを構成するには  
  
1. 移行先サーバーでダッシュボードを開きます。  
  
2. ダッシュボードの **[ホーム]** ページで、 **[セットアップ]** 、 **[Anywhere Access のセットアップ]** の順にクリックし、 **[クリックして Anywhere Access を構成する]** オプションを選択します。  
  
3. ウィザードの指示に従って、ルーターとドメインの名前を構成します。  
  
   ルーターが UPnP フレームワークをサポートしていない場合、または UPnP フレームワークが無効になっている場合は、黄色の警告アイコンがルーター名の隣に表示されることがあります。 以下のポートが開かれていて、移行先サーバーの IP アドレスに向いていることを確認します。  
  
-   ポート 80: HTTP Web トラフィック  
  
-   ポート 443: HTTPS Web トラフィック  
  
##  <a name="map-permitted-computers-to-user-accounts"></a><a name="BKMK_MapPermittedComputers"></a>許可されたコンピューターをユーザーアカウントにマップする  
 Windows Small Business Server 2011 Essentials から移行する各ユーザー アカウントを、1 つまたは複数のコンピューターにマップする必要があります。  
  
#### <a name="to-map-user-accounts-to-computers"></a>コンピューターにユーザー アカウントをマップするには  
  
1.  Windows Server Essentials ダッシュボードを開きます。  
  
2.  ナビゲーション バーで、 **[ユーザー]** をクリックします。  
  
3.  ユーザー アカウントの一覧で、ユーザー アカウントを右クリックして、 **[アカウント プロパティの表示]** をクリックします。  
  
4.  **[Anywhere Access]** タブをクリックし、 **[リモート Web アクセスを許可し、Web サービス アプリケーションにアクセスする]** をクリックします。  
  
5.  **[共有フォルダー]** 、 **[コンピューター]** 、 **[ホームページ リンク]** の順に選択し、 **[適用]** をクリックします。  
  
6.  **[コンピューター アクセス]** タブをクリックし、アクセスを許可するコンピューターの名前をクリックします。  
  
7.  各ユーザー アカウントについて、手順 3 ～ 6 を繰り返します。  
  
> [!NOTE]
>  クライアント コンピューターの構成を変更する必要はありません。 自動的に構成されます。  
  
> [!NOTE]
>  移行を完了した後、移行先サーバーで最初の新しいユーザー アカウントを作成するときに問題が発生する場合は、追加したユーザー アカウントを削除し、再度作成してください。
