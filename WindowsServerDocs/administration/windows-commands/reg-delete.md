---
title: reg delete
description: レジストリからサブキーまたはエントリを削除する reg delete コマンドの参照記事です。
ms.topic: article
ms.assetid: cee05071-1607-4ab1-b8ab-65caebeb85c3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: da541f55117e287df81b53a45c923ed2ed3ae028
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87884158"
---
# <a name="reg-delete"></a>reg delete

レジストリからサブキーまたはエントリを削除します。

## <a name="syntax"></a>構文

```
reg delete <keyname> [{/v Valuename | /ve | /va}] [/f]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
|--|--|
| `<keyname1>` | サブキーまたは追加されるエントリの完全なパスを指定します。 リモートコンピューターを指定するには、コンピューター名 (形式) を `\\<computername>\` *keyname*の一部として含めます。 省略 `\\<computername>\` すると、操作は既定でローカルコンピューターに設定されます。 *Keyname*には、有効なルートキーを含める必要があります。 ローカルコンピューターの有効なルートキーは、 **HKLM**、 **HKCU**、 **HKCR**、 **HKU**、および**HKCC**です。 リモートコンピューターが指定されている場合、有効なルートキーは**HKLM**と**HKU**です。 レジストリキー名にスペースが含まれている場合は、キー名を引用符で囲みます。 |
| /v`<Valuename>` | サブキーの特定のエントリを削除します。 エントリが指定されていない場合、すべてのエントリとサブキーの下のサブキーは削除されます。 |
| /ve | 値を持たないエントリのみが削除されることを指定します。 |
| /va | 指定したサブキーの下のすべてのエントリを削除します。 指定したサブキーの下のサブキーは削除されません。 |
| /f | 確認を求めずに、既存のレジストリ サブキーまたはエントリを削除します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>Remarks

- **Reg の削除**操作の戻り値は次のとおりです。

    | 値 | 説明 |
    |--|--|
    | 0 | 成功 |
    | 1 | 障害 |

### <a name="examples"></a>例

タイムアウトのレジストリ キーとそのすべてのサブキーと値を削除するには、次のように入力します。

```
reg delete HKLM\Software\MyCo\MyApp\Timeout
```

干支という名前のコンピューター上のレジストリ値 [HKLM\Software\MyCo MTU を削除するには、次のように入力します。

```
reg delete \\ZODIAC\HKLM\Software\MyCo /v MTU
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
