---
title: cd
description: Cd コマンドの参照記事。現在のディレクトリの名前を表示するか、現在のディレクトリを変更します。
ms.topic: article
ms.assetid: 932d9cc1-3dff-40da-835c-1cb0894874f1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 87766cd7be95eeb9cbecd29ec88a044224dc81da
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87880380"
---
# <a name="cd"></a>cd

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

現在のディレクトリの名前を表示するか、現在のディレクトリを変更します。 ドライブ文字 (など) でのみ使用する場合 `cd C:` 、 **cd**は、指定されたドライブの現在のディレクトリの名前を表示します。 パラメーターを指定せずに使用した場合、 **cd**には現在のドライブとディレクトリが表示されます。

> [!NOTE]
> このコマンドは、 [chdir コマンド](chdir.md)と同じです。

## <a name="syntax"></a>構文

```
cd [/d] [<drive>:][<path>]
cd [..]
chdir [/d] [<drive>:][<path>]
chdir [..]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| /d | 現在のドライブおよびドライブの現在のディレクトリを変更します。 |
| `<drive>:` | 表示または変更するドライブを指定します (現在のドライブと異なる場合)。 |
| `<path>` | 表示または変更するディレクトリへのパスを指定します。 |
| [..] | 親フォルダーに変更することを指定します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

## <a name="remarks"></a>Remarks

コマンド拡張機能が有効になっている場合、 **cd**コマンドには次の条件が適用されます。

- 現在のディレクトリ文字列は、ディスク上の名前と同じケースを使用するように変換されます。 たとえば、は、 `cd c:\temp` ディスク上の場合、現在のディレクトリを C:\Temp に設定します。

- スペースは区切り記号として扱われないため、 `<path>` 引用符を囲まずにスペースを含めることができます。 次に例を示します。

  ```
  cd username\programs\start menu
  ```

  は、次のコードと同じです。

  ```
  cd "username\programs\start menu"
  ```

  拡張機能が無効になっている場合は、引用符が必要です。

- コマンド拡張機能を無効にするには、次のように入力します。

  ```
  cmd /e:off
  ```

## <a name="examples"></a>例

ルートディレクトリに戻るには、ドライブのディレクトリ階層の最上位にあります。

```
cd\
```

使用しているドライブとは異なるドライブの既定のディレクトリを変更するには、次のようにします。

```
cd [<drive>:[<directory>]]
```

ディレクトリへの変更を確認するには、次のように入力します。

```
cd [<drive>:]
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [chdir コマンド](chdir.md)
