---
title: create volume simple
description: Create volume simple コマンドの参照記事。指定されたダイナミックディスクにシンプルボリュームを作成します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: da0f208d-7fda-471a-9db2-5de5ba5207c6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1e7924ca4394a64fd5a8d92577a3f3f62b917461
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85929510"
---
# <a name="create-volume-simple"></a>create volume simple

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定されたダイナミックディスクにシンプルボリュームを作成します。 ボリュームを作成すると、フォーカスは自動的に新しいボリュームに移動します。

## <a name="syntax"></a>構文

```
create volume simple [size=<n>] [disk=<n>] [align=<n>] [noerr]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| サイズ =`<n>`  | ボリュームのサイズ (MB 単位) です。 サイズを指定しないと、新しいボリュームはディスク上の残りの空き領域を占有します。 |
| ディスク =`<n>`  | ボリュームが作成されるダイナミックディスク。 ディスクが指定されていない場合は、現在のディスクが使用されます。 |
| align =`<n>` | すべてのボリュームエクステントを最も近い配置境界に配置します。 通常、パフォーマンスを向上させるために、ハードウェア RAID 論理ユニット番号 (LUN) アレイと共に使用します。 `<n>`ディスクの先頭から最も近いアラインメント境界までのキロバイト (KB) 数を指定します。 |
| noerr | スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |

## <a name="examples"></a>例

サイズが 1000 mb のボリュームを作成するには、ディスク1で次のように入力します。

```
create volume simple size=1000 disk=1
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [create コマンド](create.md)
