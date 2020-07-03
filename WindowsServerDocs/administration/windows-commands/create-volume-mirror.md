---
title: create volume mirror
description: ボリュームミラーの作成コマンドの参照記事。指定された2つのダイナミックディスクを使用してボリュームミラーを作成します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 48776917-783a-47ff-8da4-1cab77cea34b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 91f718aab181db7d3cbeb0e4255a43f2924ecd33
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85929552"
---
# <a name="create-volume-mirror"></a>create volume mirror

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定された2つのダイナミックディスクを使用してボリュームミラーを作成します。 ボリュームが作成されると、フォーカスは自動的に新しいボリュームに移ります。

## <a name="syntax"></a>構文

```
create volume mirror [size=<n>] disk=<n>,<n>[,<n>,...] [align=<n>] [noerr]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| サイズ =`<n>` | ボリュームが各ディスクで占有するディスク領域の量を mb 単位で指定します。 サイズを指定しないと、新しいボリュームは最小のディスクで残りの空き領域を占有し、それ以外のディスクでそれと同じ容量の空き領域を占有します。 |
| disk = `<n>` 、 `<n>` [ `,<n>,...` ] | ミラーボリュームを作成するダイナミックディスクを指定します。 ミラーボリュームを作成するには、2つのダイナミックディスクが必要です。 **Size**パラメーターで指定したサイズと同じ容量の領域が、各ディスクに割り当てられます。 |
| align =`<n>` | すべてのボリュームエクステントを最も近い配置境界に配置します。 このパラメータは、通常、パフォーマンスを向上させるために、ハードウェア RAID 論理ユニット番号 (LUN) アレイと共に使用されます。 `<n>`ディスクの先頭から最も近いアラインメント境界までのキロバイト (KB) 数を指定します。 |
| noerr | スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターを指定しないと、エラーが発生して DiskPart が終了します。 |

## <a name="examples"></a>例

ディスク1と2で、サイズが 1000 mb のミラーボリュームを作成するには、次のように入力します。

```
create volume mirror size=1000 disk=1,2
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [create コマンド](create.md)
