---
title: create volume stripe
description: ボリュームストライプの作成コマンドの参照記事。2つ以上の指定されたダイナミックディスクを使用してストライプボリュームを作成します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 20dce735-5f7c-4f83-a580-d087e2913a00
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8cb20a7741d49201b88345374ba1c435e81a77f6
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85929525"
---
# <a name="create-volume-stripe"></a>create volume stripe

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

2つ以上の指定されたダイナミックディスクを使用してストライプボリュームを作成します。 ボリュームを作成すると、フォーカスは自動的に新しいボリュームに移動します。

## <a name="syntax"></a>構文

```
create volume stripe [size=<n>] disk=<n>,<n>[,<n>,...] [align=<n>] [noerr]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- |  -----------|
| サイズ =`<n>` | ボリュームが各ディスクで占有するディスク領域の容量 (MB 単位) です。 サイズを指定しないと、新しいボリュームは最小のディスクで残りの空き領域を占有し、それ以外のディスクでそれと同じ容量の空き領域を占有します。 |
| ディスク =`<n>,<n>[,<n>,...]` | ストライプボリュームを作成するダイナミックディスク。 ストライプ ボリュームを作成するには、少なくとも 2 台のダイナミック ディスクが必要です。 と同じサイズの領域 `size=<n>` が各ディスクに割り当てられます。 |
| align =`<n>` | すべてのボリュームエクステントを最も近い配置境界に配置します。 通常、パフォーマンスを向上させるために、ハードウェア RAID 論理ユニット番号 (LUN) アレイと共に使用します。 `<n>`ディスクの先頭から最も近いアラインメント境界までのキロバイト (KB) 数を指定します。 |
| noerr | スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |

## <a name="examples"></a>例

ディスク1と2で、サイズが 1000 mb のストライプボリュームを作成するには、次のように入力します。

```
create volume stripe size=1000 disk=1,2
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [create コマンド](create.md)
