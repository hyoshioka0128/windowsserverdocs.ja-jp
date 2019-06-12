---
title: Windows Server Essentials migration1 の移行後のタスクを実行します。
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f2d236a4-0d62-4961-9d1f-332054e06f6d
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 93d07938435ab1ce7686b1960974696582a2924c
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66432664"
---
# <a name="perform-post-migration-tasks-for-windows-server-essentials-migration1"></a>Windows Server Essentials migration1 の移行後のタスクを実行します。

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

以下のタスクでは、移行元サーバーと部分的に同じ設定で移行先サーバーのセットアップを終了します。 移行プロセスの間に移行元サーバーで無効にした設定は、移行先サーバーに移行されていません。 または、実行することのできるオプションの構成手順です。  
  

-   [移行元サーバーの DNS エントリを削除します。](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_DeleteDNSEntries)  
  
-   [基幹業務およびその他のアプリケーション データ フォルダーを共有します。](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_ShareLineOfBusinessAndOtherApplications)  
  
-   [移行後にクライアント コンピューターの問題を修正します。](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_FixClientComputerIssuesAfterMigrating)  
  
-   [組み込みの Administrators グループにバッチ ジョブとしてログオンする権限を付与します。](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_AdminGroup)  

-   [移行元サーバーの DNS エントリを削除します。](../migrate/Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_DeleteDNSEntries)  
  
-   [基幹業務およびその他のアプリケーション データ フォルダーを共有します。](../migrate/Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_ShareLineOfBusinessAndOtherApplications)  
  
-   [移行後にクライアント コンピューターの問題を修正します。](../migrate/Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_FixClientComputerIssuesAfterMigrating)  
  
-   [組み込みの Administrators グループにバッチ ジョブとしてログオンする権限を付与します。](../migrate/Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_AdminGroup)  

  
##  <a name="BKMK_DeleteDNSEntries"></a> 移行元サーバーの DNS エントリを削除します。  
 移行元サーバーを使用停止した後、ドメイン ネーム サービス (DNS) サーバーに移行元サーバーを参照しているエントリがまだ含まれる場合があります。 そのような DNS エントリを削除します。  
  
#### <a name="to-delete-dns-entries-that-point-to-the-source-server"></a>移行元サーバーを指定する DNS エントリを削除するには  
  
1.  移行先サーバーで **[DNS マネージャー]** を開きます。  
  
2.  DNS マネージャーでサーバー名をクリックし、 **[プロパティ]** をクリックして、 **[フォワーダー]** タブをクリックします。  
  
3.  移行元サーバーを参照しているエントリがフォワーダー リストにあるかどうかを確認します。 ある場合、 **[編集]** をクリックし、 **[フォワーダーの編集]** ウィンドウでそのエントリを削除します。  
  
4.  **[DNS マネージャー]** で、サーバー名を展開し、 **[前方参照ゾーン]** を展開します。  
  
5.  前方参照ゾーンごとに、ゾーンを右クリックし、 **[プロパティ]** をクリックして、 **[ネーム サーバー]** タブをクリックします。  
  
6.  移行元サーバーを参照している **[ネーム サーバー]** ボックス内のエントリをクリックし、 **[削除]** をクリックして、 **[OK]** をクリックします。  
  
7.  手順 5 と 6 を繰り返して、移行元サーバーに対するポインターをすべて削除します。  
  
8.  **[OK]** をクリックして、 **[プロパティ]** ウィンドウを閉じます。  
  
9. **[DNS マネージャー]** コンソールで、 **[逆引き参照ゾーン]** を展開します。  
  
10. 手順 6 ～ 9 を繰り返して、移行元サーバーを指定する逆引き参照ゾーンをすべて削除します。  
  
##  <a name="BKMK_ShareLineOfBusinessAndOtherApplications"></a> 基幹業務およびその他のアプリケーション データ フォルダーを共有します。  
 基幹業務アプリケーションなどのアプリケーションのデータ フォルダーを移行先サーバーにコピーした後で、そのフォルダーに共有フォルダーのアクセス許可と NTFS アクセス許可を設定する必要があります。 Windows Server Essentials ダッシュ ボードの共有フォルダーが表示されます、アクセス許可を設定した後、**ストレージ**セクション。  
  
 ログオン スクリプトを使用してドライブを共有フォルダーに割り当てている場合、移行先サーバー上のドライブに割り当てを行うためのスクリプトを更新する必要があります。  
  
