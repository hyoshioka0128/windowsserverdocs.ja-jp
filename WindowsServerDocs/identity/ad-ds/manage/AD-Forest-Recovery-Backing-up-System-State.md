---
title: AD フォレストの回復-完全なサーバーのバックアップ
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 9238cb27-0020-42f7-90d6-fcebf7e3c0bc
ms.technology: identity-adds
ms.openlocfilehash: 321f927a3efc4f2391daff92ac4c8b7acb47c055
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80824285"
---
# <a name="ad-forest-recovery---backing-up-the-system-state-data"></a>AD フォレストの回復-システム状態データのバックアップ  

>適用対象: Windows Server 2016、Windows Server 2012、および 2012 R2、Windows Server 2008 および 2008 R2

Windows Server バックアップまたは wbadmin を使用して DC 上でシステム状態のバックアップを実行するには、次の手順に従います。  

## <a name="to-perform-a-system-state-backup-using-windows-server-backup"></a>Windows Server バックアップを使用してシステム状態のバックアップを実行するには

1. **サーバーマネージャー**を開き、 **[ツール]** をクリックし、 **[Windows Server バックアップ]** をクリックします。
   - Windows Server 2008 R2 および Windows Server 2008 で、 **[スタート]** をクリックし、 **[管理ツール]** をポイントして、 **[Windows Server バックアップ]** をクリックします。 

   ![バックアップのインストール](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup1.png)

2. メッセージが表示されたら、 **[ユーザーアカウント制御]** ダイアログボックスで、バックアップオペレーターの資格情報を入力し、[ **OK]** をクリックします。
3. **[ローカルバックアップ]** をクリックします。
4. **[操作]** メニューの **[バックアップ (1 回限り)]** をクリックします。
5. バックアップ (1 回限り) ウィザードの **[バックアップオプション]** ページで、 **[別のオプション]** をクリックし、 **[次へ]** をクリックします。

   ![バックアップのインストール](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup3.png)

6. **[バックアップ構成の選択]** ページで、 **[カスタム]** をクリックし、 **[次へ]** をクリックします。
7. **[バックアップする項目の選択]** 画面で、 **[項目の追加]** をクリックし、 **[システム状態]** を選択して [ **Ok]** をクリックします。
   - Windows Server 2008 R2 および Windows Server 2008 で、バックアップに含めるボリュームを選択します。 [**システム回復を有効に**する] チェックボックスをオンにすると、すべての重要なボリュームが選択されます。 

   ![バックアップのインストール](media/AD-Forest-Recovery-Backing-up-System-State/systemstatebackup.png)  

8. **[インストール先の種類の指定]** ページで、 **[ローカルドライブ]** または **[リモート共有フォルダー]** をクリックし、 **[次へ]** をクリックします。  リモート共有フォルダーにバックアップする場合は、次の手順を実行します。  
   - 共有フォルダーへのパスを入力します。
   - **Access Control**で、**継承しない** または **継承** を選択してバックアップへのアクセスを決定し、**次へ** をクリックします。  
   - **[バックアップ用のユーザー資格情報の指定]** ダイアログボックスで、共有フォルダーへの書き込みアクセス権を持つユーザーのユーザー名とパスワードを入力し、[ **OK]** をクリックします。

9. Windows Server 2008 R2 および Windows Server 2008 の場合は、 **[詳細オプションの指定]** ページで、 **[VSS コピーバックアップ]** を選択し、 **[次へ]** をクリックします。
10. **[バックアップ先の選択]** ページで、バックアップの場所を選択します。  [ローカルドライブ] を選択した場合は、ローカルドライブを選択するか、[リモート共有] を選択した場合はネットワーク共有を選択します。
11. 確認 画面で、**バックアップ** をクリックします。
12. この処理が完了したら、 **[閉じる]** をクリックします。
13. Windows Server バックアップを閉じます。

## <a name="to-perform-a-system-state-backup-using-wbadminexe"></a>Wbadmin を使用してシステム状態のバックアップを実行するには

管理者特権のコマンドプロンプトを開き、次のコマンドを入力して、enter キーを押します。  
  
   ```
   wbadmin start systemstatebackup -backuptarget:<targetDrive>:
   ```

   ![バックアップのインストール](media/AD-Forest-Recovery-Backing-up-System-State/systemstatebackup2.png)  

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復 - 手順](AD-Forest-Recovery-Procedures.md)
