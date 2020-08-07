---
title: reg import
description: Reg import コマンドの参照記事。エクスポートされたレジストリサブキー、エントリ、および値を含むファイルの内容をローカルコンピューターのレジストリにコピーします。
ms.topic: article
ms.assetid: 0be103de-08fc-4f02-b590-361782680b3e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4461f10cb31447a40f3d49df7731980f0f8a88a2
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87884143"
---
# <a name="reg-import"></a>reg import

コピーを含むファイルの内容は、ローカル コンピューターのレジストリにレジストリ キー、エントリ、および値をエクスポートします。

## <a name="syntax"></a>構文

```
reg import <filename>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
|--|--|
| `<filename>` | ローカル コンピューターのレジストリにコピーされるコンテンツを含むファイルのパスと名前を指定します。 使用してこのファイルを事前に作成する必要があります **reg エクスポート**します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>Remarks

- **Reg インポート**操作の戻り値は次のとおりです。

    | 値 | 説明 |
    |--|--|
    | 0 | 成功 |
    | 1 | 障害 |

### <a name="examples"></a>例

レジストリ エントリ AppBkUp.reg という名前のファイルからをインポートするには、次のように入力します。

```
reg import AppBkUp.reg
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [reg export コマンド](reg-export.md)
