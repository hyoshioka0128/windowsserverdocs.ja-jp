---
title: reg query
description: Reg query コマンドの参照記事。レジストリ内の指定されたサブキーの下にあるサブキーとエントリの次のレベルの一覧を返します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0e6a0d7c-ed9b-4318-833d-33f265a81f39
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 18b7c5223227e0cf19de22f8bc9886ae798f027f
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931064"
---
# <a name="reg-query"></a>reg query

次の層のサブキーと、レジストリで指定したサブキーの下にあるエントリの一覧を返します。

## <a name="syntax"></a>構文

```
reg query <keyname> [{/v <Valuename> | /ve}] [/s] [/se <separator>] [/f <data>] [{/k | /d}] [/c] [/e] [/t <Type>] [/z]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
|--|--|
| `<keyname>` | サブキーの完全なパスを指定します。 リモートコンピューターを指定するには、コンピューター名 (形式) を `\\<computername>\` *keyname*の一部として含めます。 省略 `\\<computername>\` すると、操作は既定でローカルコンピューターに設定されます。 *Keyname*には、有効なルートキーを含める必要があります。 ローカルコンピューターの有効なルートキーは、 **HKLM**、 **HKCU**、 **HKCR**、 **HKU**、および**HKCC**です。 リモートコンピューターが指定されている場合、有効なルートキーは**HKLM**と**HKU**です。 レジストリキー名にスペースが含まれている場合は、キー名を引用符で囲みます。 |
| /v`<Valuename>` | 照会するレジストリ値の名前を指定します。 省略した場合は、 *keyname*のすべての値の名前が返されます。 **/F**オプションも使用されている場合、このパラメーターの*Valuename*は省略可能です。 |
| /ve | 値の名前が空のクエリを実行します。 |
| /s | すべてのサブキーと値の名前を再帰的にクエリを指定します。 |
| /se`<separator>` | [値の名前の種類**REG_MULTI_SZ**で検索する単一の値の区切り記号を指定します。 *区切り記号*が指定されていない場合は、 **\ 0**が使用されます。 |
| /f `<data>` | データを検索するパターンを指定します。 文字列にスペースが含まれている場合は、二重引用符を使用します。 指定しない場合、ワイルドカード (**&#42;**) が検索パターンとして使用されます。 |
| /k | キー名のみで検索を指定します。 |
| /d | データのみで検索するよう指定します。 |
| /c | クエリを大文字小文字を区別することを示します。 既定では、クエリでは大文字小文字が区別されません。 |
| /e | 完全一致のみを返すように指定します。 既定では、すべての一致が返されます。 |
| /t`<Type>` | 検索するレジストリの種類を指定します。 有効な種類は、 **REG_SZ**、 **REG_MULTI_SZ**、 **REG_EXPAND_SZ**、 **REG_DWORD**、 **REG_BINARY**、 **REG_NONE**です。 指定されていない場合は、すべての型が検索されます。 |
| /z | レジストリの型に対応する数値を検索結果に含めるように指定します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>注釈

- **Reg クエリ**操作の戻り値は次のとおりです。

    | 値 | [説明] |
    |--|--|
    | 0 | 成功 |
    | 1 | 障害 |

### <a name="examples"></a>例

名前値のバージョンの値を HKLM\Software\Microsoft\ResKit キーを表示するには、次のように入力します。

```
reg query HKLM\Software\Microsoft\ResKit /v Version
```

ABC という名前のリモート コンピューター上のすべてのサブキーと HKLM\Software\Microsoft\ResKit\Nt\Setup キーの値を表示するに次のように入力します。

```
reg query \\ABC\HKLM\Software\Microsoft\ResKit\Nt\Setup /s
```

を区切り記号として使用 REG_MULTI_SZ 型のサブキーと値をすべて表示するには **#** 、次のように入力します。

```
reg query HKLM\Software\Microsoft\ResKit\Nt\Setup /se #
```

キーを表示するには、値と完全一致と大文字小文字を区別のデータと一致するシステムのデータ種類が REG_SZ の HKLM ルートの下。

```
reg query HKLM /f SYSTEM /t REG_SZ /c /e
```

データ型が REG_BINARY の HKCU ルートキーの下のデータで、 **0f**に一致するキー、値、およびデータを表示するには、次のように入力します。

```
reg query HKCU /f 0F /d /t REG_BINARY
```

値と値の名前は hklm \software の下にある null (既定値) のデータを表示するには、次のように入力します。

```
reg query HKLM\SOFTWARE /ve
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
