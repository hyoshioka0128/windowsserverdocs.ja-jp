---
title: ブート可能な USB フラッシュ ドライブの作成
description: Windows Server Essentials の使用方法について説明します。
ms.date: 05/04/2018
ms.topic: article
ms.assetid: 2fe8e35c-69f9-40b3-a270-22e2402510d8
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: a4a92a3ec4641b314213afe9b53d8dc033f41037
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87181428"
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

2.  管理者としてコマンド プロンプト ウィンドウを開きます。

3.  「`diskpart`.

4.  開いた新しいコマンド ライン ウィンドウで、USB フラッシュ ドライブ番号またはドライブ文字を確認するために、コマンド プロンプトに「 `list disk`」と入力して Enter キーを押します。 `list disk` コマンドは、コンピューター上のすべてのディスクを表示します。 USB フラッシュ ドライブのドライブ番号またはドライブ文字をメモしておきます。

5.  コマンド プロンプトで「 `select disk <X>`」(X は USB フラッシュ ドライブのドライブ番号またはドライブ文字) と入力し、Enter キーを押します。

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

 [Windows Server ESSENTIALS ADK を使用したはじめに](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)[イメージの作成とカスタマイズ追加の](Creating-and-Customizing-the-Image.md)[カスタマイズカスタマイズ](Additional-Customizations.md)[のイメージの準備カスタマーエクスペリエンスをテストするためのイメージの準備](Preparing-the-Image-for-Deployment.md) [Testing the Customer Experience](Testing-the-Customer-Experience.md)

 [このガイドの利用方法](https://windows.microsoft.com/windows/support)
