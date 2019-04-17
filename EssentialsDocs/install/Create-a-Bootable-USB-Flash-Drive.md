---
title: "起動可能な USB フラッシュ ドライブを作成します。"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2fe8e35c-69f9-40b3-a270-22e2402510d8
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 9d587329e1141040b2511e1574649f1844dcec90
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-bootable-usb-flash-drive"></a>起動可能な USB フラッシュ ドライブを作成します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

Windows Server Essentials の展開に使用する起動可能な USB フラッシュ ドライブを作成することができます。 最初の手順は、コマンド ライン ユーティリティである DiskPart を使用して、USB フラッシュ ドライブを準備するのには。 DiskPart の詳細については、次を参照してください。 [DiskPart コマンド ライン オプション](https://go.microsoft.com/fwlink/?LinkId=207073)します。  
  
 その他のシナリオを作成または起動可能な USB を使用することがありますについては、フラッシュ ドライブ、次のトピックを参照してください。  
  
-   [既存のクライアント コンピューター バックアップから完全なシステムを復元します。](https://technet.microsoft.com/library/jj713539.aspx#BKMK_CreateBootable)  
  
-   [Windows Server Essentials を実行しているサーバーは、復元または修復](https://technet.microsoft.com/library/jj593197.aspx#BKMK_Restore_2)  
  
### <a name="to-create-a-bootable-usb-flash-drive"></a>起動可能な USB フラッシュ ドライブを作成するには  
  
1.  実行中のコンピューターに USB フラッシュ ドライブを挿入します。  
  
2.  管理者としてコマンド プロンプト ウィンドウを開きます。  
  
3.  種類`diskpart`します。  
  
4.  開いた新しいコマンド ライン ウィンドウで確認する、USB フラッシュ ドライブ番号またはドライブ文字をコマンド プロンプトに「`list disk`し、[入力] をクリックします。 `list disk`コマンドは、コンピューター上のすべてのディスクを表示します。 ドライブ番号または USB フラッシュ ドライブのドライブ文字に注意してください。  
  
5.  コマンド プロンプトで、次のように入力します。 `select disk <X>`、ここで X はドライブ番号またはドライブ文字の USB フラッシュ ドライブ、とし、enter キーをクリックします。  
  
6.  種類`clean`、入力] をクリックします。 このコマンドは、USB フラッシュ ドライブからすべてのデータを削除します。  
  
7.  USB フラッシュ ドライブに新しいプライマリ パーティションを作成するに次のように入力します。 `create part pri`、し、[入力] をクリックします。  
  
8.  作成したパーティションを選択するには、次のように入力します。 `select part 1`、し、[入力] をクリックします。  
  
9. パーティションをフォーマットするには、次のように入力します。 `format fs=ntfs quick`、し、[入力] をクリックします。  
  
    > [!IMPORTANT]
    >  サーバー プラットフォームが Unified Extensible Firmware Interface (UEFI) をサポートする場合は、NTFS ではなく FAT32 として、USB フラッシュ ドライブをフォーマットする必要があります。 フォーマットするパーティションを FAT32 として、次のように入力します。 `format fs=fat32 quick`、し、[入力] をクリックします。  
  
10. 種類`active`、し、[入力] をクリックします。  
  
11. 種類`exit`、し、[入力] をクリックします。  
  
12. カスタム イメージの準備が完了したら、USB フラッシュ ドライブのルートに保存します。  
  
## <a name="see-also"></a>参照してください。  

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

 [どのかお困りですか。](https://windows.microsoft.com/windows/support)
