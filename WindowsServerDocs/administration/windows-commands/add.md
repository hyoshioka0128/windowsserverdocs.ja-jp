---
title: add
description: シャドウコピーするボリュームのセットにボリュームを追加するか、エイリアス環境にエイリアスを追加する [追加] コマンドの参照トピック。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 47efce7a-86d2-4872-ae31-baa108757afd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9b621a3061c4e3366085c5cc44f91f26dd33d4e3
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719007"
---
# <a name="add"></a>add

シャドウコピーするボリュームのセットにボリュームを追加するか、エイリアス環境に別名を追加します。 サブコマンドなしで使用する場合は、現在のボリュームとエイリアスの一覧を**追加**します。

> [!NOTE]
> エイリアスは、シャドウコピーが作成されるまでエイリアス環境に追加されません。 すぐに必要なエイリアスを追加するには、 **add alias**を使用します。

## <a name="syntax"></a>構文

```
add
add volume <volume> [provider <providerid>]
add alias <aliasname> <aliasvalue>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| ---------- | ----------- |
| ボリューム | シャドウコピーするボリュームのセットであるボリュームをシャドウコピーセットに追加します。 「構文とパラメーターの[ボリュームの追加](add-volume.md)」を参照してください。 |
| alias | 指定された名前と値をエイリアス環境に追加します。 「構文とパラメーターの[別名の追加](add-alias.md)」を参照してください。 |
| /? | コマンドラインでヘルプを表示します。 |

## <a name="examples"></a>例

追加されたボリュームと現在の環境内にある別名を表示するには、次のように入力します。

```
add
```

次の出力は、ドライブ C がシャドウコピーセットに追加されたことを示しています。

```
Volume c: alias System1    GUID \\?\Volume{XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX}\
1 volume in Shadow Copy Set.
No Diskshadow aliases in the environment.
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)