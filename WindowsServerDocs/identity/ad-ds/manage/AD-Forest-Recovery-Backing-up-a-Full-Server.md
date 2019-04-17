---
title: "AD フォレストの回復 - フル サーバーのバックアップ"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 398918dc-c8ab-41a6-a377-95681ec0b543
ms.technology: identity-adfs
ms.openlocfilehash: b1af97c2eb23d65c2d106906bc0f5bb1f10b23ec
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="ad-forest-recovery---backing-up-a-full-server"></a>AD フォレストの回復 - フル サーバーのバックアップ  

>Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 の R2 を適用対象:

サーバーの完全バックアップは、さまざまなハードウェアまたは別のオペレーティング システムのインスタンスに復元できるため、フォレストの回復の準備をお勧めします。  Windows Server バックアップを使用して、サーバーの完全バックアップを実行することができます。 

## <a name="windows-server-backup"></a>Windows Server バックアップ
Windows Server バックアップは、既定ではインストールされません。 Windows Server 2016 および Windows Server 2012 R2 では、次の手順に従ってインストールします。

>[!NOTE]
>手順は、Windows Server 2016 および Windows Server 2012 R2 の間で若干異なる場合がありますに注意してください。

Windows Server 2008 および Windows Server 2008 R2 にインストールする手順については、次を参照してください。[をインストールする Windows Server バックアップ](https://technet.microsoft.com/library/cc771232.aspx)します。  

### <a name="to-install-windows-server-backup"></a>Windows Server バックアップをインストールするには
1. 開いている**サーバー マネージャー** ] をクリック**役割と機能の追加**します。
2. **追加の役割と機能のウィザード**] をクリックして**次**します。
3. **インストールの種類**画面で、既定値をそのまま使用**役割ベースまたは機能ベースのインストール**] をクリック**次**します。
4. **サーバーの選択**画面で、[**次**します。
5. **サーバーの役割**画面をクリックして**次**します。
6. **機能**画面で、 **Windows Server バックアップ**] をクリック**次**
! [バックアップをインストールします。](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup2.png)
7. をクリックして**インストール**します。
8. インストールが完了したら、クリックして**閉じる**します。


### <a name="to-perform-a-backup-with-windows-server-backup"></a>Windows Server バックアップのバックアップを実行するには

1. 開いている**サーバー マネージャー**、] をクリックして**ツール**、] をクリックし、 **Windows Server バックアップ**します。
    - Windows Server 2008 R2 および Windows Server 2008 では、をクリックして**開始**、] をポイント**管理ツール**、] をクリックし、 **Windows Server バックアップ**します。 
![バックアップをインストールします。](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup1.png) 
2. 求められた場合で、**ユーザー アカウント制御**ダイアログ ボックスで、バックアップ オペレーターの資格情報を提供し、をクリックして**OK**します。
3. をクリックして**ローカル バックアップ**します。
4. **アクション**] メニューのをクリックして**1 回バックアップ**します。
5. バックアップ 1 回ウィザードで、上、**バックアップ オプション**] ページで [**さまざまなオプション**、] をクリックし、 **[次へ]**します。
![バックアップをインストールします。](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup3.png)
6. **バックアップ構成の選択**] ページで [**サーバー全体 (推奨)**、] をクリックし、 **[次へ]**します。
7. **移行先の種類を指定**] ページで [**ローカル ドライブ**または**リモート共有フォルダー**、] をクリックし、 **[次へ]**します。
8. **バックアップ先の選択**ページで、バックアップの場所を選択します。  ローカルで選択した場合、ドライブは、ローカル ドライブを選択またはリモートで選択した場合、共有はネットワーク共有を選択します。
9. 確認画面で、をクリックして**バックアップ**します。
![バックアップをインストールします。](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup4.png)
10. この手順が完了したら、クリックして**閉じる**します。
11. Windows Server バックアップを閉じます。

>[!NOTE]
>バックアップ記憶域の場所が利用可能なないことを示すエラーが表示される場合が選択されているボリュームのいずれかを除外するか、新しいボリュームまたはリモート共有を追加する必要があります。
>選択したボリュームがバックアップする項目の一覧にも含まれていることを示す警告が表示される場合を削除し] をクリックするかどうかを決定**Ok**します。

## <a name="using-wbadminexe-to-backup-a-windows-server"></a>Wbadmin.exe を使用して、windows サーバーをバックアップするには
Wbadmin.exe では、コマンド ライン ユーティリティをバックアップおよびコマンド プロンプトから、オペレーティング システム、ボリューム、ファイル、フォルダー、およびアプリケーションを復元することができます。

#### <a name="to-perform-a-full-server-backup-using-wbadminexe"></a>Wbadmin.exe を使用してサーバーの完全バックアップを実行するには  
  
1.  管理者特権でコマンド プロンプトを開き、次のコマンドを入力し、ENTER キーを押します。  

        wbadmin start backup -backuptarget:<Drive_letter_to store_backup>: -include:<Drive_letter_to_include>:

![バックアップをインストールします。](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup5.png)
## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)
