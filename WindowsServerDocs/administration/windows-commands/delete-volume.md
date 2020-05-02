---
title: delete volume
description: ボリュームの削除に関するリファレンストピックでは、選択したボリュームを削除します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f625933d-0f47-409e-93b2-a3e234049a5d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b9a8ae0fc863cec5c1a3f6debccf8201e96badd0
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82716688"
---
# <a name="delete-volume"></a>delete volume

選択されたボリュームを削除します。

## <a name="syntax"></a>構文

```
delete volume [noerr]
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| --------- | ----------- |
| noerr | スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |

## <a name="remarks"></a>Remarks

-   システム ボリューム、ブート ボリューム、またはアクティブなページング ファイルやクラッシュ ダンプ (メモリ ダンプ) を含んでいるボリュームは削除できません。
-   この操作を成功させるのには、ボリュームを選択してください。 使用して、 **ボリュームを選択して** コマンドのボリュームを選択し、それにフォーカスをします。

## <a name="examples"></a>例

フォーカスがあるボリュームを削除するには、次のように入力します。
```
delete volume
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

