---
title: add alias
description: エイリアスの追加コマンドのリファレンストピック。別名環境に別名を追加します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5fe12f5d-11e9-4f3d-b7f9-40b26c8685e5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 66301a39a1e969e270b42b5ce92a73392a134357
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83819662"
---
# <a name="add-alias"></a>add alias

エイリアスをエイリアス環境に追加します。 パラメーターを指定せずに使用する場合、**エイリアスの追加**コマンドプロンプトでヘルプを表示します。 エイリアスはメタデータファイルに保存され、**メタデータの読み込み**コマンドを使用して読み込まれます。

## <a name="syntax"></a>構文

```
add alias <aliasname> <aliasvalue>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<aliasname>` | エイリアスの名前を指定します。 |
| `<aliasvalue>` | エイリアスの値を指定します。 |
| `? | コマンド プロンプトにヘルプを表示します。 |

## <a name="examples"></a>例

エイリアスを含むすべての影を一覧表示するには、次のように入力します。

```
list shadows all
```

次の抜粋は、既定のエイリアスである*VSS_SHADOW_x*が割り当てられているシャドウコピーを示しています。

```
* Shadow Copy ID = {ff47165a-1946-4a0c-b7f4-80f46a309278}
%VSS_SHADOW_1%
```

*System1*という名前の新しいエイリアスをこのシャドウコピーに割り当てるには、次のように入力します。

```
add alias System1 %VSS_SHADOW_1%
```

または、シャドウコピー ID を使用してエイリアスを割り当てることもできます。

```
add alias System1 {ff47165a-1946-4a0c-b7f4-80f46a309278}
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [メタデータの読み込みコマンド](load-metadata.md)
