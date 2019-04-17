---
title: "Windows SBS 2003 の設定とデータ Destination Server for Windows Server Essentials の移行を移動します。"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 67087ccb-d820-4642-8ca2-7d2d38714014
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 74375d65845a7a5e9c2d6752bdee49993b8cc791
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="move-windows-sbs-2003-settings-and-data-to-the-destination-server-for-windows-server-essentials-migration"></a>Windows SBS 2003 の設定とデータ Destination Server for Windows Server Essentials の移行を移動します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

設定とデータを移動、移行先サーバーには、次のように。

1.  [移行先サーバーにデータをコピーします。](Move-Windows-SBS-2003-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_CopyData)  
  
2.  [Active Directory ユーザー アカウントを Windows Server Essentials ダッシュ ボード (省略可能) にインポートします。](Move-Windows-SBS-2003-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_ImportADaccounts)  
  
3.  [(省略可能) 以前のログオン スクリプトを削除します。](Move-Windows-SBS-2003-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_RemoveScripts)  
  
4.  [レガシ Active Directory グループ ポリシー オブジェクト (省略可能) を削除します。](Move-Windows-SBS-2003-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_RemoveLegacyADGPO)  
  
5.  [ネットワークを構成します。](Move-Windows-SBS-2003-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_Configure)  
  
6.  [許可されるコンピューターをユーザー アカウントにマップします。](Move-Windows-SBS-2003-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md#BKMK_MapPermittedComputers)  
 
##  <a name="BKMK_CopyData"></a>移行先サーバーにデータをコピーします。  
 移行元サーバーから移行先サーバーにデータをコピーする前に、次のタスクを実行します。  
  
-   各フォルダーに対するアクセス許可など、移行元サーバー上の共有フォルダーの一覧を確認します。 作成するか、移行元サーバーから移行するフォルダー構造を一致するように、移行先サーバー上のフォルダーをカスタマイズします。  
  
-   各フォルダーのサイズを確認し、移行先サーバーに十分な記憶域スペースがあることを確認します。  
  
-   移行元サーバー上の共有フォルダー Read-only の移行先サーバーにファイルをコピーしているときに、手書きできます何もしないように、すべてのユーザーがドライブに配置します。  
  
#### <a name="to-copy-data-from-the-source-server-to-the-destination-server"></a>移行元サーバーから移行先サーバーにデータをコピーするには  
  
1.  ドメイン管理者として移行先サーバーにログオンします。  
  
2.  をクリックして**開始**、種類**cmd**で検索ボックスに、し、Enter キーを押します。  
  
3.  コマンド プロンプトで、次のコマンドを入力し、Enter キーを押します。  
  
    `robocopy \\<SourceServerName> \<SharedSourceFolderName> \\<DestinationServerName> \<SharedDestinationFolderName> /E /B /COPY:DATSOU /LOG:C:\Copyresults.txt`  
  
     どこ：
     - \ < SourceServerName\ > は、移行元サーバーの名前
     - \ < SharedSourceFolderName\ > は、移行元サーバー上の共有フォルダーの名前
     - \ < DestinationServerName\ > は、移行先サーバーの名前
     - \ < SharedDestinationFolderName\ > は、データがコピー先となる移行先サーバー上の共有フォルダー。  
 
4.  移行元サーバーから移行する各共有フォルダーを前の手順を繰り返します。  
  
##  <a name="BKMK_ImportADaccounts"></a>Active Directory ユーザー アカウントを Windows Server Essentials ダッシュ ボード (省略可能) にインポートします。  
 既定では、移行元サーバーで作成されたすべてのユーザー アカウントは、Windows Server Essentials のダッシュ ボードに自動的に移行します。 ただし、一部のプロパティが移行要件を満たしていない場合、Active Directory ユーザー アカウントの自動移行は失敗します。 次の Windows PowerShell コマンドレットを使用して、Active Directory ユーザーをインポートすることができます。  
  
#### <a name="to-import-an-active-directory-user-account-to-the-windows-server-essentials-dashboard"></a>Active Directory ユーザー アカウントを Windows Server Essentials ダッシュ ボードにインポートするには  
  
1.  ドメイン管理者として移行先サーバーにログオンします。  
  
2.  管理者として Windows PowerShell を開きます。  
  
3.  次のコマンドレットを実行場所`[AD username]`にインポートする Active Directory ユーザー アカウントの名前です。  
  
     `Import-WssUser SamAccountName [AD username]`  
  
##  <a name="BKMK_RemoveScripts"></a>(省略可能) 以前のログオン スクリプトを削除します。  
 Windows SBS 2003 では、ソフトウェアのインストールやデスクトップのカスタマイズなどのタスクのログオン スクリプトを使用します。  Windows Server Essentials は、Windows SBS 2003 のログオン スクリプトをログオン スクリプトとグループ ポリシー オブジェクトの組み合わせに置き換えます。  
  
> [!NOTE]
>  Windows SBS 2003 のログオン スクリプトを変更した場合は、カスタマイズの内容を保持するスクリプトの名前を変更する必要があります。  
  
> [!NOTE]
>  Windows SBS 2003 ログオン スクリプトを使用して追加されたユーザー アカウントにのみ適用、**新しいユーザーの追加ウィザード**します。  
  
#### <a name="to-remove-the-windows-sbs-2003-logon-scripts"></a>Windows SBS 2003 のログオン スクリプトを削除するには  
  
1.  をクリックして**開始**、] をポイント**管理ツール**、] をクリックし、**Active Directory ユーザーとコンピューター**します。  
  
