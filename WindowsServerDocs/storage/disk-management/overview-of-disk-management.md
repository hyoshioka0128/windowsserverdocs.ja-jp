---
title: ディスクの管理の概要
description: ディスクの管理は、新しいドライブの初期化、ボリュームの拡張、パーティションの圧縮、およびドライブ文字の変更などの記憶域に関する高度なタスクを実行できる Windows のシステム ユーティリティです。
ms.date: 06/07/2019
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 333b8f5676fbb83a16a8e56249701135eabd7d4a
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87935947"
---
# <a name="overview-of-disk-management"></a>ディスクの管理の概要

> **適用対象:** Windows 10、Windows 8.1、Windows 7、Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ディスクの管理は、記憶域に関する高度なタスクを実行できる Windows のシステム ユーティリティです。 ディスクの管理で行えることを以下にいくつか示します。

- 新しいドライブをセットアップするには、[新しいドライブの初期化](initialize-new-disks.md)に関するページを参照してください。
- 同じドライブ上のボリュームの一部になっていない領域にボリュームを拡張するには、「[ベーシック ボリュームを拡張する](extend-a-basic-volume.md)」を参照してください。
- パーティションを圧縮するには (通常は隣接するパーティションを拡張できるようにするために行います)、「[ベーシック ボリュームを圧縮する](shrink-a-basic-volume.md)」を参照してください。
- ドライブ文字を変更したり、新しいドライブ文字を割り当てたりするには、「[ドライブ文字を変更する](change-a-drive-letter.md)」を参照してください。

![3 つのパーティションがある一般的なドライブを表示するディスクの管理 - 499 MB のシステム パーティション、Windows 用のサイズの大きい C ドライブ、およびもう 1 つの 499 MB のリカバリ用パーティション](media/disk-management.png)

> [!TIP]
>  次の手順の実行時にエラーが発生したり、うまくいかない場合は、「[ディスクの管理のトラブルシューティング](troubleshooting-disk-management.md)」のトピックを参照してください。 解決しなくても、慌てる必要はありません。 [Microsoft コミュニティ](https://answers.microsoft.com/en-us/windows) サイトに大量の情報があります。[[ファイル、フォルダー、オンライン ストレージ]](https://answers.microsoft.com/en-us/windows/forum/windows_10-files?sort=lastreplydate&dir=desc&tab=All&status=all&mod=&modAge=&advFil=&postedAfter=&postedBefore=&threadType=all&isFilterExpanded=true&tm=1514405359639) セクションを検索してみてください。それでもヘルプが必要な場合は、そこで質問を投稿してください。Microsoft またはコミュニティのその他のメンバーがヘルプを試みます。 これらのトピックを改善する方法についてフィードバックがございましたら、ぜひお知らせください。 *[このページはお役に立ちましたか?]* のプロンプトに答えて、そちらか、このトピックの下部にあるパブリック コメントのスレッドにコメントを残してください。

実行する必要があるが Windows の別のツールを使用するいくつかの共通タスクを以下に示します。

- ディスク領域を解放するには、「[Windows 10 のドライブの空き領域を増やす](https://support.microsoft.com/help/12425/windows-10-free-up-drive-space)」を参照してください。
- ドライブを最適化するには、「[Windows 10 PC を最適化する](https://support.microsoft.com/help/4026701/windows-defragment-your-windows-10-pc)」を参照してください。
- 複数のハード ドライブをまとめて RAID のように 1 つにプールするには、[記憶域スペース](https://support.microsoft.com/help/12438/windows-10-storage-spaces)に関するページを参照してください。

## <a name="about-those-extra-recovery-partitions"></a>余分な回復パーティションについて

興味のある方のための説明となりますが (お客様からのご意見に記載されていました)、Windows には通常、メイン ドライブ (通常は C:\ ドライブ) に以下の 3 つのパーティションが含まれています。

![3 つのパーティションを示すディスク 0 - EFI システム パーティション、Windows パーティション、および回復パーティション](media/windows-partitions.png)

- **EFI システム パーティション** - これは最新の PC が PC およびオペレーティング システムを起動 (ブート) するために使用されます。
- **Windows オペレーティング システム ドライブ (C:)** -これは Windows がインストールされる場所で、通常は残りのアプリとファイルを配置します。
- **回復パーティション** - これは Windows の起動に問題が発生したり、その他の重大な問題が発生した場合に Windows の回復に役立つ特別なツールを格納する場所です。

ディスクの管理では、EFI システム パーティションと回復パーティションが 100% 空き容量であると表示する場合がありますが、これは正しくありません。 これらのパーティションは一般的に、PC が正常に動作するために必要な非常に重要なファイルでほぼいっぱいになっています。 これらは PC を起動したり問題からの回復を支援したりするジョブを実行させるために、そのままにしておくことをお勧めします。

## <a name="additional-references"></a>その他の参照情報

- [ディスクを管理する](manage-disks.md)
- [ベーシック ボリュームを管理する](manage-basic-volumes.md)
- [ディスクの管理のトラブルシューティング](troubleshooting-disk-management.md)
- [Windows 10 の回復オプション](https://support.microsoft.com/help/12415/windows-10-recovery-options)
- [Windows 10 へのアップグレード後に失われたファイルを検索する方法](https://support.microsoft.com/help/12386/windows-10-find-lost-files-after-update)
- [ファイルをバックアップまたは復元する](https://support.microsoft.com/help/17143/windows-10-back-up-your-files)
- [回復ドライブを作成する](https://support.microsoft.com/help/4026852/windows-create-a-recovery-drive)
- [システムの復元ポイントを作成する](https://support.microsoft.com/help/4027538/windows-create-a-system-restore-point)
- [BitLocker 回復キーを探す](https://support.microsoft.com/help/4026181/windows-find-my-bitlocker-recovery-key)
