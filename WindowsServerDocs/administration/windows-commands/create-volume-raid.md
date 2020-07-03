---
title: create volume raid
description: ボリューム raid の作成コマンドの参照記事。3つ以上の指定されたダイナミックディスクを使用して RAID-5 ボリュームを作成します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9f257950-9240-4d5f-9537-8ad653d48ebf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0c3b142e7fd678af04d1bc4e109ac399807da06e
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85929542"
---
# <a name="create-volume-raid"></a>create volume raid

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定された3つ以上のダイナミックディスクを使用して RAID-5 ボリュームを作成します。 ボリュームを作成すると、フォーカスは自動的に新しいボリュームに移動します。

## <a name="syntax"></a>構文

```
create volume raid [size=<n>] disk=<n>,<n>,<n>[,<n>,...] [align=<n>] [noerr]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| サイズ =`<n>` | ボリュームが各ディスクで占有するディスク領域の容量 (MB 単位) です。 サイズが指定されていない場合は、可能な限り最大の RAID-5 ボリュームが作成されます。 利用できる連続した空き領域が最も小さいディスクが RAID-5 ボリュームのサイズを決定し、同じ容量の領域が各ディスクから割り当てられます。 RAID-5 ボリュームで使用できるディスク領域の実際の容量は、ディスク領域の合計容量よりも小さくなります。これは、ディスク領域の一部がパリティとして使われるためです。 |
| ディスク =`<n>,<n>,<n>[,<n>,...]` | RAID-5 ボリュームを作成するダイナミックディスク。 RAID-5 ボリュームを作成するには、3 台以上のダイナミック ディスクが必要です。 と同じサイズの領域 `size=<n>` が各ディスクに割り当てられます。 |
| align =`<n>` | すべてのボリュームエクステントを最も近い配置境界に配置します。 通常、パフォーマンスを向上させるために、ハードウェア RAID 論理ユニット番号 (LUN) アレイと共に使用します。 `<n>`ディスクの先頭から最も近いアラインメント境界までのキロバイト (KB) 数を指定します。 |
| noerr | スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |

## <a name="examples"></a>例

ディスク1、2、3を使用して、サイズが 1000 mb の RAID-5 ボリュームを作成するには、次のように入力します。

```
create volume raid size=1000 disk=1,2,3
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [create コマンド](create.md)
