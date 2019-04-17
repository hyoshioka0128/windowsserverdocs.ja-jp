---
title: "AD フォレストの回復 - フル サーバーのバックアップ"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 9238cb27-0020-42f7-90d6-fcebf7e3c0bc
ms.technology: identity-adfs
ms.openlocfilehash: a86d61536f8b426e1a5258c661d4e53da63d4162
ms.sourcegitcommit: 84a2bdcb92ba6af45781fab9727617e50fa5e911
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2017
---
# <a name="ad-forest-recovery---backing-up-the-system-state-data"></a>AD フォレストの回復 - システム状態データをバックアップします。  

>Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 の R2 を適用対象:
 
Windows Server バックアップまたは wbadmin.exe を使用して、DC でシステム状態のバックアップを実行するのにには、次の手順を使用します。  
  
## <a name="to-perform-a-system-state-backup-using-windows-server-backup"></a>Windows Server バックアップを使用してシステム状態バックアップを実行するには  
1. 開いている**サーバー マネージャー**、] をクリックして**ツール**、] をクリックし、 **Windows Server バックアップ**します。
    - Windows Server 2008 R2 および Windows Server 2008 では、をクリックして**開始**、] をポイント**管理ツール**、] をクリックし、 **Windows Server バックアップ**します。 
![バックアップをインストールします。](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup1.png) 
2. 求められた場合で、**ユーザー アカウント制御**ダイアログ ボックスで、バックアップ オペレーターの資格情報を提供し、をクリックして**OK**します。
3. をクリックして**ローカル バックアップ**します。
4. **アクション**] メニューのをクリックして**1 回バックアップ**します。
5. バックアップ 1 回ウィザードで、上、**バックアップ オプション**] ページで [**さまざまなオプション**、] をクリックし、 **[次へ]**します。
![バックアップをインストールします。](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup3.png)
6. **バックアップ構成の選択**] ページで [**カスタム)**、] をクリックし、 **[次へ]**します。
7. **バックアップ項目を選択**画面で、[**項目の追加**選択**システム状態**] をクリック**Ok**します。
    - Windows Server 2008 R2、Windows Server 2008 では、バックアップに含めるために、ボリュームを選択します。 選択した場合、**システム回復を有効にする**] チェック ボックスをすべての重要なボリュームを選択します。 
![バックアップをインストールします。](media/AD-Forest-Recovery-Backing-up-System-State/systemstatebackup.png)  
8. **移行先の種類を指定**] ページで [**ローカル ドライブ**または**リモート共有フォルダー**、] をクリックし、 **[次へ]**します。  リモート共有フォルダーをバックアップする場合は、次の操作を行います。  
  
 1.  共有フォルダーへのパスを入力します。  
 2.  下にある**アクセス制御**[**を継承しません**または**継承**、バックアップへのアクセスを決定し、[ **[次へ]**します。  
 3.  **バックアップのユーザーの資格情報を提供する**] ダイアログ ボックスで、共有フォルダーへの書き込みアクセス権を持つユーザーのユーザー名とパスワードを入力し、をクリックして**OK**します。
9. Windows Server 2008 R2 および Windows Server 2008 では、上、**詳細オプションを指定する**] ページで、[ **VSS コピー バックアップ**] をクリックし、 **[次へ]**します。
10. **バックアップ先の選択**ページで、バックアップの場所を選択します。  ローカルで選択した場合、ドライブは、ローカル ドライブを選択またはリモートで選択した場合、共有はネットワーク共有を選択します。
11. 確認画面で、をクリックして**バックアップ**します。
12. この手順が完了したら、クリックして**閉じる**します。
13. Windows Server バックアップを閉じます。

  
## <a name="to-perform-a-system-state-backup-using-wbadminexe"></a>Wbadmin.exe を使用してシステム状態バックアップを実行するには  
  
1.  管理者特権でコマンド プロンプトを開き、次のコマンドを入力し、ENTER キーを押します。  
  
    ```  
    wbadmin start systemstatebackup -backuptarget:<targetDrive>:
    ```  
![バックアップをインストールします。](media/AD-Forest-Recovery-Backing-up-System-State/systemstatebackup2.png)  

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)
