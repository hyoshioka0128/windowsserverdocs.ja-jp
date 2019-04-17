---
title: "手順 7: Windows Server Essentials 移行の移行後のタスクを実行します。"
description: "Windows Server Essentials を使用する方法について説明します。"
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
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="step-7-perform-post-migration-tasks-for-the-windows-server-essentials-migration"></a>手順 7: Windows Server Essentials 移行の移行後のタスクを実行します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

次のタスクを使用して、移行先サーバーと移行元サーバー上にあった同じ設定の一部の設定を完了できます。 可能性があります無効にしたこれらの設定のいくつか、移行元サーバーで、移行プロセス中にため、移行先サーバーに移行されていません。  
  
1.  [移行元サーバーの DNS エントリを削除します。](Step-7--Perform-post-migration-tasks-for-the-Windows-Server-Essentials-migration.md#BKMK_DeleteDNSEntries)  
  
2.  [基幹業務アプリケーションなどのデータ フォルダーを共有します。](Step-7--Perform-post-migration-tasks-for-the-Windows-Server-Essentials-migration.md#BKMK_ShareLineOfBusinessAndOtherApplications)  
  
##  <a name="BKMK_DeleteDNSEntries"></a>移行元サーバーの DNS エントリを削除します。  
 移行元サーバーを使用停止した後、ドメイン ネーム サービス (DNS) サーバーが移行元サーバーを指定するエントリを格納できます。 これらの DNS エントリを削除します。  
  
#### <a name="to-delete-dns-entries-that-point-to-the-source-server"></a>移行元サーバーをポイントする DNS エントリを削除するには  
  
1.  移行先サーバーで、開く**DNS マネージャー**します。  
  
2.  DNS マネージャーで、サーバー名を右クリックし、をクリックして**プロパティ**、クリックして、**フォワーダ**] タブ。  
  
3.  移行元サーバーを指すフォワーダー リストにエントリがあるかどうかを決定します。 ある場合、] をクリックして**編集**でそのエントリを削除し、**フォワーダの編集**ウィンドウ。  
  
4.  **DNS マネージャー**、サーバー名を展開し、展開、**前方参照ゾーン**します。  
  
5.  各前方参照ゾーンのゾーンを右クリックして] をクリックして**プロパティ**、クリックして、**ネーム サーバー** ] タブ。  
  
6.  内のエントリを選択、**ネーム サーバー**、移行元サーバーへのポインターの [テキスト ボックス**を削除する**、] をクリックし、**OK**します。  
  
7.  移行元サーバーにすべてのポインターが削除されるまで、手順 5 と 6 を繰り返します。  
  
8.  をクリックして**OK**を閉じるには、**プロパティ**ウィンドウ。  
  
9. **DNS マネージャー**、展開**逆引き参照ゾーン**します。  
  
10. 手順 6 ~ 9、移行元サーバーをポイントするすべての逆引き参照ゾーンを削除する.  
  
##  <a name="BKMK_ShareLineOfBusinessAndOtherApplications"></a>基幹業務アプリケーションなどのデータ フォルダーを共有します。  
 共有フォルダーのアクセス許可と、基幹業務と移行先サーバーにコピーしたその他のアプリケーション データ フォルダーの NTFS アクセス許可を設定する必要があります。 アクセス許可を設定すると、共有フォルダーが表示される、ダッシュ ボードで、**記憶域**] タブ。  
  
 共有フォルダーにドライブをマップするをログオン スクリプトを使用している場合、移行先サーバー上のドライブにマップするスクリプトを更新する必要があります。  
  
## <a name="next-steps"></a>次の手順  
 Windows Server Essentials 移行の移行後のタスクを実行しました。 移動できるようになりました[手順 8 - Windows Server Essentials ベスト プラクティス アナライザーを実行](Step-8--Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md)します。  
  

すべての手順を参照してください[Windows Server Essentials への移行](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)します。

