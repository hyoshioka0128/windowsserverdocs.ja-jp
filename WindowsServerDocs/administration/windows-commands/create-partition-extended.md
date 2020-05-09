---
title: create partition extended
description: Create partition extended コマンドのリファレンストピック。フォーカスがあるディスクに拡張パーティションを作成します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4ad7cb66-9c66-4153-b94e-1030a7225070
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9d2cc591dca276f70b3ddda1827607d5e2953ed2
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2020
ms.locfileid: "82993281"
---
# <a name="create-partition-extended"></a>create partition extended

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

フォーカスがあるディスクに拡張パーティションを作成します。 パーティションを作成すると、フォーカスは自動的に新しいパーティションに移動します。

>[!IMPORTANT]
> このコマンドは、マスターブートレコード (MBR) ディスクでのみ使用できます。 [[ディスクの選択](select-disk.md)] コマンドを使用して、ベーシック MBR ディスクを選択し、それにフォーカスを移動する必要があります。
>
> 論理ドライブを作成する前に、拡張パーティションを作成する必要があります。 1 台のディスクには、1 つの拡張パーティションしか作成できません。 別の拡張パーティション内に拡張パーティションを作成しようとすると、このコマンドは失敗します。

## <a name="syntax"></a>構文

```
create partition extended [size=<n>] [offset=<n>] [align=<n>] [noerr]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| サイズ =`<n>` | パーティションのサイズ (MB 単位) を指定します。 サイズが指定されていない場合、パーティションは拡張パーティションの空き領域がなくなるまで続行されます。 |
| オフセット =`<n>` | パーティションが作成されるオフセットをキロバイト (KB) 単位で指定します。 オフセットが指定されていない場合、パーティションは、新しいパーティションを保持するのに十分な大きさのディスクの空き領域の先頭から開始されます。 |
| align =`<n>` | すべてのパーティションエクステントを最も近いアラインメント境界に配置します。 通常、パフォーマンスを向上させるために、ハードウェア RAID 論理ユニット番号 (LUN) アレイと共に使用します。 `<n>`ディスクの先頭から最も近いアラインメント境界までのキロバイト (KB) 数を指定します。 |
| noerr | スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |

## <a name="examples"></a>使用例

サイズが 1000 mb の拡張パーティションを作成するには、次のように入力します。

```
create partition extended size=1000
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [create コマンド](create.md)

- [select disk](select-disk.md)
