---
title: ディスクの管理の概要
description: ディスクの管理は、新しいドライブの初期化、ボリュームの拡張、パーティションの圧縮、およびドライブ文字を変更するなどの高度なストレージ タスクを実行することができる Windows のシステム ユーティリティです。
ms.date: 06/07/2019
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: a3885ae6b09ad431fd1ea5e4c593e02c7bb274d9
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812550"
---
# <a name="overview-of-disk-management"></a>ディスクの管理の概要

> **適用対象します。** Windows 10、Windows 8.1、Windows 7、Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ディスクの管理は、高度なストレージ タスクを実行することができる Windows のシステム ユーティリティです。 ディスクの管理に適しています事項の一部を次に示します。

- 新しいドライブをセットアップするには、次を参照してください。[新しいドライブの初期化](initialize-new-disks.md)します。
- 既に同じドライブ上のボリュームの一部ではない領域にボリュームを拡張するを参照してください。[ベーシック ボリュームを拡張](extend-a-basic-volume.md)します。
- パーティションの圧縮は、通常、隣接するパーティションを拡張するように表示[ベーシック ボリュームを圧縮](shrink-a-basic-volume.md)します。
- ドライブ文字を変更したり、新しいドライブ文字を割り当て、次を参照してください。[ドライブ文字を変更する](change-a-drive-letter.md)します。

![ディスクの管理 - 499 MB のシステム パーティション、サイズの大きい C ドライブの Windows、および回復の 499 MB のもう 1 つのパーティションの 3 つのパーティションがある一般的なドライブの表示](media/disk-management.png)

> [!TIP]
>  エラーが発生する、またはこれらの手順で動作しないのは何かをかけて、[ディスク管理のトラブルシューティング](troubleshooting-disk-management.md)トピック。 解決しない場合に、慌てないでください。 大量の情報がある、[マイクロソフト コミュニティ](https://answers.microsoft.com/en-us/windows)サイト - 検索してみてください、[ファイル、フォルダー、および記憶域](https://answers.microsoft.com/en-us/windows/forum/windows_10-files?sort=lastreplydate&dir=desc&tab=All&status=all&mod=&modAge=&advFil=&postedAfter=&postedBefore=&threadType=all&isFilterExpanded=true&tm=1514405359639)セクション、およびヘルプ必要がある場合は、質問や Microsoft の他のメンバーに投稿しますコミュニティは、ヘルプを試みます。 これらのトピックを改善する方法についてのフィードバックをした場合をいただいております。 だけに回答する、*このページをお勧めしますか?* プロンプト、またはこのトピックの下部にあるパブリック コメント スレッドでコメントのままにします。

次のとおりいくつかの一般的なタスクを行いたい場合がありますが、Windows で他のツールを使用します。

- ディスク領域を解放する、次を参照してください。 [Windows 10 のドライブの領域を解放する](https://support.microsoft.com/help/12425/windows-10-free-up-drive-space)します。
- ドライブを最適化するには、次を参照してください。 [Windows 10 PC の断片化を解消](https://support.microsoft.com/help/4026701/windows-defragment-your-windows-10-pc)します。
- 複数のハード ドライブの実行をまとめて、RAID のようなプールは、次を参照してください。[記憶域スペース](https://support.microsoft.com/help/12438/windows-10-storage-spaces)します。

## <a name="about-those-extra-recovery-partitions"></a>これらの余分な回復パーティションについて

Windows に通常メイン ドライブ (通常は、C:\ の 3 つのパーティションが含まれます (コメントを読んだしました!) が興味を場合ドライブ):

![0 が表示された 3 つのパーティションの EFI システム パーティション、Windows パーティション、および復旧パーティションをディスクします。](media/windows-partitions.png)

- **EFI システム パーティション**-これは、起動 (ブート) に最新の Pc で使用されます、PC と、オペレーティング システム。
- **Windows オペレーティング システム ドライブ (c:)** -これは、Windows がインストールされていると、通常は、アプリとファイルの残りの部分を配置します。
- **復旧パーティション**-これは問題が以降であるかその他の重大な問題が発生した場合に、Windows を回復するための特別なツールを格納する場所。

ディスクの管理は、EFI システム パーティションと復旧パーティションを 100% の空きとして表示可能性があります、楕円が。 これらのパーティションは一般的に、PC が正常に動作する必要がある非常に重要なファイルを非常に完全です。 お使いの PC を開始して、問題から回復するために、ジョブの実行を単独でそのままにすることをお勧めします。

## <a name="see-also"></a>関連項目

- [ディスクを管理する](manage-disks.md)
- [ベーシック ボリュームを管理する](manage-basic-volumes.md)
- [ディスクの管理のトラブルシューティング](troubleshooting-disk-management.md)
- [Windows 10 での回復オプション](https://support.microsoft.com/help/12415/windows-10-recovery-options)
- [Windows 10 への更新後の失われたファイルを検索します。](https://support.microsoft.com/help/12386/windows-10-find-lost-files-after-update)
- [バックアップおよびファイルを復元します。](https://support.microsoft.com/help/17143/windows-10-back-up-your-files)
- [回復のドライブを作成します。](https://support.microsoft.com/help/4026852/windows-create-a-recovery-drive)
- [システム復元ポイントを作成します。](https://support.microsoft.com/help/4027538/windows-create-a-system-restore-point)
- [BitLocker 回復キーを検索します。](https://support.microsoft.com/help/4026181/windows-find-my-bitlocker-recovery-key)
