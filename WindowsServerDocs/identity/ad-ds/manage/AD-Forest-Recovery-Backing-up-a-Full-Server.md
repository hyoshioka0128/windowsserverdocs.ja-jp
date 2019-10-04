---
title: AD フォレストの回復-完全なサーバーのバックアップ
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 398918dc-c8ab-41a6-a377-95681ec0b543
ms.technology: identity-adds
ms.openlocfilehash: 4377c1d993b4f6d30cf8ca8a7d149b741d7f8d2f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71369363"
---
# <a name="ad-forest-recovery---backing-up-a-full-server"></a>AD フォレストの回復-完全なサーバーのバックアップ  

>適用先:Windows Server 2016、Windows Server 2012、および 2012 R2、Windows Server 2008 および 2008 R2

フォレストの回復を準備するには、サーバーの完全バックアップを使用することをお勧めします。これは、別のハードウェアや別のオペレーティングシステムのインスタンスに復元できるためです。  Windows Server バックアップを使用すると、サーバーの完全バックアップを実行できます。 

## <a name="windows-server-backup"></a>Windows Server バックアップ

Windows Server バックアップは、既定ではインストールされません。 Windows Server 2016 および Windows Server 2012 R2 で、次の手順に従ってインストールします。

>[!NOTE]
>Windows Server 2016 と Windows Server 2012 R2 では、手順が若干異なる場合があることに注意してください。

Windows Server 2008 および Windows Server 2008 R2 にインストールする手順については、「 [Windows Server バックアップのインストール](https://technet.microsoft.com/library/cc771232.aspx)」を参照してください。  

### <a name="to-install-windows-server-backup"></a>Windows Server バックアップをインストールするには

1. **サーバーマネージャー**を開き、 **[役割と機能の追加]** をクリックします。
2. **役割と機能の追加ウィザード**で、 **[次へ]** をクリックします。
3. **[インストールの種類]** 画面で、既定の**役割ベースまたは機能ベースのインストール**をそのまま使用し、 **[次へ]** をクリックします。
4. **[サーバーの選択]** 画面で、 **[次へ]** をクリックします。
5. **[サーバーの役割]** 画面で、 **[次へ]** をクリックします。
6. **[機能]** 画面で、[ **Windows Server バックアップ**を選択し、 **[次へ]** をクリック 
    @ no__t-4install Backup @ no__t-5
7. **[インストール]** をクリックします。
8. インストールが完了したら、 **[閉じる]** をクリックします。

### <a name="to-perform-a-backup-with-windows-server-backup"></a>Windows Server バックアップでバックアップを実行するには

1. **サーバーマネージャー**を開き、 **[ツール]** をクリックし、 **[Windows Server バックアップ]** をクリックします。
   - Windows Server 2008 R2 および Windows Server 2008 で、 **[スタート]** をクリックし、 **[管理ツール]** をポイントして、 **[Windows Server バックアップ]** をクリックします。

   ![バックアップのインストール](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup1.png) 

2. メッセージが表示されたら、 **[ユーザーアカウント制御]** ダイアログボックスで、バックアップオペレーターの資格情報を入力し、[ **OK]** をクリックします。
3. **[ローカルバックアップ]** をクリックします。
4. **[操作]** メニューの **[バックアップ (1 回限り)]** をクリックします。
5. バックアップ (1 回限り) ウィザードの **[バックアップオプション]** ページで、 **[別のオプション]** をクリックし、 **[次へ]** をクリックします。

   ![バックアップのインストール](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup3.png)

6. **[バックアップ構成の選択]** ページで、 **[フルサーバー (推奨)]** をクリックし、 **[次へ]** をクリックします。
7. **[インストール先の種類の指定]** ページで、 **[ローカルドライブ]** または **[リモート共有フォルダー]** をクリックし、 **[次へ]** をクリックします。
8. **[バックアップ先の選択]** ページで、バックアップの場所を選択します。  [ローカルドライブ] を選択した場合は、ローカルドライブを選択するか、[リモート共有] を選択した場合はネットワーク共有を選択します。
9. 確認 画面で、**バックアップ** をクリックします。

   ![バックアップのインストール](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup4.png)

10. この処理が完了したら、 **[閉じる]** をクリックします。
11. Windows Server バックアップを閉じます。

>[!NOTE]
>バックアップ記憶域の場所が使用できないことを示すエラーが表示された場合は、選択されているボリュームの1つを除外するか、新しいボリュームまたはリモート共有を追加する必要があります。
>選択したボリュームがバックアップする項目の一覧にも含まれていることを示す警告が表示された場合は、削除するかどうかを判断し、[ **Ok]** をクリックします。

## <a name="using-wbadminexe-to-backup-a-windows-server"></a>Wbadmin を使用して windows server をバックアップする

Wbadmin は、コマンドプロンプトからオペレーティングシステム、ボリューム、ファイル、フォルダー、およびアプリケーションをバックアップして復元できるコマンドラインユーティリティです。

### <a name="to-perform-a-full-server-backup-using-wbadminexe"></a>Wbadmin を使用してサーバーの完全バックアップを実行するには
  
- 管理者特権のコマンドプロンプトを開き、次のコマンドを入力して、enter キーを押します。  

   ```
   wbadmin start backup -backuptarget:<Drive_letter_to store_backup>: -include:<Drive_letter_to_include>:
   ```

   ![バックアップのインストール](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup5.png)

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復 - 手順](AD-Forest-Recovery-Procedures.md)
