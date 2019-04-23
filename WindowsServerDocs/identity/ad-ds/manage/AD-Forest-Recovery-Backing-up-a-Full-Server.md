---
title: AD フォレストの回復の完全なサーバーをバックアップします。
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 398918dc-c8ab-41a6-a377-95681ec0b543
ms.technology: identity-adds
ms.openlocfilehash: fec8de8ea1dadb392f6a3bd1c881e8df2266f404
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59846523"
---
# <a name="ad-forest-recovery---backing-up-a-full-server"></a>AD フォレストの回復の完全なサーバーをバックアップします。  

>適用先:Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 R2

別のハードウェアまたはオペレーティング システムの異なるインスタンスに復元できるため、フォレストの回復に備えるには、サーバーの完全バックアップをお勧めします。  Windows Server バックアップを使用して、サーバーの完全バックアップを実行することができます。 

## <a name="windows-server-backup"></a>Windows Server バックアップ

既定では、Windows Server バックアップがインストールされていません。 Windows Server 2016 および Windows Server 2012 R2 では、次の手順に従ってインストールします。

>[!NOTE]
>手順は、Windows Server 2016 および Windows Server 2012 R2 の間で若干異なる場合がありますに注意してください。

Windows Server 2008 および Windows Server 2008 R2 にインストールする手順については、次を参照してください。[をインストールする Windows Server バックアップ](https://technet.microsoft.com/library/cc771232.aspx)します。  

### <a name="to-install-windows-server-backup"></a>Windows Server バックアップをインストールするには

1. 開いている**サーバー マネージャー**  をクリック**役割と機能の追加**します。
2. **追加の役割と機能ウィザード**クリックして **[次へ]** します。
3. **インストールの種類**画面で、既定値のままに**役割ベースまたは機能ベースのインストール** をクリック**次**します。
4. **サーバーの選択**画面で、**次**します。
5. **サーバーの役割**画面をクリック**次**します。
6. **機能**画面で、**[Windows Server バックアップ]** をクリック**次**
   ![バックアップのインストール](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup2.png)
7. **[インストール]** をクリックします。
8. インストールが完了したらクリックして**閉じる**します。

### <a name="to-perform-a-backup-with-windows-server-backup"></a>Windows Server バックアップでバックアップを実行するには

1. 開いている**サーバー マネージャー**、 をクリックして**ツール**、 をクリックし、 **Windows Server バックアップ**します。
   - Windows Server 2008 R2 および Windows Server 2008 では、次のようにクリックします。**開始**、 をポイント**管理ツール**、 をクリックし、 **Windows Server バックアップ**します。

   ![バックアップをインストールします。](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup1.png) 

2. 求められた場合、**ユーザー アカウント制御**ダイアログ ボックスで、バックアップ オペレーターの資格情報を入力し、順にクリックします**OK**します。
3. クリックして**ローカル バックアップ**します。
4. **[操作]** メニューの **[バックアップ (1 回限り)]** をクリックします。
5. バックアップ 1 回ウィザードで、上、**バックアップ オプション**] ページで [**さまざまなオプション**、順にクリックします **[次へ]** します。

   ![バックアップをインストールします。](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup3.png)

6. **[バックアップ構成] を**] ページで [**サーバー全体 (推奨)**、順にクリックします **[次へ]** します。
7. **変換先の型を指定**] ページで [**ローカル ドライブ**または**リモート共有フォルダー**、順にクリックします**次**。
8. **バックアップ先の選択**ページで、バックアップの場所を選択します。  ドライブがローカル ドライブを選択してローカルを選択した場合、またはリモートで選択した場合、共有は、ネットワーク共有を選択します。
9. 確認画面で、をクリックして**バックアップ**します。

   ![バックアップをインストールします。](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup4.png)

10. これが完了したら、クリックして**閉じる**します。
11. Windows Server バックアップを閉じます。

>[!NOTE]
>バックアップ記憶域の場所が使用可能なないことを示すエラーが発生した場合は、選択されたボリュームのいずれかを除外するか、新しいボリュームまたはリモート共有を追加する必要があります。
>選択したボリュームがバックアップする項目の一覧にも含まれていることを示す警告が発生した場合は削除し、をクリックするかどうかを決定**Ok**します。

## <a name="using-wbadminexe-to-backup-a-windows-server"></a>Wbadmin.exe を使用して、windows server をバックアップするには

Wbadmin.exe では、コマンド ライン ユーティリティをバックアップし、コマンド プロンプトから、オペレーティング システム、ボリューム、ファイル、フォルダー、およびアプリケーションを復元することができます。

### <a name="to-perform-a-full-server-backup-using-wbadminexe"></a>Wbadmin.exe を使用してサーバーの完全バックアップを実行するには
  
- 管理者特権のコマンド プロンプトを開き、次のコマンドを入力し、ENTER キーを押します。  

   ```
   wbadmin start backup -backuptarget:<Drive_letter_to store_backup>: -include:<Drive_letter_to_include>:
   ```

   ![バックアップをインストールします。](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup5.png)

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)
