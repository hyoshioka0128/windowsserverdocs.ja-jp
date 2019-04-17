---
title: "Windows Server Essentials でのファイル履歴に関するトラブルシューティングします。"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ed062945-27e9-4572-b1bb-6c8cf1b9c2f4
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 34442565b54b089064c1fa19317a24f591e44fda
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="troubleshoot-file-history-in-windows-server-essentials"></a>Windows Server Essentials でのファイル履歴に関するトラブルシューティングします。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象: 
  
## <a name="troubleshoot-issues-with-user-file-history-backups"></a>ユーザーのファイル履歴のバックアップに関する問題をトラブルシューティングします。  
 ユーザーまたは Windows Server Essentials を実行するサーバーに追加されたコンピューターのファイル履歴のバックアップの管理中に、次の問題が発生します。  
  
### <a name="file-history-data-is-not-automatically-deleted"></a>ファイル履歴データが自動的に削除されません。  
 ファイル履歴データ可能性がありますいない取得場合自動的に削除します。  
  
-   ユーザー アカウントを削除するには、するされません s ファイル履歴データ、ユーザー アカウントの削除を選択し、データを手動で削除することを選択します。  
  
-   ファイル履歴データを削除するときに、ファイル履歴データは、他のプロセスが使用します。  
  
 この問題を解決するのには、手動で、次の手順を使用して、ファイル履歴を削除する必要があります。  
  
####  <a name="BKMK_manuallyDelete"></a>ユーザーまたはコンピューターのファイル履歴のバックアップを手動で削除するには  
  
1.  管理者としてサーバーにログオンします。  
  
2.  ファイル エクスプ ローラーを管理者として実行します。  
  
3.  File History Backups フォルダーに移動します。 既定の場所は、C:\ServerFolders\File History Backups です。  
  
4.  ファイル履歴バックアップを格納する共有フォルダーを削除します。  
  
    -   ユーザーのファイル履歴を削除するには、ユーザーの名前を持つファイル History backup 子フォルダーを削除します。  
  
    -   コンピューターのファイル履歴を削除するには、コンピューター名を持つファイル History backup 子フォルダーを削除します。 たとえば、ユーザーは、新しいラップトップ コンピューター < MyComputer02\ > で作業を開始した後、< MyComputer01\ > をインベントリから削除する場合を削除する C:\ServerFolders\File 履歴 Backups\\ < MyAccount\ > \\ < MyComputer01\ > を新しいラップトップすべてのファイルとフォルダーが転送し、不要になったファイル履歴が将来彼女のユーザーに確認した後です。  
  
### <a name="cannot-apply-file-history-setting-to-a-new-user"></a>新しいユーザーにファイル履歴の設定を適用することはできません。  
 ユーザー名が Windows Server Essentials から削除されたユーザーのユーザー名と同じですが、新しいユーザーを追加する場合、新しいユーザーのファイル履歴構成可能性があります Windows Server Essentials は、新しいユーザーのファイル履歴を保存するフォルダーを作成しようとすると名前付けの競合のため失敗します。 この問題を解決するには、削除されたユーザーのファイル履歴フォルダーに名前を変更することができます。  
  
##### <a name="to-locate-user-file-history-on-the-server"></a>サーバー上のファイル履歴のユーザーを検索するには  
  
1.  管理者としてサーバーにログオンします。  
  
2.  Windows Server Essentials ダッシュ ボード] をクリックして**記憶域**します。  
  
3.  **サーバー フォルダー** ] タブで、File History Backups フォルダーの場所に注意してください。 既定の場所は、%SystemDrive%\ServerFolders\File 履歴 Backups\\ です。  
  
##### <a name="to-resolve-file-history-issues-for-a-new-user-with-a-name-conflict"></a>名前の競合している新しいユーザーのファイル履歴問題を解決するのには  
  
1.  管理者としてサーバーにログオンします。  
  
2.  ファイル エクスプ ローラーを管理者として実行します。  
  
3.  File History Backups フォルダーに移動します。 既定の場所は、C:\ServerFolders\File History Backups です。  
  
     File History Backups フォルダーは、Windows Server Essentials に追加されたユーザー アカウントごとにサブフォルダーを持ちます。 たとえば、ユーザー John Smith のファイル履歴は、サブフォルダー File History backups \johnsmith に保存されます。  
  
4.  たとえば、削除したユーザーのサブフォルダーの名前**<*UserName*> _Deleted * * します。 ユーザーのファイル履歴が不要になった必要がある場合は、フォルダーを削除することができます。  
  

5.  新しいユーザーを追加できます。 手順については、ユーザー アカウントの追加を参照してください。[ユーザー アカウントの管理](../manage/Manage-User-Accounts-in-Windows-Server-Essentials.md)します。  
  
### <a name="a-user-account-was-removed-but-the-users-file-history-remains"></a>ユーザー アカウントは削除されましたが、ユーザーのファイル履歴が残っています。  
 場合によっては、ユーザーまたはコンピューター、サーバーから削除するが、将来の使用に備えてバックアップ ファイルの履歴を保存するネットワーク管理者こともできます。 ファイル履歴が不要になった必要がある場合は、サーバー上の共有フォルダーから、ユーザーまたはコンピューターの File History Backups フォルダーを削除します。 これを行うには、次を参照してください。[ユーザーまたはコンピューターのファイル履歴のバックアップを手動で削除](Troubleshoot-File-History-in-Windows-Server-Essentials.md#BKMK_manuallyDelete)します。  

5.  新しいユーザーを追加できます。 手順については、ユーザー アカウントの追加を参照してください。[ユーザー アカウントの管理](../manage/Manage-User-Accounts-in-Windows-Server-Essentials.md)します。  
  
### <a name="a-user-account-was-removed-but-the-users-file-history-remains"></a>ユーザー アカウントは削除されましたが、ユーザーのファイル履歴が残っています。  
 場合によっては、ユーザーまたはコンピューター、サーバーから削除するが、将来の使用に備えてバックアップ ファイルの履歴を保存するネットワーク管理者こともできます。 ファイル履歴が不要になった必要がある場合は、サーバー上の共有フォルダーから、ユーザーまたはコンピューターの File History Backups フォルダーを削除します。 これを行うには、次を参照してください。[ユーザーまたはコンピューターのファイル履歴のバックアップを手動で削除](../support/Troubleshoot-File-History-in-Windows-Server-Essentials.md#BKMK_manuallyDelete)します。  

  
## <a name="see-also"></a>参照してください。  
  
-   [クライアント バックアップを管理します。](../manage/Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md)  
  

-   [Windows Server Essentials をサポートします。](Support-Windows-Server-Essentials.md)

-   [Windows Server Essentials をサポートします。](../support/Support-Windows-Server-Essentials.md)

