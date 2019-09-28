---
ms.assetid: 77545920-2d13-4f35-a4d1-14dbec8340dc
title: Fsutil sparse
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: f9fb3cf46afb7e96c13fb623bc8f4fe67c1f3694
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376808"
---
# <a name="fsutil-sparse"></a>Fsutil sparse
>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows 7

スパースファイルを管理します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
fsutil sparse [queryflag] <FileName>
fsutil sparse [queryrange] <FileName>
fsutil sparse [setflag] <FileName>
fsutil sparse [setrange] <FileName> <BeginningOffset> <Length>
```

## <a name="parameters"></a>パラメーター

|     パラメーター     |                                                    説明                                                    |
|-------------------|-------------------------------------------------------------------------------------------------------------------|
|     queryflag     |                                                  クエリのスパース。                                                  |
|    queryrange     |                        ファイルをスキャンし、0以外のデータを含む可能性のある範囲を検索します。                        |
|      setflag      |                                        指定されたファイルをスパースとしてマークします。                                        |
|     setrange      |                                   指定されたファイルの範囲を0で塗りつぶします。                                   |
|    <FileName>     | ファイル名と拡張子を含むファイルへの完全パスを指定します (例 C:\documents\filename.txt.)。 |
| <BeginningOffset> |                              スパースとしてマークするファイル内のオフセットを指定します。                              |
|     <Length>      |                 スパースとしてマークするファイル内の領域の長さを指定します (バイト単位)。                 |

## <a name="remarks"></a>コメント

-   スパースファイルは、割り当てられていないデータの1つ以上の領域を含むファイルです。 プログラムでは、これらの未割り当て領域が、値0のバイトを含むものとして表示されますが、これらのゼロを表すためのディスク領域は使用されません。 意味のある、または0以外のデータはすべて割り当てられますが、意味のないすべてのデータ (0 で構成される大きな文字列データ) は割り当てられません。 スパースファイルが読み込まれると、割り当てられたデータが格納済みとして返され、C2 セキュリティ要件の仕様に従って、既定で未割り当てデータが0として返されます。 スパースファイルのサポートにより、ファイル内のどこからでもデータの割り当てを解除できます。

-   スパースファイルでは、大規模なゼロの場合、ディスク割り当ては必要ありません。 0以外のデータの領域は、ファイルが書き込まれたときに必要に応じて割り当てられます。

-   オペレーティングシステムに認識されるゼロの範囲を持つことができるのは、圧縮ファイルまたはスパースファイルだけです。

-   ファイルがスパースまたは圧縮されている場合は、NTFS によってファイル内のディスク領域の割り当てが解除されることがあります。 これにより、ファイルサイズを拡張せずに、バイトの範囲がゼロに設定されます。

## <a name="BKMK_examples"></a>例
C:\Temp ディレクトリの file.txt という名前のファイルをスパースとしてマークするには、次のように入力します。

```
fsutil sparse setflag c:\temp\sample.txt 
```

#### <a name="additional-references"></a>その他の参照情報
[コマンド ライン構文の記号](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)


