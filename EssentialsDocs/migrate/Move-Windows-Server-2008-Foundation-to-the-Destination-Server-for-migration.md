---
title: Windows Server 2008 Foundation の設定とデータを Windows Server Essentials 移行の移行先サーバーに移動する
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3ff7d040-ebd1-421c-80db-765deacedd4c
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 3d9e662a6474823cae42d0a2abec60963273ca18
ms.sourcegitcommit: 9a4ab3a0d00b06ff16173aed616624c857589459
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2019
ms.locfileid: "66828546"
---
# <a name="move-windows-server-2008-foundation-settings-and-data-to-the-destination-server-for-windows-server-essentials-migration"></a>Windows Server 2008 Foundation の設定とデータを Windows Server Essentials 移行の移行先サーバーに移動する

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

移行先サーバーへの設定とデータの移動は次のように行います。

1. [(省略可能)、移行先サーバーにデータをコピーします。](#copy-data-to-the-destination-server)

2. [Active Directory ユーザー アカウントを Windows Server Essentials ダッシュ ボード (省略可能) にインポートします。](#import-active-directory-user-accounts-to-the-windows-server-essentials-dashboard)

3. [移行元サーバーから DHCP サーバーの役割をルーターに移動します。](#move-the-dhcp-server-role-from-the-source-server-to-the-router)

4. [ネットワークを構成します。](#configure-the-network) 

5. [許可されているコンピューターのユーザー アカウントをマップします。](#map-permitted-computers-to-user-accounts)
  
## <a name="copy-data-to-the-destination-server"></a>データを移行先サーバーにコピーする
 移行元サーバーから移行先サーバーにデータをコピーする前に、以下のタスクを実行します。  
  
- 移行元サーバーで共有フォルダーのリストを確認します。各フォルダーのアクセス許可も含まれます。 移行元サーバーから移行するフォルダー構造に合わせて、移行先サーバーのフォルダーを作成またはカスタマイズします。  
  
- 各フォルダーのサイズを調べて、移行先サーバーに十分な記憶域があることを確認します。  
  
- 移行先サーバーにファイルをコピーしている間にドライブで書き込みが発生しないように、移行元サーバーの共有フォルダーをすべてのユーザーに対して読み取り専用にします。  
  
#### <a name="to-copy-data-from-the-source-server-to-the-destination-server"></a>移行元サーバーから移行先サーバーにデータをコピーするには  
  
1.  移行先サーバーにドメイン管理者としてサインオンし、コマンド ウィンドウを開きます。  
  
2.  コマンド プロンプトで、次のコマンドを入力して Enter キーを押します。  
  
    `robocopy \\<SourceServerName> \<SharedSourceFolderName> \\<DestinationServerName> \<SharedDestinationFolderName> /E /B /COPY:DATSOU /LOG:C:\Copyresults.txt`  
  
     各項目の意味は次のとおりです。
     - \<SourceServerName\>移行元サーバーの名前を指定します
     - \<SharedSourceFolderName\>移行元サーバー上の共有フォルダーの名前を指定します
     - \<DestinationServerName\>移行先サーバーの名前を指定します
     - \<SharedDestinationFolderName\>はデータをコピーする移行先サーバーで共有フォルダーです。  
  
3.  移行元サーバーから移行する共有フォルダーごとに前記の手順を繰り返します。  
  
## <a name="import-active-directory-user-accounts-to-the-windows-server-essentials-dashboard"></a>Active Directory ユーザー アカウントを Windows Server Essentials ダッシュ ボードにインポートします。
 既定では、移行元サーバーで作成されたすべてのユーザー アカウントは Windows Server essentials ダッシュ ボードに自動的に移行します。 ただし、すべてのプロパティが移行要件を満たしていない場合、Active Directory ユーザー アカウントの自動移行は失敗します。 次の Windows PowerShell コマンドレットを使用して、Active Directory ユーザーをインポートできます。  
  
#### <a name="to-import-an-active-directory-user-account-to-the-windows-server-essentials-dashboard"></a>Windows Server Essentials ダッシュ ボードに、Active Directory ユーザー アカウントをインポートするには
  
1.  移行先サーバーにドメイン管理者としてログオンします。  
  
2.  管理者として Windows PowerShell を開きます。  
  
3.  次のコマンドレットを実行します。 `[AD username]` は、インポートする Active Directory ユーザー アカウントの名前です。  
  
     `Import-WssUser  SamAccountName [AD username]`  
  
## <a name="move-the-dhcp-server-role-from-the-source-server-to-the-router"></a>DHCP サーバーの役割を移行元サーバーからルーターに移動する
 移行元サーバーが DHCP の役割を実行している場合、次の手順を実行して、DHCP の役割をルーターに移動します。  
  
#### <a name="to-move-the-dhcp-role-from-the-source-server-to-the-router"></a>DHCP の役割を移行元サーバーからルーターに移動するには  
  
1.  次のようにして、移行元サーバーで DHCP サービスをオフにします。  
  
    1.  移行元サーバーをクリックし、 **[スタート]** 、 **[管理ツール]** 、 **[サービス]** の順にクリックします。  
  
    2.  現在実行しているサービスの一覧で、 **[DHCP Server]** を右クリックし、 **[プロパティ]** をクリックします。  
  
    3.  **[開始の種類]** で、 **[無効]** を選択します。  
  
    4.  サービスを停止します。  
  
2.  ルーターで DHCP の役割を有効にします。  
  
    1.  ルーターで DHCP の役割を有効にするには、ルーターのドキュメントの手順に従います。  
  
    2.  移行元サーバーによって発行される IP アドレスが変わらないようにするには、ルーターのドキュメントの手順に従って、ルーターの DHCP 範囲を、移行元サーバーの DHCP 範囲と同じように構成します。  
  
        > [!IMPORTANT]
        >  ルーターで移行先サーバー用に静的 IP または DHCP 予約が設定されていず、DHCP 範囲が移行元サーバーと異なる場合は、ルーターが移行先サーバーの新しい IP アドレスを発行する可能性があります。 その場合は、ルーターのポート転送ルールを、移行先サーバーの新しい IP アドレスに転送するように設定しなおします。  
  
## <a name="configure-the-network"></a>ネットワークの構成
 DHCP の役割をルーターに移動した後、移行先サーバーでネットワークの設定を構成します。  
  
#### <a name="to-configure-the-network"></a>ネットワークを構成するには  
  
1. 移行先サーバーでダッシュボードを開きます。  
  
2. ダッシュボードの **[ホーム]** ページで、 **[セットアップ]** 、 **[Anywhere Access のセットアップ]** の順にクリックし、 **[クリックして Anywhere Access を構成する]** オプションを選択します。  
  
3. ウィザードの指示に従って、ルーターとドメインの名前を構成します。  
  
   ルーターが UPnP フレームワークをサポートしていない場合、または UPnP フレームワークが無効になっている場合は、黄色の警告アイコンがルーター名の隣に表示されることがあります。 以下のポートが開かれていて、移行先サーバーの IP アドレスに向いていることを確認します。  
  
-   ポート 80:HTTP Web トラフィック  
  
-   ポート 443:HTTPS Web トラフィック  
  
## <a name="map-permitted-computers-to-user-accounts"></a>許可されたコンピューターをユーザー アカウントにマップする  
 Windows Server Essentials でリモート Web アクセスで表示するためのコンピューターへユーザーが明示的に割り当てする必要があります。 Windows Server 2008 Foundation から移行する各ユーザー アカウントを、1 つまたは複数のコンピューターにマップする必要があります。  
  
#### <a name="to-map-user-accounts-to-computers"></a>コンピューターにユーザー アカウントをマップするには  
  
1.  Windows Server Essentials ダッシュ ボードを開きます。  
  
2.  ナビゲーション バーで、 **[ユーザー]** をクリックします。  
  
3.  ユーザー アカウントの一覧で、ユーザー アカウントを右クリックして、 **[アカウント プロパティの表示]** をクリックします。  
  
4.  **[Anywhere Access]** タブをクリックし、 **[リモート Web アクセスを許可し、Web サービス アプリケーションにアクセスする]** をクリックします。  
  
5.  **[共有フォルダー]** 、 **[コンピューター]** 、 **[ホームページ リンク]** の順に選択し、 **[適用]** をクリックします。  
  
6.  **[コンピューター アクセス]** タブをクリックし、アクセスを許可するコンピューターの名前をクリックします。  
  
7.  各ユーザー アカウントについて、手順 3 ～ 6 を繰り返します。  
  
> [!NOTE]
> クライアント コンピューターの構成を変更する必要はありません。 自動的に構成されます。  
>
> 移行を完了した後、移行先サーバーで最初の新しいユーザー アカウントを作成するときに問題が発生する場合は、追加したユーザー アカウントを削除し、再度作成してください。
