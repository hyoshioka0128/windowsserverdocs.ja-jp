---
title: Windows Server Essentials のファイル履歴に関するトラブルシューティング
description: Windows Server Essentials を使用する方法について説明します
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
ms.openlocfilehash: f080bed5714ae4426cc6d0ca8edb5fab2d3c65b2
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66432472"
---
# <a name="troubleshoot-file-history-in-windows-server-essentials"></a>Windows Server Essentials のファイル履歴に関するトラブルシューティング

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials 
  
## <a name="troubleshoot-issues-with-user-file-history-backups"></a>ユーザーのファイル履歴のバックアップに関する問題のトラブルシューティング  
 Windows Server Essentials が実行されているサーバーに追加されたユーザーまたはコンピューターのファイル履歴のバックアップを管理するときに、次の問題が生じる場合があります。  
  
### <a name="file-history-data-is-not-automatically-deleted"></a>ファイル履歴が自動削除されない  
 次の場合に、ファイル履歴データが自動的に削除されない可能性があります。  
  
- ユーザー アカウントを削除するときに、s ファイル履歴データ、ユーザー アカウントは削除を選択し、データを手動で削除することを選択します。  
  
- ファイル履歴データを削除するときに、そのファイル履歴データが他のプロセスで使用中の場合。  
  
  この問題を解決するには、次の手順を実行してファイル履歴を手動で削除しなければなりません。  
  
####  <a name="BKMK_manuallyDelete"></a> ユーザーまたはコンピューターのファイル履歴のバックアップを手動で削除するには  
  
1.  管理者としてサーバーにログオンします。  
  
2.  管理者としてエクスプローラーを実行します。  
  
3.  File History Backups フォルダーに移動します。 既定の場所は C:\ServerFolders\File History Backups です。  
  
4.  File History Backups に格納されている共有フォルダーを次のようにして削除します。  
  
    -   ユーザーのファイル履歴を削除するには、ユーザーの名前を持つ File History backup 子フォルダーを削除します。  
  
    -   コンピューターのファイル履歴を削除する場合には、そのコンピューター名の File History backup 子フォルダーを削除します。 たとえば、ユーザーが提供終了 < MyComputer01\>新しいラップトップ コンピューターで作業を開始後に < MyComputer02\>、C:\ServerFolders\File History Backups を削除する\\< MyAccount\> \\< MyComputer01\>ことはすべてのファイルとフォルダーを新しいラップトップ コンピューターに転送が必要としないファイル履歴の今後のユーザーに確認した後。  
  
### <a name="cannot-apply-file-history-setting-to-a-new-user"></a>新しいユーザーにファイル履歴の設定を適用できない  
 新しいユーザーを追加する場合に、そのユーザー名が、Windows Server Essentials から削除したことがあるユーザーのユーザー名と同じであると、新しいユーザーのファイル履歴構成で障害が生じる可能性があります。Windows Server Essentials によって新しいユーザーのファイル履歴を格納するためのフォルダーの作成が試行されるときに、名前付けの競合が生じるためです。 この問題を解決するには、削除したファイル履歴フォルダーの名前を変更できます。  
  
##### <a name="to-locate-user-file-history-on-the-server"></a>サーバー上にあるユーザーのファイル履歴の場所を特定するには  
  
1.  管理者としてサーバーにログオンします。  
  
2.  Windows Server Essentials ダッシュボードで、 **[記憶域]** をクリックします。  
  
3.  **[サーバー フォルダー]** タブで、File History Backups フォルダーの場所に注目します。 既定の場所は %SystemDrive%\ServerFolders\File History Backups\\します。  
  
##### <a name="to-resolve-file-history-issues-for-a-new-user-with-a-name-conflict"></a>名前が競合している新しいユーザーのファイル履歴問題を解決するには  
  
1.  管理者としてサーバーにログオンします。  
  
2.  管理者としてエクスプローラーを実行します。  
  
3.  File History Backups フォルダーに移動します。 既定の場所は C:\ServerFolders\File History Backups です。  
  
     File History Backups フォルダーには、Windows Server Essentials に追加された各ユーザー アカウントのサブフォルダーが含まれています。 たとえば、ユーザー John Smith のファイル履歴は、サブフォルダー File History Backups\JohnSmith に格納されます。  
  
4.  たとえば、削除したユーザーのサブフォルダーの名前を変更 **< *UserName*> _Deleted**します。 ユーザーのファイル履歴が不要な場合には、そのフォルダーを削除できます。  
  

5.  これで、新しいユーザーを追加できます。 手順については、ユーザー アカウントの追加を参照してください。[ユーザー アカウントを管理する](../manage/Manage-User-Accounts-in-Windows-Server-Essentials.md)します。  
  
### <a name="a-user-account-was-removed-but-the-users-file-history-remains"></a>ユーザー アカウントは削除したものの、ユーザーのファイル履歴が残っている  
 ネットワーク管理者がサーバーからユーザーまたはコンピューターの削除を選択したものの、将来の使用に備えてファイル履歴のバックアップの保持を選択することがあります。 対象のファイル履歴が不要な場合には、対象ユーザーまたはコンピューターの File History Backups フォルダーを、サーバー上の共有フォルダーから削除します。 その方法については、「 [To manually delete File History backups for a user or a computer](Troubleshoot-File-History-in-Windows-Server-Essentials.md#BKMK_manuallyDelete)」をご覧ください。  

5. これで、新しいユーザーを追加できます。 手順については、ユーザー アカウントの追加を参照してください。[ユーザー アカウントを管理する](../manage/Manage-User-Accounts-in-Windows-Server-Essentials.md)します。  
  
### <a name="a-user-account-was-removed-but-the-users-file-history-remains"></a>ユーザー アカウントは削除したものの、ユーザーのファイル履歴が残っている  
 ネットワーク管理者がサーバーからユーザーまたはコンピューターの削除を選択したものの、将来の使用に備えてファイル履歴のバックアップの保持を選択することがあります。 対象のファイル履歴が不要な場合には、対象ユーザーまたはコンピューターの File History Backups フォルダーを、サーバー上の共有フォルダーから削除します。 その方法については、「 [To manually delete File History backups for a user or a computer](../support/Troubleshoot-File-History-in-Windows-Server-Essentials.md#BKMK_manuallyDelete)」をご覧ください。  

  
## <a name="see-also"></a>関連項目  
  
-   [クライアント バックアップを管理します。](../manage/Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md)  
  

-   [Windows Server Essentials のサポート](Support-Windows-Server-Essentials.md)

-   [Windows Server Essentials のサポート](../support/Support-Windows-Server-Essentials.md)

