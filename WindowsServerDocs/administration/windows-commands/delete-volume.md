---
title: delete volume
description: ボリュームの削除コマンドのリファレンストピックでは、選択したボリュームを削除します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f625933d-0f47-409e-93b2-a3e234049a5d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 59856e89ff96d2881040365d157540dc62c1aeb0
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2020
ms.locfileid: "82993097"
---
# <a name="delete-volume"></a>delete volume

選択されたボリュームを削除します。 開始する前に、この操作を成功させるボリュームを選択する必要があります。 使用して、 [ボリュームを選択して](select-volume.md) コマンドのボリュームを選択し、それにフォーカスをします。

> [!IMPORTANT]
> システムボリューム、ブートボリューム、またはアクティブなページングファイルまたはクラッシュダンプ (メモリダンプ) を含むボリュームを削除することはできません。

## <a name="syntax"></a>構文

```
delete volume [noerr]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| noerr | スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |

## <a name="examples"></a>使用例

フォーカスがあるボリュームを削除するには、次のように入力します。

```
delete volume
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [select volume](select-volume.md)

- [delete コマンド](delete.md)