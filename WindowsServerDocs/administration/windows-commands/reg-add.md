---
title: reg add
description: レジストリに新しいサブキーまたはエントリを追加する reg add コマンドの参照記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d9ad143e-dc10-4e2e-a229-408393c40079
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: db968e8fb55a4de73f5221f8149f794600f6884e
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933517"
---
# <a name="reg-add"></a>reg add

新しいサブキーまたはエントリをレジストリに追加します。

## <a name="syntax"></a>構文

```
reg add <keyname> [{/v Valuename | /ve}] [/t datatype] [/s Separator] [/d Data] [/f]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
|--|--|
| `<keyname>` | サブキーまたは追加されるエントリの完全なパスを指定します。 リモートコンピューターを指定するには、コンピューター名 (形式) を `\\<computername>\` *keyname*の一部として含めます。 省略 `\\<computername>\` すると、操作は既定でローカルコンピューターに設定されます。 *Keyname*には、有効なルートキーを含める必要があります。 ローカルコンピューターの有効なルートキーは、 **HKLM**、 **HKCU**、 **HKCR**、 **HKU**、および**HKCC**です。 リモートコンピューターが指定されている場合、有効なルートキーは**HKLM**と**HKU**です。 レジストリキー名にスペースが含まれている場合は、キー名を引用符で囲みます。 |
| /v`<Valuename>` | Add レジストリエントリの名前を指定します。 |
| /ve | 追加されたレジストリエントリの値が null であることを指定します。 |
| /t`<Type>` | レジストリ エントリの種類を指定します。 *型* 、次のいずれかを指定する必要があります。<ul><li>REG_SZ</li><li>REG_MULTI_SZ</li><li>REG_DWORD_BIG_ENDIAN</li><li>REG_DWORD</li><li>REG_BINARY</li><li>REG_DWORD_LITTLE_ENDIAN</li><li>REG_LINK</li><li>REG_FULL_RESOURCE_DESCRIPTOR</li><li>REG_EXPAND_SZ</li></ul> |
| /s`<Separator>` | **REG_MULTI_SZ**データ型が指定されていて、複数のエントリが一覧表示されている場合に、データの複数のインスタンスを区切るために使用する文字を指定します。 既定の区切り記号は、指定しない場合、 **\0**します。 |
| d`<Data>` | 新しいレジストリ エントリのデータを指定します。 |
| /f | 確認を求めずに、レジストリ エントリを追加します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>注釈

- この操作でサブツリーを追加することはできません。 このバージョンの**reg**は、サブキーを追加するときに確認を求めません。

- **Reg add**操作の戻り値は次のとおりです。

| 値 | [説明] |
|--|--|
| 0 | 成功 |
| 1 | 障害 |

- **REG_EXPAND_SZ**キーの種類には、 **^** /d パラメーターの内部にあるカレット記号 () を使用し **%** ます。

### <a name="examples"></a>例

リモートコンピューター *ABC*にキー *HKLM\Software\MyCo*を追加するには、次のように入力します。

```
reg add \\ABC\HKLM\Software\MyCo
```

*HKLM\Software\MyCo*に、*データ*という名前の値、型*REG_BINARY*、および*fe340ead*のデータと共にレジストリエントリを追加するには、次のように入力します。

```
reg add HKLM\Software\MyCo /v Data /t REG_BINARY /d fe340ead
```

*HKLM\Software\MyCo*に複数値レジストリエントリを追加するには、 *MRU*、型*REG_MULTI_SZ*、および*fax\0mail\0\0*のデータ型の値を使用して、次のように入力します。

```
reg add HKLM\Software\MyCo /v MRU /t REG_MULTI_SZ /d fax\0mail\0\0
```

展開されたレジストリエントリを*HKLM\Software\MyCo*に追加するには、 *Path*、type *REG_EXPAND_SZ*、および *% systemroot%* のデータを次のように入力します。

```
reg add HKLM\Software\MyCo /v Path /t REG_EXPAND_SZ /d ^%systemroot^%
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
