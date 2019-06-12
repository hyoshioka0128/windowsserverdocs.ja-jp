---
ms.assetid: 77545920-2d13-4f35-a4d1-14dbec8340dc
title: fsutil スパース
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: b1bc4e45ed2a2b06c72318e0999988ed8f016c40
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438969"
---
# <a name="fsutil-sparse"></a>fsutil スパース
>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows 7

スパース ファイルを管理します。

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
|     queryflag     |                                                  クエリはスパースです。                                                  |
|    queryrange     |                        ファイルをスキャンし、0 以外のデータが含まれる範囲を検索します。                        |
|      setflag      |                                        スパースとして指定されたファイルをマークします。                                        |
|     setrange      |                                   ファイルの指定した範囲をゼロに設定します。                                   |
|    <FileName>     | ファイル名と拡張子、たとえば C:\documents\filename.txt を含むファイルへの完全パスを指定します。 |
| <BeginningOffset> |                              スパース ファイルとしてマークするファイル内のオフセットを指定します。                              |
|     <Length>      |                 領域の長さ (バイト) をスパースとしてマーク済みであるファイルを指定します。                 |

## <a name="remarks"></a>注釈

-   スパース ファイルは、未割り当てのデータの 1 つまたは複数の領域を持つファイルです。 プログラムは、値が 0 バイトを含むようこれら未割り当てのリージョンが表示されますが、これらのゼロを表すためにディスク領域は使用されません。 Nonmeaningful のすべてのデータ (ゼロで構成されるデータの大きな文字列) が割り当てられていませんが、意味のある、または 0 以外のすべてのデータが割り当てられます。 スパース ファイルが読み取られるときに、格納されている割り当て済みのデータが返され、未割り当てのデータが返されます、既定では、値 0 の場合は、C2 セキュリティ要件の仕様に従って。 スパース ファイルのサポートにより、データをファイルに任意の場所から解除します。

-   スパース ファイルでは、ゼロの大きな範囲はディスクの割り当てのない必要があります。 ファイルが書き込まれるときに、必要に応じて、0 以外のデータ用の領域が割り当てられます。

-   のみ圧縮またはスパース ファイルにオペレーティング システムに既知の範囲をゼロがあることができます。

-   ファイルがスパース ファイルまたは圧縮の場合は、NTFS はファイル内のディスク領域を解放できます。 ファイルのサイズを拡張せずゼロ バイトの範囲を設定します。

## <a name="BKMK_examples"></a>例
スパースとして C:\Temp ディレクトリに Sample.txt をという名前のファイルをマークするには、次のように入力します。

```
fsutil sparse setflag c:\temp\sample.txt 
```

#### <a name="additional-references"></a>その他の参照情報
[コマンド ライン構文の記号](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)