2.  **Active Directory ユーザーとコンピューター**、ネットワークを展開し、[クリックして**ユーザー**します。  
  
3.  ユーザー名を右クリックし、をクリックして**プロパティ**、クリックして、**プロファイル**] タブ。  
  
4.  内容を削除、**ログオン スクリプト**テキスト ボックス、およびクリック**OK**します。  
  
5.  ユーザーごとに、手順 3. および 4. を繰り返します。  
  
##  <a name="BKMK_RemoveLegacyADGPO"></a>レガシ Active Directory グループ ポリシー オブジェクト (省略可能) を削除します。  
 Windows Server Essentials のグループ ポリシー オブジェクト (Gpo) が更新されます。 Windows SBS 2003 Gpo のスーパー セットです。 Windows Server Essentials での Windows Server Essentials Gpo および WMI フィルターとの競合を避けるために数、Windows SBS 2003 Gpo および Windows Management Instrumentation (WMI) フィルターが手動で削除する必要があります。  
  
> [!NOTE]
>  元の Windows SBS 2003 グループ ポリシー オブジェクトを変更した場合は、別の場所にそれらのコピーを保存し、Windows SBS 2003 から削除してください。  
  
#### <a name="to-remove-old-group-policy-objects-from-windows-sbs-2003"></a>Windows SBS 2003 から古いグループ ポリシー オブジェクトを削除するには  
  
1.  管理者アカウントを使用して、移行元サーバーにログオンします。  
  
2.  をクリックして**開始**、] をクリックし、**サーバー管理**します。  
  
3.  ナビゲーション ウィンドウで、をクリックして**高度な管理**、] をクリックして**グループ ポリシーの管理**、] をクリックし、**フォレスト:***< YourDomainName\ >*します。  
  
4.  をクリックして**ドメイン**、] をクリックして*< YourDomainName\ >*、] をクリックし、**グループ ポリシー オブジェクト**します。  
  
5.  右クリック**Small Business Server の監査ポリシー**、] をクリックして**削除**、] をクリックし、**OK**します。  
  
6.  ネットワークに適用される次の Gpo を削除する手順 5 を繰り返します。  
  
    -   Small Business Server クライアント コンピューター  
  
    -   Small Business Server ドメイン パスワード ポリシー  
  
         強力なパスワードを強制する Windows Server Essentials では、パスワード ポリシーを構成することをお勧めします。 パスワード ポリシーを構成するには、既定のドメイン ポリシーに書き込まダッシュ ボードを使用します。 パスワード ポリシーの構成は、Windows SBS 2003 では異なり、Small Business Server ドメイン パスワード ポリシー オブジェクトには書き込まれません。  
  
    -   Small Business Server インターネット接続ファイアウォール  
  
    -   Small Business Server ロックアウト ポリシー  
  
    -   Small Business Server のリモート アシスタンスのポリシー  
  
    -   Small Business Server Windows ファイアウォール  
  
    -   Small Business Server Update Services クライアント コンピューター ポリシー  
  
         この GPO は、Windows SBS 2003 R2 から移行する場合に表示されます。  
  
    -   Small Business Server Update Services 共通設定ポリシー  
  
         この GPO は、Windows SBS 2003 R2 から移行する場合に表示されます。  
  
    -   Small Business Server Update Services サーバー コンピューター ポリシー  
  
         この GPO は、Windows SBS 2003 R2 から移行する場合に表示されます。  
  
