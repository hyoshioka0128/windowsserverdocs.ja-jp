---
title: 手順 7:Windows Server Essentials の移行の移行後のタスクを実行します。
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d382e3fd-d393-4bd0-883f-db50104a969f
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 6a61d28f29097bcb6993a471587f4cc1ae0bcc3f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819163"
---
# <a name="step-7-perform-post-migration-tasks-for-the-windows-server-essentials-migration"></a>手順 7:Windows Server Essentials の移行の移行後のタスクを実行します。

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

以下のタスクでは、移行元サーバーと部分的に同じ設定で移行先サーバーのセットアップを終了します。 移行プロセスの間に移行元サーバーで無効にした設定は、移行先サーバーに移行されていません。  
  
1.  [移行元サーバーの DNS エントリを削除します。](Step-7--Perform-post-migration-tasks-for-the-Windows-Server-Essentials-migration.md#BKMK_DeleteDNSEntries)  
  
2.  [基幹業務およびその他のアプリケーション データ フォルダーを共有します。](Step-7--Perform-post-migration-tasks-for-the-Windows-Server-Essentials-migration.md#BKMK_ShareLineOfBusinessAndOtherApplications)  
  
##  <a name="BKMK_DeleteDNSEntries"></a> 移行元サーバーの DNS エントリを削除します。  
 移行元サーバーを使用停止した後、ドメイン ネーム サービス (DNS) サーバーに移行元サーバーを参照しているエントリがまだ含まれる場合があります。 そのような DNS エントリを削除します。  
  
#### <a name="to-delete-dns-entries-that-point-to-the-source-server"></a>移行元サーバーを指定する DNS エントリを削除するには  
  
1.  移行先サーバーで **[DNS マネージャー]** を開きます。  
  
2.  DNS マネージャーでサーバー名をクリックし、**[プロパティ]** をクリックして、**[フォワーダー]** タブをクリックします。  
  
3.  移行元サーバーを参照しているエントリがフォワーダー リストにあるかどうかを確認します。 ある場合、**[編集]** をクリックし、**[フォワーダーの編集]** ウィンドウでそのエントリを削除します。  
  
4.  **[DNS マネージャー]** で、サーバー名を展開し、**[前方参照ゾーン]** を展開します。  
  
5.  前方参照ゾーンごとに、ゾーンを右クリックし、**[プロパティ]** をクリックして、**[ネーム サーバー]** タブをクリックします。  
  
6.  移行元サーバーを参照している **[ネーム サーバー]** ボックス内のエントリを選択し、**[削除]** をクリックして、**[OK]** をクリックします。  
  
7.  手順 5 と 6 を繰り返して、移行元サーバーに対するポインターをすべて削除します。  
  
8.  **[OK]** をクリックして、**[プロパティ]** ウィンドウを閉じます。  
  
9. **[DNS マネージャー]** で **[逆引き参照ゾーン]** を展開します。  
  
10. 手順 6 ～ 9 を繰り返して、移行元サーバーを指定する逆引き参照ゾーンをすべて削除します。  
  
##  <a name="BKMK_ShareLineOfBusinessAndOtherApplications"></a> 基幹業務およびその他のアプリケーション データ フォルダーを共有します。  
 基幹業務アプリケーションなどのアプリケーションのデータ フォルダーを移行先サーバーにコピーした後で、そのフォルダーに共有フォルダーのアクセス許可と NTFS アクセス許可を設定する必要があります。 アクセス許可を設定すると、ダッシュボードの **[記憶域]** タブに共有フォルダーが表示されるようになります。  
  
 ログオン スクリプトを使用してドライブを共有フォルダーに割り当てている場合、移行先サーバー上のドライブに割り当てを行うためのスクリプトを更新する必要があります。  
  
## <a name="next-steps"></a>次のステップ  
 Windows Server Essentials への移行の移行後のタスクを実行しました。 次に「[手順 8 - Windows Server Essentials ベスト プラクティス アナライザーを実行](Step-8--Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md)します。  
  

すべての手順を表示するを参照してください。 [Windows Server Essentials への移行](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)します。