##  <a name="BKMK_FixClientComputerIssuesAfterMigrating"></a> 移行後にクライアント コンピューターの問題を修正します。  
 Microsoft ファイアウォール クライアントとインターネットから Windows Small Business Server 2003 Premium Edition を Microsoft Internet Security と Acceleration (ISA) Server がインストールされている Windows Server Essentials に移行する場合、ネットワーク上のクライアント コンピューターが必要もエクスプ ローラーのプロキシ サーバーを使用するように構成します。  
  
 プロキシ サーバーは存在しなくなったので、これはクライアント コンピューターでの接続の問題の原因になります。 別のプロキシ サーバーが構成されている場合は、プロキシ サーバーの Windows SBS 2003 を実行しているサーバーを使用するクライアント コンピューターが続行します。 この問題を修正するには、プロキシ サーバーを使用しないように、または新しいプロキシ サーバーを使用するように、Internet Explorer を構成する必要があります。  
  
#### <a name="to-reconfigure-internet-explorer"></a>Internet Explorer を再構成するには  
  
1.  Internet Explorer で、 **[ツール]** をクリックし、 **[インターネット オプション]** をクリックします。  
  
2.  **[接続]** タブをクリックし、 **[LAN の設定]** をクリックして、次のいずれかを行います。  
  
    -   ネットワークでプロキシ サーバーを使用していない場合は、 **[ローカル エリア ネットワーク (LAN) の設定]** ダイアログ ボックスのすべてのチェック ボックスをオフにします。  
  
    -   新しいプロキシ サーバーをネットワークで使用する場合:  
  
        1.  **[ローカル エリア ネットワーク (LAN) の設定]** ダイアログ ボックスで、 **[自動構成]** セクションのチェック ボックスをオフにします。  
  
        2.  **[プロキシ サーバー]** セクションで、両方のチェック ボックスがオンになっていることを確認します。  
  
        3.  **[アドレス]** ボックスに、プロキシ サーバーの完全修飾ドメイン名 (FQDN) を入力します。  
  
        4.  **[ポート]** ボックスに「**80**」と入力します。  
  
3.  **[OK]** を 2 回クリックします。  
  
4.  Web サイトにアクセスして、接続の設定が正しいことを確認します。  
  
##  <a name="BKMK_AdminGroup"></a> 組み込みの Administrators グループにバッチ ジョブとしてログオンする権限を付与します。  
 既存の Windows Small Business Server 2003 ドメインを Windows Server Essentials に移行した後は、組み込みの Administrators グループにバッチ ジョブとしてログオンする権限を付与する必要があります。 組み込み Administrators グループに移行先サーバーにバッチ ジョブとしてログオンするための権利がまだあることを確認します。 移行先サーバーにログオンしないでアラートを実行するために、Administrators にはこの権利が必要です。  
  
#### <a name="to-give-the-built-in-administrators-group-the-right-to-log-on-as-a-batch-job"></a>組み込み Administrators グループにバッチ ジョブとしてログオンする権利を付与するには  
  
1. 移行先サーバーで、 **[グループ ポリシーの管理]** 管理ツールを開きます。  
  
2. **Group Policy Management**コンソール ツリーで、展開**フォレスト:** *< ServerName\>* ドメインを展開し、順に展開します。  
  
3. **[ドメイン コントローラー]** を展開し、 **[既定のドメイン コントローラーのポリシー]** を右クリックして、 **[編集]** をクリックします。  
  
4. **グループ ポリシー管理エディター**、 をクリックして**既定のドメイン コント ローラー ポリシー**<em>< ServerName\></em>**ポリシー**、順に展開**コンピューターの構成**します。  
  
5. **[ポリシー]** 、 **[Windows の設定]** 、 **[セキュリティの設定]** の順に展開します。  
  
6. **[セキュリティの設定]** ツリーで、 **[ローカル ポリシー]** を展開し、 **[ユーザー権利の割り当て]** をクリックします。  
  
7. 結果ウィンドウで、**バッチ ジョブとしてログオン** を右クリックして、プロパティ をクリックします。  
  
8. **[バッチ ジョブとしてログオンのプロパティ]** ページで、 **[ユーザーまたはグループの追加]** をクリックします。  
  
9. **[ユーザーまたはグループの追加]** ダイアログ ボックスで、 **[参照]** をクリックします。  
  
10. **[ユーザー、コンピューター、またはグループの選択]** ダイアログ ボックスで、「**Administrators**」と入力します。  
  
11. **[名前の確認]** をクリックして組み込み Administrators グループが表示されることを確認した後、 **[OK]** を 3 回クリックして設定を保存します。  
  
## <a name="see-also"></a>関連項目  
  

-   [Windows SBS 2003 から移行します。](Migrate-Windows-Small-Business-Server-2003-to-Windows-Server-Essentials.md)  
  
-   [サーバー データの Windows Server Essentials への移行](Migrate-Server-Data-to-Windows-Server-Essentials.md)

-   [Windows SBS 2003 から移行します。](../migrate/Migrate-Windows-Small-Business-Server-2003-to-Windows-Server-Essentials.md)  
  
-   [サーバー データの Windows Server Essentials への移行](../migrate/Migrate-Server-Data-to-Windows-Server-Essentials.md)

