---
title: add
description: '**[追加]** の Windows コマンドトピックでは、シャドウコピーするボリュームのセットにボリュームを追加したり、エイリアス環境に別名を追加したりします。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 47efce7a-86d2-4872-ae31-baa108757afd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9895082cc10223fd08cff6916c20c3af5613e947
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851345"
---
# <a name="add"></a>add

シャドウコピーするボリュームのセットにボリュームを追加するか、エイリアス環境に別名を追加します。 サブコマンドなしで使用する場合は、現在のボリュームとエイリアスの一覧を**追加**します。

> [!NOTE]
> エイリアスは、シャドウコピーが作成されるまでエイリアス環境に追加されません。 すぐに必要なエイリアスを追加するには、 **add alias**を使用します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
add 
add volume <Volume> [provider <ProviderID>] 
add alias <AliasName> <AliasValue>
```

## <a name="add-subcommands"></a>サブコマンドの追加

| サブコマンド | 説明 |
| ---------- | ----------- |
| ボリューム●ぼりゅーむ○ | シャドウコピーするボリュームのセットであるボリュームをシャドウコピーセットに追加します。 「構文とパラメーターの[ボリュームの追加](add-volume.md)」を参照してください。 |
| 別名 | 指定された名前と値をエイリアス環境に追加します。 「構文とパラメーターの[別名の追加](add-alias.md)」を参照してください。 |
| `/?` | コマンドラインでヘルプを表示します。 |

## <a name="examples"></a><a name=BKMK_examples></a>例

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

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)