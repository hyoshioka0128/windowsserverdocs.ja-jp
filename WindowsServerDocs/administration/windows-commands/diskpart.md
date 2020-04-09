---
title: DiskPart
description: DiskPart の Windows コマンドに関するトピック。コンピューターのドライブを管理するのに役立ちます。
ms.prod: windows-server
ms.technology: storage
author: jasongerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 45fe66e4843b96db8e4593c0e963e4a80dbd22c2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80845475"
---
# <a name="diskpart"></a>DiskPart

>適用対象: Windows 10、Windows 8.1、Windows 8、Windows 7、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、windows server 2008 R2、Windows Server 2008

DiskPart コマンドを使用すると、コンピューターのドライブ (ディスク、パーティション、ボリューム、または仮想ハードディスク) を管理できます。 

DiskPart コマンドを使用するには、まず、オブジェクトを一覧表示してから、フォーカスを与えるオブジェクトを選択する必要があります。 オブジェクトにフォーカスがある場合、入力した DiskPart コマンドはそのオブジェクトに対して動作します。

## <a name="list-the-available-objects"></a>使用可能なオブジェクトを一覧表示する

次のように使用して、使用可能なオブジェクトの一覧を表示し、オブジェクトの番号またはドライブ文字を特定することができます。

- `list disk`-コンピューター上のすべてのディスクを表示します。

- `list volume`-コンピューター上のすべてのボリュームを表示します。

- `list partition`-コンピューターにフォーカスがあるディスク上のパーティションを表示します。

- `list vdisk`-コンピューター上のすべての仮想ディスクを表示します。

**List**コマンドを使用すると、フォーカスがあるオブジェクトの横にアスタリスク (\*) が表示されます。

## <a name="determine-focus"></a>フォーカスの決定

オブジェクトを選択すると、別のオブジェクトを選択するまで、フォーカスはそのオブジェクトに残ります。 たとえば、フォーカスがディスク0に設定されていて、ディスク2で [ボリューム 8] を選択した場合、フォーカスはディスク0からディスク2のボリューム8に移ります。

一部のコマンドでは、フォーカスが自動的に変更されます。 たとえば、新しいパーティションを作成すると、フォーカスは自動的に新しいパーティションに切り替わります。

選択したディスクのパーティションにのみフォーカスを移すことができます。 パーティションにフォーカスがあるとき、関連するボリュームがある場合には、そのボリュームにもフォーカスがあります。 ボリュームにフォーカスがあるとき、そのボリュームが単一の特定パーティションに割り当てられている場合は、関連するディスクとパーティションにもフォーカスがあります。 そうでない場合は、ディスクとパーティションにフォーカスが失われます。

## <a name="diskpart-commands"></a>DiskPart コマンド

DiskPart コマンドインタープリターを起動するには、コマンドプロンプトで次のように入力します。

```
diskpart
```

> [!IMPORTANT]
> DiskPart を実行するには、ローカルの**Administrators**グループ、または同様のアクセス許可を持つグループに存在する必要があります。 

Diskpart コマンドインタープリターでは、次のコマンドを実行できます。

| コマンド | 説明 |
| ------- | ----------- |
| [Active](active.md) | フォーカスがあるディスクのパーティションをアクティブとしてマークします。 |
| [[追加]](add.md) | フォーカスのあるシンプル ボリュームを、指定されたディスクにミラー化します。 |
| [割り当てる](assign.md) | フォーカスがあるボリュームに、ドライブ文字またはマウント ポイントを割り当てます。 |
| [Vdisk のアタッチ](attach-vdisk.md) | 仮想ハードディスク (VHD) を接続します。これにより、ホストコンピューターにローカルハードディスクドライブとして表示されます。 |
| [アトリビュート](attributes.md) | ディスクまたはボリュームの属性を表示、設定、またはクリアします。 |
| [オートマ](automount.md) | 自動マウント機能を有効または無効にします。 | 
| [改](break.md) | フォーカスのあるミラー ボリュームを 2 つのシンプル ボリュームに分割します。 |
| [中身](clean.md) | フォーカスがあるディスクから、パーティション フォーマットまたはボリューム フォーマットをすべて削除します。 |
| [Compact vdisk](compact-vdisk.md) | 容量可変の拡張バーチャルハードディスク (VHD) ファイルの物理サイズを小さくします。 |
| [Convert.exe](convert.md) | ファイルアロケーションテーブル (FAT) および FAT32 ボリュームを NTFS ファイルシステムに変換し、既存のファイルとディレクトリをそのまま残します。 |
| [生成](create.md) | ディスク上のパーティション、1つまたは複数のディスク上のボリューム、または仮想ハードディスク (VHD) を作成します。 |
| [削除](delete.md) | パーティションまたはボリュームを削除します。 |
| [Vdisk のデタッチ](detach-vdisk.md) | 選択した仮想ハードディスク (VHD) がホストコンピューター上のローカルハードディスクドライブとして表示されなくなります。 |
| [データ](detail.md) | 選択したディスク、パーティション、ボリューム、または仮想ハードディスク (VHD) に関する情報を表示します。 |
| [終了](exit.md) | DiskPart コマンド インタープリターを終了します。 |
| [Vdisk を展開する](expand-vdisk.md) | 
| [Extend](extend.md) | 
| [ファイルシステム](filesystems.md) | 
| [Format](format.md) | 
| [GPT](gpt.md) | 
| [ヘルプ](help.md) | 
| [[インポート](import.md)] | 
| [稼動](inactive.md) | 
| [表](list.md) | 
| [マージ vdisk](merge-vdisk.md) | 
| [なっ](offline.md) | 
| [オンライン](online.md) | 
| [回復](recover.md) | 
| [Rem](rem.md) | 
| [[削除]](remove.md) | 
| [回復](repair.md) | 
| [再スキャン](rescan.md) | 
| [日数](retain.md) | 
| [San](san.md) | 
| [選択](select.md) | 
| [Id の設定](set-id.md) | 
| [伸縮](shrink.md) | 
| [Uniqueid](uniqueid.md) | 

## <a name="additional-references"></a>その他の参照情報

- [コマンドライン構文のキー](command-line-syntax-key.md

- [ディスクの管理の概要](https://docs.microsoft.com/windows-server/storage/disk-management/overview-of-disk-management)

- [Windows PowerShell の記憶域コマンドレット](https://docs.microsoft.com/powershell/module/storage/)
