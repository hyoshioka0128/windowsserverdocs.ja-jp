---
ms.assetid: fb95c8ee-a418-4520-a12a-7754ae947c3c
title: Fsutil reparsepoint
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: fe274ad9a6dffc72607102d3430ba7527d3cc558
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376855"
---
# <a name="fsutil-reparsepoint"></a>Fsutil reparsepoint
>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows 7、Windows 2008、Windows Vista

再解析ポイントを照会または削除します。  **Fsutil reparsepoint**コマンドは、通常、サポート担当者によって使用されます。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
fsutil reparsepoint [query] <FileName>
fsutil reparsepoint [delete] <FileName>
```

## <a name="parameters"></a>パラメーター

| パラメーター  |                                                                説明                                                                |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------|
|   クエリ (query)    |            指定したハンドルによって識別されるファイルまたはディレクトリに関連付けられている再解析ポイントデータを取得します。             |
|   delete   | 指定したハンドルによって識別されるファイルまたはディレクトリから再解析ポイントを削除します。ただし、ファイルまたはディレクトリは削除しません。 |
| <FileName> |             ファイル名と拡張子を含むファイルへの完全パスを指定します (例 C:\documents\filename.txt.)。             |

## <a name="remarks"></a>コメント

-   再解析ポイントは、ユーザー定義データを含む定義可能な属性を持つ NTFS ファイルシステムオブジェクトです。このオブジェクトは、入力/出力 (i/o) サブシステムの機能を拡張するために使用されます。

-   再解析ポイントは、ディレクトリの接合ポイントとボリュームマウントポイントに使用されます。 また、ファイルシステムフィルタードライバーによって、特定のファイルをそのドライバーに特別なマークを付けるためにも使用されます。

-   プログラムは、再解析ポイントを設定すると、このデータと再解析タグを格納します。このタグは、格納されているデータを一意に識別します。 ファイルシステムは、再解析ポイントを使用してファイルを開くと、関連付けられているファイルシステムフィルターの検索を試みます。 ファイルシステムフィルターが見つかった場合、フィルターは再解析データによって指示されたファイルを処理します。 ファイルシステムフィルターが見つからない場合、ファイルオープン操作は失敗します。

## <a name="BKMK_examples"></a>例
C:\ サーバーに関連付けられている再解析ポイントデータを取得するには、次のように入力します。

```
fsutil reparsepoint query c:\server
```

指定したファイルまたはディレクトリから再解析ポイントを削除するには、次の形式を使用します。

```
fsutil reparsepoint delete c:\server
```

#### <a name="additional-references"></a>その他の参照情報
[コマンド ライン構文の記号](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)


