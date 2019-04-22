---
title: AD フォレストの回復の完全なサーバーをバックアップします。
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 9238cb27-0020-42f7-90d6-fcebf7e3c0bc
ms.technology: identity-adds
ms.openlocfilehash: a5306960bb2dca3849bdb4fc7304781af3f25335
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59815873"
---
# <a name="ad-forest-recovery---backing-up-the-system-state-data"></a>AD フォレストの回復 - システム状態データをバックアップします。  

>適用先:Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 R2

Windows Server バックアップまたは wbadmin.exe を使用して DC のシステム状態のバックアップを実行するのにには、次の手順を使用します。  

## <a name="to-perform-a-system-state-backup-using-windows-server-backup"></a>Windows Server バックアップを使用してシステム状態バックアップを実行するには

1. 開いている**サーバー マネージャー**、 をクリックして**ツール**、 をクリックし、 **Windows Server バックアップ**します。
   - Windows Server 2008 R2 および Windows Server 2008 では、次のようにクリックします。**開始**、 をポイント**管理ツール**、 をクリックし、 **Windows Server バックアップ**します。 

   ![バックアップをインストールします。](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup1.png)

2. 求められた場合、**ユーザー アカウント制御**ダイアログ ボックスで、バックアップ オペレーターの資格情報を入力し、順にクリックします**OK**します。
3. クリックして**ローカル バックアップ**します。
4. **[操作]** メニューの **[バックアップ (1 回限り)]** をクリックします。
5. バックアップ 1 回ウィザードで、上、**バックアップ オプション**] ページで [**さまざまなオプション**、順にクリックします **[次へ]** します。

   ![バックアップをインストールします。](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup3.png)

6. **[バックアップ構成] を**] ページで [**カスタム)**、順にクリックします**次**します。
7. **バックアップ項目を選択**画面で、[**項目の追加**を選択し、**システム状態**] をクリック**Ok**します。
   - Windows Server 2008 R2 および Windows Server 2008 では、バックアップに含めるために、ボリュームを選択します。 選択した場合、**システム回復を有効にする**チェック ボックスで、すべての重要なボリュームが選択されています。 

   ![バックアップをインストールします。](media/AD-Forest-Recovery-Backing-up-System-State/systemstatebackup.png)  

8. **変換先の型を指定**] ページで [**ローカル ドライブ**または**リモート共有フォルダー**、順にクリックします**次**。  リモート共有フォルダーをバックアップする場合は、次の操作を行います。  
   - 共有フォルダーへのパスを入力します。
   - **アクセス制御**を選択します**継承しない**または**継承**をクリックして、バックアップへのアクセスを決定**次**。  
   - **バックアップのユーザーの資格情報を提供** ダイアログ ボックスで、共有フォルダーへの書き込みアクセス権を持つユーザーのユーザー名とパスワードを入力し、順にクリックします**OK**します。

9. Windows Server 2008 R2 および Windows Server 2008 では、上、**詳細オプションを指定する**] ページで、[ **VSS コピー バックアップ**順にクリックします **[次へ]** します。
10. **バックアップ先の選択**ページで、バックアップの場所を選択します。  ドライブがローカル ドライブを選択してローカルを選択した場合、またはリモートで選択した場合、共有は、ネットワーク共有を選択します。
11. 確認画面で、をクリックして**バックアップ**します。
12. これが完了したら、クリックして**閉じる**します。
13. Windows Server バックアップを閉じます。

## <a name="to-perform-a-system-state-backup-using-wbadminexe"></a>Wbadmin.exe を使用してシステム状態バックアップを実行するには

管理者特権のコマンド プロンプトを開き、次のコマンドを入力し、ENTER キーを押します。  
  
   ```
   wbadmin start systemstatebackup -backuptarget:<targetDrive>:
   ```

   ![バックアップをインストールします。](media/AD-Forest-Recovery-Backing-up-System-State/systemstatebackup2.png)  

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)
