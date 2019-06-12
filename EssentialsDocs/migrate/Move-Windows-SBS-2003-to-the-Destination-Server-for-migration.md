---
title: Windows SBS 2003 の設定とデータを Windows Server Essentials 移行の移行先サーバーに移動する
description: Windows Server Essentials を使用する方法について説明します
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
ms.openlocfilehash: 9fd9cdfaea641a0aee615befb5d400fa45160d97
ms.sourcegitcommit: 9a4ab3a0d00b06ff16173aed616624c857589459
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2019
ms.locfileid: "66828556"
---
# <a name="move-windows-sbs-2003-settings-and-data-to-the-destination-server-for-windows-server-essentials-migration"></a>Windows SBS 2003 の設定とデータを Windows Server Essentials 移行の移行先サーバーに移動する

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

移行先サーバーへの設定とデータの移動は次のように行います。

1. [移行先サーバーにデータのコピー](#copy-data-to-the-destination-server)

2. [Active Directory ユーザー アカウントを Windows Server Essentials ダッシュ ボード (省略可能) にインポートします。](#import-active-directory-user-accounts-to-the-windows-server-essentials-dashboard)

3. [(省略可能) の古いログオン スクリプトを削除します。](#remove-old-logon-scripts)

4. [レガシ Active Directory グループ ポリシー オブジェクト (省略可能) を削除します。](#remove-legacy-active-directory-group-policy-objects) 

5. [ネットワークを構成します。](#configure-the-network) 

6. [許可されているコンピューターのユーザー アカウントをマップします。](#map-permitted-computers-to-user-accounts)

## <a name="copy-data-to-the-destination-server"></a>データを移行先サーバーにコピーする
移行元サーバーから移行先サーバーにデータをコピーする前に、以下のタスクを実行します。 

- 移行元サーバーで共有フォルダーのリストを確認します。各フォルダーのアクセス許可も含まれます。 移行元サーバーから移行するフォルダー構造に合わせて、移行先サーバーのフォルダーを作成またはカスタマイズします。 

- 各フォルダーのサイズを調べて、移行先サーバーに十分な記憶域があることを確認します。 

- 移行先サーバーにファイルをコピーしている間にドライブで書き込みが発生しないように、移行元サーバーの共有フォルダーをすべてのユーザーに対して読み取り専用にします。 

#### <a name="to-copy-data-from-the-source-server-to-the-destination-server"></a>移行元サーバーから移行先サーバーにデータをコピーするには 

1. 移行先サーバーにドメイン管理者としてログオンします。 

2. **[スタート]** ボタンをクリックし、検索ボックスに「 **cmd** 」と入力して、Enter キーを押します。 

3. コマンド プロンプトで、次のコマンドを入力して Enter キーを押します。 

    `robocopy \\<SourceServerName> \<SharedSourceFolderName> \\<DestinationServerName> \<SharedDestinationFolderName> /E /B /COPY:DATSOU /LOG:C:\Copyresults.txt` 

各項目の意味は次のとおりです。
 - \<SourceServerName\>移行元サーバーの名前を指定します
 - \<SharedSourceFolderName\>移行元サーバー上の共有フォルダーの名前を指定します
 - \<DestinationServerName\>移行先サーバーの名前を指定します
 - \<SharedDestinationFolderName\>はデータをコピーする移行先サーバーで共有フォルダーです。 

4. 移行元サーバーから移行する共有フォルダーごとに前記の手順を繰り返します。

## <a name="import-active-directory-user-accounts-to-the-windows-server-essentials-dashboard"></a>Active Directory ユーザー アカウントを Windows Server Essentials ダッシュ ボードにインポートします。
 既定では、移行元サーバーで作成されたすべてのユーザー アカウントは Windows Server essentials ダッシュ ボードに自動的に移行します。 ただし、一部のプロパティが移行要件を満たしていない場合、Active Directory ユーザー アカウントの自動移行は失敗します。 次の Windows PowerShell コマンドレットを使用して、Active Directory ユーザーをインポートできます。

#### <a name="to-import-an-active-directory-user-account-to-the-windows-server-essentials-dashboard"></a>Windows Server Essentials ダッシュ ボードに、Active Directory ユーザー アカウントをインポートするには

1. 移行先サーバーにドメイン管理者としてログオンします。

2. 管理者として Windows PowerShell を開きます。

3. 次のコマンドレットを実行します。 `[AD username]` は、インポートする Active Directory ユーザー アカウントの名前です。

    `Import-WssUser SamAccountName [AD username]`

## <a name="remove-old-logon-scripts"></a>古いログオン スクリプトを削除します。
Windows SBS 2003 では、ソフトウェアのインストールやデスクトップのカスタマイズなどのタスクに、ログオン スクリプトが使用されています。 Windows Server Essentials は、Windows SBS 2003 のログオン スクリプトをログオン スクリプトとグループ ポリシー オブジェクトの組み合わせに置き換えます。

> [!NOTE]
> Windows SBS 2003 のログオン スクリプトを変更した場合、カスタマイズを維持するにはスクリプトの名前を変更する必要があります。
>
> Windows SBS 2003 のログオン スクリプトは、 **新しいユーザーの追加ウィザード**を使用して追加されたユーザー アカウントにのみ適用されます。

#### <a name="to-remove-the-windows-sbs-2003-logon-scripts"></a>Windows SBS 2003 のログオン スクリプトを削除するには 

1. **[スタート]** ボタンをクリックし、 **[管理ツール]** をポイントして、 **[Active Directory ユーザーとコンピューター]** をクリックします。

2. **[Active Directory ユーザーとコンピューター]** で、ネットワークを展開し、 **[ユーザー]** をクリックします。

3. ユーザー名を右クリックし、 **[プロパティ]** をクリックして、 **[プロファイル]** タブをクリックします。

4. **[ログオン スクリプト]** ボックスの内容を削除し、 **[OK]** をクリックします。

5. 各ユーザーに対して、手順 3. および 4. を繰り返します。

## <a name="remove-legacy-active-directory-group-policy-objects"></a>レガシ Active Directory グループ ポリシー オブジェクトを削除します。
Windows Server Essentials のグループ ポリシー オブジェクト (Gpo) が更新されます。 これは Windows SBS 2003 GPO のスーパーセットです。 Windows Server essentials では、Windows SBS 2003 Gpo および Windows Management Instrumentation (WMI) フィルターは、Windows Server Essentials の Gpo および WMI フィルターとの競合を避けるために手動で削除する必要があります。 

> [!NOTE]
> 元の Windows SBS 2003 グループ ポリシー オブジェクトを変更した場合は、そのコピーを別の場所に保存した後、Windows SBS 2003 から削除します。

#### <a name="to-remove-old-group-policy-objects-from-windows-sbs-2003"></a>古いグループ ポリシー オブジェクトを Windows SBS 2003 から削除するには 

1. 管理者アカウントで移行元サーバーにログオンします。 

2. **[スタート]** ボタンをクリックし、 **[サーバー管理]** をクリックします。 

3. ナビゲーション ウィンドウで、[**高度な管理**、] をクリックして**グループ ポリシー管理**、順にクリックします **フォレスト: * * * < YourDomainName\>* します。 

4. クリックして**ドメイン**、 をクリックして *< YourDomainName\>* 、順にクリックします**グループ ポリシー オブジェクト**します。 

5. **[Small Business Server の監査のポリシー]** を右クリックし、 **[削除]** をクリックして、 **[OK]** をクリックします。 

6. 手順 5 を繰り返して、ネットワークに適用される次の GPO を削除します。 

 - Small Business Server クライアント コンピューター 

 - Small Business Server ドメイン パスワード ポリシー 

強力なパスワードを Windows Server Essentials でのパスワード ポリシーを構成することをお勧めします。 パスワード ポリシーを構成するにはダッシュボードを使用します。構成は既定のドメイン ポリシーに書き込まれます。 パスワード ポリシーの構成は、Windows SBS 2003 とは異なり、Small Business Server ドメイン パスワード ポリシー オブジェクトには書き込まれません。 

 - Small Business Server インターネット接続ファイアウォール 

 - Small Business Server ロックアウト ポリシー 

 - Small Business Server リモート アシスタンスのポリシー 

 - Small Business Server Windows ファイアウォール 

 - Small Business Server Update Services クライアント コンピューター ポリシー 

 この GPO は、Windows SBS 2003 R2 から移行している場合に存在します。 

 - Small Business Server Update Services 共通設定ポリシー 

 この GPO は、Windows SBS 2003 R2 から移行している場合に存在します。 
 
 - Small Business Server Update Services サーバー コンピューター ポリシー 
 
 この GPO は、Windows SBS 2003 R2 から移行している場合に存在します。

7. すべての GPO が削除されたことを確認します。

#### <a name="to-remove-wmi-filters-from-windows-sbs-2003"></a>WMI フィルターを Windows SBS 2003 から削除するには

1. 管理者アカウントで移行元サーバーにログオンします。

2. **[スタート]** ボタンをクリックし、 **[サーバー管理]** をクリックします。

3. ナビゲーション ウィンドウで、[**高度な管理**、] をクリックして**Group Policy Management**、順にクリックします **フォレスト: * * * < ネットワーク ドメイン名\>*

4. をクリックして**ドメイン**、 をクリックして *< ネットワーク ドメイン名\>* 、 をクリックし、 **WMI フィルター**します。

5. **[PostSP2]** を右クリックし、 **[削除]** をクリックして、 **[はい]** をクリックします。

6. **[PreSP2]** を右クリックし、 **[削除]** をクリックして、 **[はい]** をクリックします。

7. これら 3 つの WMI フィルターが削除されたことを確認します。

## <a name="configure-the-network"></a>ネットワークの構成

#### <a name="to-configure-the-network"></a>ネットワークを構成するには 

1. 移行先サーバーでダッシュボードを開きます。 

2. ダッシュボードの **[ホーム]** ページで、 **[セットアップ]** 、 **[Anywhere Access のセットアップ]** の順にクリックし、 **[クリックして Anywhere Access を構成する]** オプションを選択します。 

3. **[Anywhere Access のセットアップ]** ウィザードの指示に従って、ルーターとドメイン名を構成します。

 ルーターが UPnP フレームワークをサポートしていない場合、または UPnP フレームワークが無効になっている場合は、黄色の警告アイコンがルーター名の隣に表示されることがあります。 以下のポートが開かれていて、移行先サーバーの IP アドレスに向いていることを確認します。

- ポート 80:HTTP Web トラフィック

- ポート 443:HTTPS Web トラフィック

> [!NOTE]
> 第 2 のサーバーにオンプレミス Exchange サーバーを設定してある場合は、ポート 25 (SMTP 用) も開かれていること、およびオンプレミス Exchange サーバーの IP アドレスにリダイレクトされることを確認する必要があります。

## <a name="map-permitted-computers-to-user-accounts"></a>許可されたコンピューターをユーザー アカウントにマップする
 Windows SBS 2003 では、ユーザーがリモート Web アクセスに接続する場合、ネットワーク内のすべてのコンピューターが表示されます。 これには、ユーザーがアクセス許可を持たないものも含まれる場合があります。 Windows Server Essentials でリモート Web アクセスで表示するためのコンピューターへユーザーが明示的に割り当てする必要があります。 Windows SBS 2003 から移行する各ユーザー アカウントを、1 つまたは複数のコンピューターにマップする必要があります。 

#### <a name="to-map-user-accounts-to-computers"></a>コンピューターにユーザー アカウントをマップするには 

1. 移行先サーバーでは、Windows Server Essentials ダッシュ ボードを開きます。 

2. ナビゲーション バーで、 **[ユーザー]** をクリックします。 

3. ユーザー アカウントの一覧で、ユーザー アカウントを右クリックして、 **[アカウント プロパティの表示]** をクリックします。 

4. **[Anywhere Access]** タブをクリックし、 **[リモート Web アクセスを許可し、Web サービス アプリケーションにアクセスする]** をクリックします。 

5. **[共有フォルダー]** 、 **[コンピューター]** 、 **[ホームページ リンク]** の順にクリックし、 **[適用]** をクリックします。 

6. **[コンピューター アクセス]** タブをクリックし、アクセスを許可するコンピューターの名前をクリックします。 

7. 各ユーザー アカウントについて、手順 3 ～ 6 を繰り返します。 

> [!NOTE]
> クライアント コンピューターの構成を変更する必要はありません。 自動的に構成されます。
>
> 移行を完了した後、移行先サーバーで最初の新しいユーザー アカウントを作成するときに問題が発生する場合は、追加したユーザー アカウントを削除し、再度作成してください。
