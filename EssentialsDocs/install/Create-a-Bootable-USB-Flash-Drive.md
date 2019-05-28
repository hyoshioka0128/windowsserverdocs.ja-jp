---
title: ブート可能な USB フラッシュ ドライブの作成
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 05/04/2018
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2fe8e35c-69f9-40b3-a270-22e2402510d8
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: cb62a460c09fdb2874bcc051176a05e88cee19e7
ms.sourcegitcommit: 7cb939320fa2613b7582163a19727d7b77debe4b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/14/2019
ms.locfileid: "65621282"
---
# <a name="create-a-bootable-usb-flash-drive"></a>ブート可能な USB フラッシュ ドライブの作成

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

起動可能な USB フラッシュ ドライブを使用して Windows Server Essentials の展開を作成することができます。 最初の手順は、コマンド ライン ユーティリティである DiskPart を使用して USB フラッシュ ドライブを準備することです。 DiskPart の詳細については、「 [DiskPart のコマンド ライン オプション](https://go.microsoft.com/fwlink/?LinkId=207073)」を参照してください。  


> [!TIP]
> 回復またはサーバーではなく、PC に Windows を再インストールで使用するため、起動可能な USB フラッシュ ドライブを作成するを参照してください。 [recovery ドライブを作成する](https://support.microsoft.com/help/4026852/windows-create-a-recovery-drive)します。
  
 ブート可能な USB フラッシュ ドライブを作成または使用する可能性のあるその他のシナリオについては、次のトピックを参照してください。  
  
-   [既存のクライアント コンピューターのバックアップからシステム全体を復元する](../manage/restore-a-full-system-from-an-existing-client-computer-backup.md)  
  
-   [Windows Server Essentials を実行しているサーバーの復元または修復](../manage/restore-or-repair-your-server-running-windows-server-essentials.md)  

  
### <a name="to-create-a-bootable-usb-flash-drive"></a>起動可能な USB フラッシュ ドライブを作成するには  
  
1.  USB フラッシュ ドライブを実行中のコンピューターに挿入します。  
  
2.  [コマンド プロンプト] ウィンドウを管理者として開きます。  
  
3.  「`diskpart`.  
  
4.  開いた新しいコマンド ライン ウィンドウで、USB フラッシュ ドライブ番号またはドライブ文字を確認するために、コマンド プロンプトに「`list disk`」と入力して Enter キーを押します。 `list disk` コマンドは、コンピューター上のすべてのディスクを表示します。 USB フラッシュ ドライブのドライブ番号またはドライブ文字をメモしておきます。  
  
5.  コマンド プロンプトで「`select disk <X>`」(X は USB フラッシュ ドライブのドライブ番号またはドライブ文字) と入力し、Enter キーを押します。  
  
6.  「 `clean`」と入力して、Enter キーを押します。 このコマンドは、USB フラッシュ ドライブからすべてのデータを削除します。  
  
7.  USB フラッシュ ドライブに新しいプライマリ パーティションを作成するには、「 `create partition primary`」と入力し、Enter キーを押します。  
  
8.  作成したパーティションを選択するには、「 `select partition 1`」と入力し、Enter キーを押します。  
  
9. パーティションをフォーマットするには、「 `format fs=ntfs quick`」と入力し、Enter キーを押します。  
  
    > [!IMPORTANT]
    >  サーバー プラットフォームが Unified Extensible Firmware Interface (UEFI) をサポートしている場合、USB フラッシュ ドライブを NTFS ではなく FAT32 としてフォーマットする必要があります。 パーティションを FAT32 としてフォーマットするには、「 `format fs=fat32 quick`」と入力し、Enter キーを押します。  
  
10. 「 `active`」と入力して、Enter キーを押します。  
  
11. 「 `exit`」と入力して、Enter キーを押します。  
  
12. カスタム イメージの準備が完了したら、それを USB フラッシュ ドライブのルートに保存します。  
  
## <a name="see-also"></a>関連項目  

 [Windows Server Essentials ADK の概要](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)   

 [Windows Server Essentials ADK の概要](../install/Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [作成して、イメージをカスタマイズします。](../install/Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](../install/Additional-Customizations.md)   
 [イメージの展開の準備](../install/Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](../install/Testing-the-Customer-Experience.md)   

 [どのようなサポートするでしょうか。](https://windows.microsoft.com/windows/support)
