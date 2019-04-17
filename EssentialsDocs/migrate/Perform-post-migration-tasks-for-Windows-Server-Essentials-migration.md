---
title: "Windows Server Essentials migration1 の移行後のタスクを実行します。"
description: "Windows Server Essentials を使用する方法について説明します。"
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
ms.openlocfilehash: 535a547ded55cb4afc0942259eadf5222a815274
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="perform-post-migration-tasks-for-windows-server-essentials-migration1"></a>Windows Server Essentials migration1 の移行後のタスクを実行します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

次のタスクを使用して、移行先サーバーと移行元サーバー上にあった同じ設定の一部の設定を完了できます。 可能性があります無効にしたこれらの設定のいくつか、移行元サーバーで、移行プロセス中にため、移行先サーバーに移行されていません。 または、オプションの構成手順を実行することがあります。  
  

-   [移行元サーバーの DNS エントリを削除します。](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_DeleteDNSEntries)  
  
-   [基幹業務アプリケーションなどのデータ フォルダーを共有します。](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_ShareLineOfBusinessAndOtherApplications)  
  
-   [移行後にクライアント コンピューターの問題を修正します。](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_FixClientComputerIssuesAfterMigrating)  
  
-   [組み込みの Administrators グループにバッチ ジョブとしてログオンする権限を付与します。](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_AdminGroup)  

-   [移行元サーバーの DNS エントリを削除します。](../migrate/Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_DeleteDNSEntries)  
  
-   [基幹業務アプリケーションなどのデータ フォルダーを共有します。](../migrate/Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_ShareLineOfBusinessAndOtherApplications)  
  
-   [移行後にクライアント コンピューターの問題を修正します。](../migrate/Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_FixClientComputerIssuesAfterMigrating)  
  
-   [組み込みの Administrators グループにバッチ ジョブとしてログオンする権限を付与します。](../migrate/Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_AdminGroup)  

  
##  <a name="BKMK_DeleteDNSEntries"></a>移行元サーバーの DNS エントリを削除します。  
 移行元サーバーを使用停止した後、ドメイン ネーム サービス (DNS) サーバーが移行元サーバーを指定するエントリを格納できます。 これらの DNS エントリを削除します。  
  
#### <a name="to-delete-dns-entries-that-point-to-the-source-server"></a>移行元サーバーをポイントする DNS エントリを削除するには  
  
1.  移行先サーバーで、開く**DNS マネージャー**します。  
  
2.  DNS マネージャーで、サーバー名を右クリックし、をクリックして**プロパティ**、クリックして、**フォワーダ**] タブ。  
  
3.  移行元サーバーを指すフォワーダー リストにエントリがあるかどうかを決定します。 ある場合、] をクリックして**編集**でそのエントリを削除し、**フォワーダの編集**ウィンドウ。  
  
4.  **DNS マネージャー**、サーバー名を展開し、展開、**前方参照ゾーン**します。  
  
5.  各前方参照ゾーンのゾーンを右クリックして] をクリックして**プロパティ**、クリックして、**ネーム サーバー** ] タブ。  
  
6.  エントリをクリックして、**ネーム サーバー**、移行元サーバーへのポインター クリックしてボックス**削除**、] をクリックし、**[OK]**します。  
  
7.  移行元サーバーにすべてのポインターが削除されるまで、手順 5 と 6 を繰り返します。  
  
8.  をクリックして**OK**を閉じるには、**プロパティ**ウィンドウ。  
  
9. **DNS マネージャー**コンソールで、[**逆引き参照ゾーン**します。  
  
10. 手順 6 ~ 9、移行元サーバーをポイントするすべての逆引き参照ゾーンを削除する.  
  
##  <a name="BKMK_ShareLineOfBusinessAndOtherApplications"></a>基幹業務アプリケーションなどのデータ フォルダーを共有します。  
 共有フォルダーのアクセス許可と、基幹業務と移行先サーバーにコピーしたその他のアプリケーション データ フォルダーの NTFS アクセス許可を設定する必要があります。 アクセス許可を設定すると、共有フォルダーが表示される、Windows Server Essentials ダッシュ ボードで、**記憶域**セクションです。  
  
 共有フォルダーにドライブをマップするをログオン スクリプトを使用している場合、移行先サーバー上のドライブにマップするスクリプトを更新する必要があります。  
  
##  <a name="BKMK_FixClientComputerIssuesAfterMigrating"></a>移行後にクライアント コンピューターの問題を修正します。  
 Windows Small Business Server 2003 Premium Edition では、Microsoft Internet Security と Acceleration (ISA) Server がインストールされているから Windows Server Essentials に移行する場合、ネットワーク上のクライアント コンピューターはまだ Microsoft ファイアウォール クライアントと Internet Explorer プロキシ サーバーを使用するように構成します。  
  
 これにより、接続の問題、クライアント コンピューター、プロキシ サーバーが存在しないため。 構成されている別のプロキシ サーバーがある場合、クライアント コンピューターは引き続き、プロキシ サーバーの Windows SBS 2003 を実行しているサーバーを使用します。 この問題を修正するのには、Internet Explorer のプロキシ サーバーを使用しないように、または新しいプロキシ サーバーを使用するを再構成する必要があります。  
  
#### <a name="to-reconfigure-internet-explorer"></a>Internet Explorer を再構成するには  
  
1.  Internet Explorer で、をクリックして**ツール**、] をクリックし、**インターネット オプション**します。  
  
