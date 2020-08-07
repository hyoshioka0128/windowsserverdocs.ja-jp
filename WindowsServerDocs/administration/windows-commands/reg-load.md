---
title: reg load
description: レジストリの別のサブキーに保存されたサブキーとエントリを書き込む reg load コマンドのリファレンス記事です。
ms.topic: article
ms.assetid: 3b0b2b1b-f510-4108-9e9d-7057e924aa6e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bc44a6d992312f67abb29a91da848cc17787d507
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87884095"
---
# <a name="reg-load"></a>reg load

書き込みは、サブキーと別のサブキーにエントリをレジストリに保存します。 このコマンドは、レジストリエントリのトラブルシューティングや編集に使用される一時ファイルで使用するためのものです。

## <a name="syntax"></a>構文

```
reg load <keyname> <filename>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
|--|--|
| `<keyname>` | 読み込むサブキーの完全なパスを指定します。 リモートコンピューターを指定するには、コンピューター名 (形式) を `\\<computername>\` *keyname*の一部として含めます。 省略 `\\<computername>\` すると、操作は既定でローカルコンピューターに設定されます。 *Keyname*には、有効なルートキーを含める必要があります。 ローカルコンピューターの有効なルートキーは、 **HKLM**、 **HKCU**、 **HKCR**、 **HKU**、および**HKCC**です。 リモートコンピューターが指定されている場合、有効なルートキーは**HKLM**と**HKU**です。 レジストリキー名にスペースが含まれている場合は、キー名を引用符で囲みます。  |
| `<filename>` | 読み込むファイルのパスと名前を指定します。 このファイルは、事前に**reg save**コマンドを使用して作成する必要があり、.hiv 拡張子を持つ必要があります。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>Remarks

- **Reg 読み込み**操作の戻り値は次のとおりです。

    | 値 | 説明 |
    |--|--|
    | 0 | 成功 |
    | 1 | 障害 |

### <a name="examples"></a>例

キー HKLM\TempHive に TempHive.hiv をという名前のファイルを読み込むには、次のように入力します。

```
reg load HKLM\TempHive TempHive.hiv
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [reg save コマンド](reg-save.md)
