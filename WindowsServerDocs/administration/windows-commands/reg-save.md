---
title: reg save
description: 指定したファイルにレジストリの指定したサブキー、エントリ、および値のコピーを保存する reg save コマンドの参照記事です。
ms.topic: article
ms.assetid: b326482b-c8af-467d-a20c-0481eeda3d5c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 187811b277ca109ac3f3e1517aeb169bd8baca15
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87884016"
---
# <a name="reg-save"></a>reg save

指定したファイルで指定されたサブキー、エントリ、およびレジストリの値のコピーを保存します。

## <a name="syntax"></a>構文

```
reg save <keyname> <filename> [/y]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
|--|--|
| `<keyname>` | サブキーの完全なパスを指定します。 リモートコンピューターを指定するには、コンピューター名 (形式) を `\\<computername>\` *keyname*の一部として含めます。 省略 `\\<computername>\` すると、操作は既定でローカルコンピューターに設定されます。 *Keyname*には、有効なルートキーを含める必要があります。 ローカルコンピューターの有効なルートキーは、 **HKLM**、 **HKCU**、 **HKCR**、 **HKU**、および**HKCC**です。 リモートコンピューターが指定されている場合、有効なルートキーは**HKLM**と**HKU**です。 レジストリキー名にスペースが含まれている場合は、キー名を引用符で囲みます。 |
| `<filename>` | 作成されたファイルの名前とパスを指定します。 パスが指定されていない場合は、現在のパスが使用されます。 |
| /y | 確認を求めるメッセージを表示せずに、既存のファイルを*filename*という名前で上書きします。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>Remarks

- レジストリエントリを編集する前に、 **reg save**コマンドを使用して親サブキーを保存する必要があります。 編集に失敗した場合は、 **reg 復元**操作を使用して元のサブキーを復元できます。

- **Reg 保存**操作の戻り値は次のとおりです。

    | 値 | 説明 |
    |--|--|
    | 0 | 成功 |
    | 1 | 障害 |

### <a name="examples"></a>例

現在のフォルダーに hive MyApp AppBkUp.hiv という名前のファイルを保存するには、次のように入力します。

```
reg save HKLM\Software\MyCo\MyApp AppBkUp.hiv
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [reg 復元コマンド](reg-restore.md)