7.  すべての Gpo が削除されたことを確認します。  
  
#### <a name="to-remove-wmi-filters-from-windows-sbs-2003"></a>Windows SBS 2003 からの WMI フィルターを削除するには  
  
1.  管理者アカウントを使用して、移行元サーバーにログオンします。  
  
2.  をクリックして**開始**、] をクリックし、**サーバー管理**します。  
  
3.  ナビゲーション ウィンドウで、をクリックして**高度な管理**、] をクリックして**グループ ポリシーの管理**、] をクリックし、**フォレスト:***< YourNetworkDomainName\ >*  
  
4.  をクリックして**ドメイン**、] をクリックして*< YourNetworkDomainName\ >*、] をクリックし、**WMI フィルター**します。  
  
5.  右クリック**PostSP2**、] をクリックして**削除**、] をクリックし、**はい**します。  
  
6.  右クリック**PreSP2**、] をクリックして**削除**、] をクリックし、**はい**します。  
  
7.  これら 3 つの WMI フィルターが削除されたことを確認します。  
  
##  <a name="BKMK_Configure"></a>ネットワークを構成します。  
  
#### <a name="to-configure-the-network"></a>ネットワークの構成  
  
1.  移行先サーバーで、ダッシュ ボードを開きます。  
  
2.  ダッシュ ボードで**ホーム**] ページで [**セットアップ**、] をクリックして**Anywhere Access のセットアップ**を選び、**Anywhere Access を構成する] をクリックします。**オプション。  
  
3.  指示に従って、**Anywhere Access のセットアップ**ウィザード、ルーターとドメイン名を構成します。  
  
 ルーターが UPnP フレームワークをサポートしていない場合、または UPnP フレームワークが無効にした場合は、ルーター名の横に黄色の警告アイコンがあります。 次のポートが開かれていることと、移行先サーバーの IP アドレスにリダイレクトされた場合のことを確認します。  
  
-   ポート 80: HTTP Web トラフィック  
  
-   ポート 443: HTTPS Web トラフィック  
  
> [!NOTE]
>  2 番目のサーバー上の内部設置型 Exchange server をセットアップする場合は、ポート 25 (SMTP) も、内部設置型 Exchange サーバーの IP アドレスにリダイレクトされることを確認する必要があります。  
  
##  <a name="BKMK_MapPermittedComputers"></a>許可されるコンピューターをユーザー アカウントにマップします。  
 Windows SBS 2003 では、ユーザーがリモート Web アクセスに接続する場合、ネットワーク内のすべてのコンピューターが表示されます。 これには、コンピューター、ユーザーはへのアクセス許可を持たないものにはが含まれます。 Windows Server Essentials でユーザー割り当てる必要があります明示的にリモート Web アクセスに表示するのには、コンピューターにします。 Windows SBS 2003 から移行する各ユーザー アカウントは、1 つまたは複数のコンピューターにマップする必要があります。  
  
#### <a name="to-map-user-accounts-to-computers"></a>コンピューターにユーザー アカウントにマップするには  
  
1.  移行先サーバーで、Windows Server Essentials ダッシュ ボードを開きます。  
  
2.  ナビゲーション バーで、クリックして**ユーザー**します。  
  
3.  ユーザー アカウントの一覧でユーザー アカウントを右クリックし、をクリックして**アカウント プロパティの表示**します。  
  
4.  をクリックして、**Anywhere Access**タブをクリックし、をクリックして**リモート Web アクセスを許可し、Web サービス アプリケーションにアクセスします。**.  
  
5.  をクリックして**共有フォルダー**、] をクリックして**コンピューター**、] をクリックして**ホームページのリンク**、] をクリックし、**適用**します。  
  
6.  をクリックして、**コンピューター アクセス**タブをクリックし、アクセスを許可するコンピューターの名前をクリックします。  
  
7.  ユーザー アカウントごとに、手順 3、4、5、6 を繰り返します。  
  
> [!NOTE]
>  クライアント コンピューターの構成を変更する必要はありません。 自動的に構成されます。  
  
> [!NOTE]
>  完了したら、移行、移行先サーバー上の最初の新しいユーザー アカウントを作成するときに問題が発生した場合、追加したユーザー アカウントを削除し、再度作成します。