2.  をクリックして、**接続**] タブ、[ **LAN の設定**、次のいずれかの操作を実行します。  
  
    -   ネットワークでプロキシ サーバーを使用していない場合は、内のすべてのチェック ボックスをオフ、**ローカル エリア ネットワーク (LAN) の設定**] ダイアログ ボックス。  
  
    -   ネットワーク上で新しいプロキシ サーバーを使用する場合は。  
  
        1.  **ローカル エリア ネットワーク (LAN) の設定**] ダイアログ ボックスで、チェック ボックスをオンにクリア、**自動構成**セクションです。  
  
        2.  **プロキシ サーバー**セクションで、両方のチェック ボックスが選択されていることを確認します。  
  
        3.  **アドレス**ボックスに、プロキシ サーバーの完全修飾ドメイン名 (FQDN) を入力します。  
  
        4.  **ポート**ボックスに、入力**80**します。  
  
3.  をクリックして**OK** 2 回クリックします。  
  
4.  接続の設定が正しいことを確認する Web サイトを参照します。  
  
##  <a name="BKMK_AdminGroup"></a>組み込みの Administrators グループにバッチ ジョブとしてログオンする権限を付与します。  
 既存の Windows Small Business Server 2003 ドメインを Windows Server Essentials に移行した後は、組み込みの Administrators グループにバッチ ジョブとしてログオンする権限を付与する必要があります。 組み込み Administrators グループにも移行先サーバーにバッチ ジョブとしてログオンする権利があることを確認します。 管理者には、ログオンしなくても、移行先サーバーで、アラートを実行するには、この権限が必要があります。  
  
#### <a name="to-give-the-built-in-administrators-group-the-right-to-log-on-as-a-batch-job"></a>管理者グループにバッチ ジョブとしてログオンする権利を組み込みを提供するには  
  
1.  移行先サーバーで、開く、**グループ ポリシーの管理**管理ツールです。  
  
2.  **グループ ポリシーの管理**コンソール ツリーを展開し、**フォレスト:***< ServerName\ >*、ドメインを展開し、サーバーを展開します。  
  
3.  展開**ドメイン コントローラー**、右クリック**既定のドメイン コントローラー ポリシー**、] をクリックし、**編集**します。  
  
4.  **グループ ポリシー管理エディター**、] をクリックして**既定のドメイン コントローラー ポリシー***< ServerName\ >***ポリシー**、し、展開**コンピューターの構成**します。  
  
5.  展開**ポリシー**、展開**Windows 設定**、し、展開**セキュリティ設定**します。  
  
6.  **セキュリティ設定**ツリーを展開し、**ローカル ポリシー**、] をクリックし、**ユーザー権利の割り当て**します。  
  
7.  結果ウィンドウで右クリックして**バッチ ジョブとしてログオン**、し、[プロパティ] をクリックします。  
  
8.  **プロパティ バッチ ジョブとしてログオン**] ページで [ **[ユーザーまたはグループ**します。  
  
9. **[ユーザーまたはグループ**ダイアログ ボックスで、をクリックして**参照**します。  
  
10. **[ユーザー、コンピューター、またはグループ**] ダイアログ ボックスで、「**管理者**します。  
  
11. をクリックして**名前の確認**いることを確認、組み込み Administrators グループが表示されたら、をクリックする**OK** 3 回設定を保存します。  
  
## <a name="see-also"></a>参照してください。  
  

-   [Windows SBS 2003 からの移行します。](Migrate-Windows-Small-Business-Server-2003-to-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials へのサーバー データを移行します。](Migrate-Server-Data-to-Windows-Server-Essentials.md)

-   [Windows SBS 2003 からの移行します。](../migrate/Migrate-Windows-Small-Business-Server-2003-to-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials へのサーバー データを移行します。](../migrate/Migrate-Server-Data-to-Windows-Server-Essentials.md)

