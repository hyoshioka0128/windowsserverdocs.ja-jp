---
title: パラメーターの説明
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0b3486a5-896b-4d92-84b8-e463a0b76487
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: abebe5799075653d2ace1af4eadbdd5d477d97a6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362161"
---
# <a name="where"></a>パラメーターの説明



指定された検索パターンに一致するファイルの場所を表示します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
where [/r <Dir>] [/q] [/f] [/t] [$<ENV>:|<Path>:]<Pattern>[ ...] 
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/r \<Dir >|指定されたディレクトリから始まる再帰検索を示します。|
|/q|一致するファイルの一覧を表示せずに、終了コード (成功の場合は**0** 、失敗の場合は**1** ) を返します。|
|/f|**Where**コマンドの結果を引用符で囲んで表示します。|
|/t|ファイルのサイズと、一致した各ファイルの最終更新日時を表示します。|
|[$ \<ENV >: \| @ no__t-2Path >:] \<Pattern > [...]|一致するファイルの検索パターンを指定します。 少なくとも1つのパターンが必要であり、パターンには **&#42;** ワイルドカード文字 (と **?** ) を含めることができます。 既定では、は、現在のディレクトリと PATH 環境変数で指定されているパス**を検索し**ます。 別の検索パスを指定するには、$*ENV*:*pattern* ( *ENV*は1つ以上のパスを含む既存の環境変数) を使用するか、format *path*:*pattern* ( *path*は検索するディレクトリパス。 これらの省略可能な形式は、 **/r**コマンドラインオプションと共に使用することはできません。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>コメント

-   ファイル名拡張子を指定しない場合、PATHEXT 環境変数に記載されている拡張子が既定でパターンに追加されます。
-   では、再帰的な検索を実行したり、日付やサイズなどのファイル情報を表示したり、ローカルコンピューター上のパスの代わりに環境変数を使用し**たりできます**。

## <a name="BKMK_examples"></a>例

現在のコンピューターとそのサブディレクトリの C ドライブにある Test という名前のすべてのファイルを検索するには、次のように入力します。
```
where /r c:\ test 
```
パブリックディレクトリ内のすべてのファイルを一覧表示するには、次のように入力します。
```
where $public:*.*
```
リモートコンピューターのドライブ C、Computer1、およびそのサブディレクトリにあるメモ帳という名前のすべてのファイルを検索するには、次のように入力します。
```
where /r \\computer1\c notepad.*
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)