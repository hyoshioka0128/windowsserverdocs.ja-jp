---
title: fsutil sparse
description: スパースファイルを管理する fsutil sparse コマンドのリファレンストピックです。
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
ms.assetid: 77545920-2d13-4f35-a4d1-14dbec8340dc
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: e68ac844bb7aa7e22a9df0ddb0c982b3701231d7
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2020
ms.locfileid: "83435717"
---
# <a name="fsutil-sparse"></a>fsutil sparse

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8

スパースファイルを管理します。 スパースファイルは、割り当てられていないデータの1つ以上の領域を含むファイルです。

プログラムは、これらの未割り当て領域を、ゼロ値のバイトを含むものとして認識し、これらのゼロを表すディスク領域は存在しません。 スパースファイルが読み込まれると、割り当てられたデータが格納済みとして返され、C2 セキュリティ要件の仕様に従って、既定で未割り当てデータが0として返されます。 スパースファイルのサポートにより、ファイル内のどこからでもデータの割り当てを解除できます。

## <a name="syntax"></a>構文

```
fsutil sparse [queryflag] <filename>
fsutil sparse [queryrange] <filename>
fsutil sparse [setflag] <filename>
fsutil sparse [setrange] <filename> <beginningoffset> <length>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| queryflag | クエリのスパース。 |
| queryrange | ファイルをスキャンし、0以外のデータを含む可能性のある範囲を検索します。 |
| setflag | 指定されたファイルをスパースとしてマークします。 |
| setrange | 指定されたファイルの範囲を0で塗りつぶします。 |
| `<filename>` | ファイル名と拡張子を含むファイルへの完全パスを指定します (例*C:\documents\filename.txt*)。 |
| `<beginningoffset>` | スパースとしてマークするファイル内のオフセットを指定します。 |
| `<length>` | スパースとしてマークするファイル内の領域の長さを指定します (バイト単位)。 |

#### <a name="remarks"></a>解説

- 意味のある、または0以外のデータはすべて割り当てられますが、意味のないすべてのデータ (0 で構成される大きな文字列データ) は割り当てられません。

- スパースファイルでは、大規模なゼロの場合、ディスク割り当ては必要ありません。 0以外のデータの領域は、ファイルが書き込まれたときに必要に応じて割り当てられます。

- オペレーティングシステムに認識されるゼロの範囲を持つことができるのは、圧縮ファイルまたはスパースファイルだけです。

- ファイルがスパースまたは圧縮されている場合は、NTFS によってファイル内のディスク領域が割り当て解除されることがあります。 これにより、ファイルサイズを拡張せずに、バイトの範囲がゼロに設定されます。

### <a name="examples"></a>例

*C:\temp*ディレクトリの*file.txt*という名前のファイルをスパースとしてマークするには、次のように入力します。

```
fsutil sparse setflag c:\temp\sample.txt
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [fsutil](fsutil.md)
