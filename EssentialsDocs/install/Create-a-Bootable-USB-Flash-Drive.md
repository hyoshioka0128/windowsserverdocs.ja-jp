---
title: ブート可能な USB フラッシュ ドライブの作成
description: Windows Server Essentials の使用方法について説明します。
ms.date: 05/04/2018
ms.prod: windows-server
ms.topic: article
ms.assetid: 2fe8e35c-69f9-40b3-a270-22e2402510d8
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: ddcdb9576072af6b7014f6dc9b0c38e9f5bdd25d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80818365"
---
# <a name="create-a-bootable-usb-flash-drive"></a>ブート可能な USB フラッシュ ドライブの作成

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

ブート可能な USB フラッシュドライブを作成して、Windows Server Essentials の展開に使用することができます。 最初の手順は、コマンド ライン ユーティリティである DiskPart を使用して USB フラッシュ ドライブを準備することです。 DiskPart の詳細については、「 [DiskPart のコマンド ライン オプション](https://go.microsoft.com/fwlink/?LinkId=207073)」を参照してください。  


> [!TIP]
> サーバーではなく PC での Windows の回復または再インストールに使用する起動可能な USB フラッシュドライブを作成するには、「[回復ドライブを作成](https://support.microsoft.com/help/4026852/windows-create-a-recovery-drive)する」を参照してください。
  
 ブート可能な USB フラッシュ ドライブを作成または使用する可能性のあるその他のシナリオについては、次のトピックを参照してください。  
  
-   [既存のクライアント コンピューターのバックアップからシステム全体を復元する](../manage/restore-a-full-system-from-an-existing-client-computer-backup.md)  
  
-   [Windows Server Essentials を実行しているサーバーの復元または修復](../manage/restore-or-repair-your-server-running-windows-server-essentials.md)  

  
### <a name="to-create-a-bootable-usb-flash-drive"></a>起動可能な USB フラッシュ ドライブを作成するには  
  
1.  USB フラッシュ ドライブを実行中のコンピューターに挿入します。  
  
2.  [コマンド プロンプト] ウィンドウを管理者として開きます。  
  
3.  「`diskpart`」と入力します。  
  
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
  
## <a name="see-also"></a>参照  

 [Windows Server ESSENTIALS ADK でのはじめに](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [イメージ  の作成とカスタマイズ](Creating-and-Customizing-the-Image.md)  
 [追加のカスタマイズ](Additional-Customizations.md)   
 [展開  のイメージの準備](Preparing-the-Image-for-Deployment.md)  
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)   

 [Windows Server ESSENTIALS ADK でのはじめに](../install/Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [イメージ  の作成とカスタマイズ](../install/Creating-and-Customizing-the-Image.md)  
 [追加のカスタマイズ](../install/Additional-Customizations.md)   
 [展開  のイメージの準備](../install/Preparing-the-Image-for-Deployment.md)  
 [カスタマー エクスペリエンスのテスト](../install/Testing-the-Customer-Experience.md)   

 [お役に立ちますか?](https://windows.microsoft.com/windows/support)
