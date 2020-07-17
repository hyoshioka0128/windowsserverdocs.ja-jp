---
title: create partition logical
description: Create partition logical コマンドの参照記事。既存の拡張パーティションに論理パーティションを作成します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1f59b79a-d690-4d0e-ad38-40df5a0ce38e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4860f61d23c9ae51732c1fb0e127047c4944d2ed
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85929671"
---
# <a name="create-partition-logical"></a>create partition logical

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

既存の拡張パーティションに論理パーティションを作成します。 パーティションを作成すると、フォーカスは自動的に新しいパーティションに移動します。

>[!IMPORTANT]
> このコマンドは、マスターブートレコード (MBR) ディスクでのみ使用できます。 [[ディスクの選択](select-disk.md)] コマンドを使用して、ベーシック MBR ディスクを選択し、それにフォーカスを移動する必要があります。
>
> 論理ドライブを作成する前に、[拡張パーティション](create-partition-extended.md)を作成する必要があります。

## <a name="syntax"></a>構文

```
create partition logical [size=<n>] [offset=<n>] [align=<n>] [noerr]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| サイズ =`<n>` | 論理パーティションのサイズをメガバイト (MB) 単位で指定します。このサイズは拡張パーティションよりも小さくする必要があります。 サイズが指定されていない場合、パーティションは拡張パーティションの空き領域がなくなるまで続行されます。 |
| オフセット =`<n>` | パーティションが作成されるオフセットをキロバイト (KB) 単位で指定します。 オフセットは、使用されるシリンダーサイズを完全に埋めるために切り上げられます。 オフセットが指定されない場合、パーティションを保持するうえで十分な大きさを持つ最初のディスク拡張にパーティションが配置されます。 パーティションは、少なくとも、 **size = `<n>` **で指定された数と同じ長さのバイトになります。 論理パーティションのサイズを指定する場合は、拡張パーティションよりも小さくする必要があります。 |
| align =`<n>` | すべてのボリュームまたはパーティションエクステントを最も近いアラインメント境界に配置します。 通常、パフォーマンスを向上させるために、ハードウェア RAID 論理ユニット番号 (LUN) アレイと共に使用します。 `<n>`ディスクの先頭から最も近いアラインメント境界までのキロバイト (KB) 数を指定します。 |
| noerr | スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |

#### <a name="remarks"></a>注釈

- **Size**パラメーターと**offset**パラメーターが指定されていない場合、論理パーティションは拡張パーティションで使用可能な最大のディスクエクステントに作成されます。

## <a name="examples"></a>例

サイズが 1000 mb の論理パーティションを作成するには、選択したディスクの拡張パーティションで、次のように入力します。

```
create partition logical size=1000
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [create コマンド](create.md)

- [select disk](select-disk.md)
