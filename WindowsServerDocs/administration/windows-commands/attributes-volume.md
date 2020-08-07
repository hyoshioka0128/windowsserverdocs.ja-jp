---
title: attributes volume
description: 属性 volume コマンドのリファレンス記事。ボリュームの属性を表示、設定、またはクリアします。
ms.topic: article
ms.assetid: e40e8284-3d57-4de8-a46c-e4ade34a0d53
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a4e0e7110bd23d1a8127e867dd991d1dc620c164
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87895488"
---
# <a name="attributes-volume"></a>attributes volume

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ボリュームの属性を表示、設定、またはクリアします。

## <a name="syntax"></a>構文

```
attributes volume [{set | clear}] [{hidden | readonly | nodefaultdriveletter | shadowcopy}] [noerr]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ------- | -------- |
| set | フォーカスがあるボリュームの指定された属性を設定します。 |
| オフ | フォーカスがあるボリュームの指定された属性をクリアします。 |
| readonly | ボリュームを読み取り専用に指定します。 |
| hidden | ボリュームを非表示に指定します。 |
| nodefaultdriveletter | ボリュームに既定のドライブ文字を割り当てないように指定します。 |
| shadowcopy | ボリュームをシャドウ コピー ボリュームに指定します。 |
| noerr | スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |

### <a name="remarks"></a>Remarks

- ベーシックマスタブートレコード (MBR) ディスクでは、 **hidden**、 **readonly**、および**nodefaultdriveletter**各パラメータがディスク上のすべてのボリュームに適用されます。

- 基本的な GUID パーティションテーブル (GPT) ディスク、およびダイナミック MBR および GPT ディスクでは、 **hidden**、 **readonly**、および**nodefaultdriveletter**各パラメーターは、選択したボリュームにのみ適用されます。

- **属性 volume**コマンドを正常に実行するには、ボリュームを選択する必要があります。 使用して、 **ボリュームを選択して** コマンドのボリュームを選択し、それにフォーカスをします。

## <a name="examples"></a>例

選択したボリュームの現在の属性を表示するには、次のように入力します。

```
attributes volume
```

選択したボリュームを非表示または読み取り専用として設定するには、次のように入力します。

```
attributes volume set hidden readonly
```

選択したボリュームの非表示属性と読み取り専用属性を削除するには、次のように入力します。

```
attributes volume clear hidden readonly
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [ボリュームの選択コマンド](select-volume.md)
