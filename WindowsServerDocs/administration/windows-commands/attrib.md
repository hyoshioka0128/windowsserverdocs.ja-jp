---
title: attrib
description: ファイルまたはディレクトリに割り当てられた属性を表示、設定、または削除する、 **attrib**の Windows コマンドトピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5e763ca5-21a2-45d2-b26d-a9c44c99091a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 94a6f307450b06dff81180b70f864bd9e1ed5885
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851255"
---
# <a name="attrib"></a>attrib

ファイルまたはディレクトリに割り当てられた属性を表示、設定、または削除します。 パラメーターを指定せずに使用した場合、 **attrib**では、現在のディレクトリ内のすべてのファイルの属性が表示されます。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
attrib [{+|-}r] [{+|-}a] [{+|-}s] [{+|-}h] [{+|-}i] [<Drive>:][<Path>][<FileName>] [/s [/d] [/l]]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `{+|-}r` | 読み取り専用のファイル属性を設定 ( **+** ) またはクリア ( **-** ) します。 |
| `{+\|-}a` | アーカイブファイルの属性を設定 ( **+** ) またはクリア ( **-** ) します。 |
| `{+\|-}s` | システムファイルの属性を設定 ( **+** ) またはクリア ( **-** ) します。 |
| `{+\|-}h` | 隠しファイル属性を設定 ( **+** ) またはクリア ( **-** ) します。 |
| `{+\|-}i` | Not Content インデックス付きファイル属性を設定 ( **+** ) またはクリア ( **-** ) します。 |
| `[<Drive>:][<Path>][<FileName>]` | 属性を表示または変更するディレクトリ、ファイル、またはファイルのグループの場所と名前を指定します。 使用することができ**ますか?** ファイル **&#42;** グループの属性を表示または変更するために、 *FileName*パラメーターにワイルドカード文字を使用します。 |
| /s | 現在のディレクトリとそのすべてのサブディレクトリ内のファイルに一致するように、 **attrib**および任意のコマンドラインオプションを適用します。 |
| /d | **Attrib**および任意のコマンドラインオプションをディレクトリに適用します。 |
| /l | シンボリックリンクのターゲットではなく、 **attrib**および任意のコマンドラインオプションをシンボリックリンクに適用します。 |
| /? | コマンド プロンプトでヘルプを表示します。 |

## <a name="remarks"></a>コメント

- ワイルドカード文字 ( **?** また **&#42;** は) ファイルグループの属性を表示または変更するための*FileName*パラメーターを使用します。

- ファイルに System (**s**) 属性または Hidden (**h**) 属性が設定されている場合は、そのファイルの他の属性を変更する前に属性をクリアする必要があります。

- Archive 属性 (**a**) は、前回のバックアップ以降に変更されたファイルをマークします。 **Xcopy**コマンドでは archive 属性が使用されていることに注意してください。

## <a name="examples"></a><a name=BKMK_examples></a>例

現在のディレクトリにある News86 という名前のファイルの属性を表示するには、次のように入力します。

```
attrib news86 
```

Test.txt という名前のファイルに読み取り専用属性を割り当てるには、次のように入力します。

```
attrib +r report.txt 
```

パブリックディレクトリのファイルと、ドライブ B のディスク上のサブディレクトリから読み取り専用の属性を削除するには、次のように入力します。

```
attrib -r b:\public\*.* /s 
```

ドライブ A のすべてのファイルに Archive 属性を設定し、.bak 拡張子を持つファイルの Archive 属性をクリアするには、次のように入力します。

```
attrib +a a:*.* & attrib -a a:*.bak 
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)