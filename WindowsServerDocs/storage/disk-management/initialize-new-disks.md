---
title: 新しいディスクの初期化
description: ディスク管理では、準備を使用して、新しいディスクを初期化する方法。 トラブルシューティングの問題へのリンクも表示されます。
ms.date: 10/24/2018
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 61c8eb2321ee2a282345aba01c6d04a128f0448c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819393"
---
# <a name="initialize-new-disks"></a>新しいディスクの初期化

> **適用対象します。** Windows 10、Windows 8.1、Windows 7、Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

お使いのコンピューターに新しいディスクを追加し、ファイル エクスプ ローラーに表示されないことの場合には必要[ドライブ文字を追加](change-a-drive-letter.md)、または使用する前に初期化します。 書式指定されていないドライブのみ初期化できます。 ディスクの初期化では、すべての機能を消去しをフォーマットし、上のファイルを保存している Windows で使用するために準備します。

> [!WARNING]
> ディスク上に関心のあるファイルを既に持っている場合に初期化しないでください。 - すべてのファイルが利用できなくなります。 代わりに、ディスクをトラブルシューティングする推奨のファイルを読み取ることができますを参照してください[ディスクの状態が初期化されていないか、ディスクが不足している完全](troubleshooting-disk-management.md#disk-not-initialized)します。

## <a name="to-initialize-new-disks"></a>新しいディスクを初期化するには

ディスクの管理を使用して新しいディスクを初期化する方法を次に示します。 PowerShell を使用する場合、使用、[ディスクの初期化](https://docs.microsoft.com/powershell/module/storage/initialize-disk)コマンドレット代わりにします。

1. 管理者のアクセス許可を持つディスクの管理を開きます。 <br>タスク バーの検索ボックスに、これには、次のように入力します**ディスクの管理**、を選択し、保持 (または右クリック)**ディスクの管理**を選択し、**管理者として実行** > 。**はい**します。 入力の場合は、管理者として開くにはできません、**コンピュータの管理**代わりに、順に移動**ストレージ** > **ディスクの管理**します。
1. ディスク管理で、クリックして、初期化するディスクを右クリックして**ディスクの初期化**(下図)。 として表示されている場合*オフライン*、まず右クリックし、選択**オンライン**します。<br>一部の USB ドライブを初期化するオプションはありませんは、これらだけ形式を取得し、[ドライブ文字](change-a-drive-letter.md)します。

    ![ディスクの管理と表示されるディスクの初期化のショートカット メニューを未フォーマットのディスクを表示](media\uninitialized-disk.PNG)
2. **ディスクの初期化**(表示) ダイアログ ボックスで、正しいディスクが選択されていることを確認し、クリックしてチェック**OK**を既定のパーティション スタイルを受け入れるようにします。 パーティション スタイル (GPT または MBR) 参照を変更する必要がある場合[パーティション スタイルより-GPT と MBR について](#about-partition-styles-GPT-and-MBR)します。<br>ディスクの状態を簡単に変更**初期化**とし、さらに、**オンライン**状態。 何らかの理由が失敗を初期化する場合は、次を参照してください。[ディスクの状態が初期化されていないか、ディスクが不足している完全](troubleshooting-disk-management.md#disk-not-initialized)します。

    ![GPT パーティション スタイルが選択されているディスクの初期化 ダイアログ ボックス](media\initialize-disk.PNG)

## <a name="about-partition-styles---gpt-and-mbr"></a>パーティションのスタイルの GPT と MBR について

ディスクは、パーティションと呼ばれる複数のチャンクに分割できます。 -各パーティションがある 1 の場合でも必要 - GPT または MBR パーティション スタイルです。 Windows では、パーティション スタイルを使用して、ディスク上のデータにアクセスする方法を理解します。

最近は、通常では、パーティション スタイルについて心配する必要はありません - Windows は自動的に適切なディスクの種類を使用している、一番下の行は興味深く、おそらくこれではありません。

ほとんどの Pc では、ハード ドライブと Ssd の GUID パーティション テーブル (GPT) ディスクの種類を使用します。 GPT はありより堅牢な 2 TB を超えるボリュームに対して実行できます。 以前のマスター ブート レコード (MBR) ディスクの種類は、32 ビット Pc、古い Pc、およびメモリ カードなどのリムーバブル ドライブで使用されます。

MBR または GPT ディスクを変換するには、最初に削除する必要がすべてのボリューム、ディスクから、ディスク上のすべてを消去します。 詳細については、次を参照してください。 [MBR ディスクを GPT ディスクに変換](change-an-mbr-disk-into-a-gpt-disk.md)、または[GPT ディスクを MBR ディスクに変換](change-a-gpt-disk-into-an-mbr-disk.md)します。