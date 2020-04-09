---
title: を割り当てます。ここで、
description: Windows コマンドに関するトピックでは、指定された検索パターンに一致するファイルの場所が表示されます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0b3486a5-896b-4d92-84b8-e463a0b76487
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1b32424622e8a893023aad9365b6aec4a91764fa
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80829335"
---
# <a name="where"></a>を割り当てます。ここで、



指定された検索パターンに一致するファイルの場所を表示します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
where [/r <Dir>] [/q] [/f] [/t] [$<ENV>:|<Path>:]<Pattern>[ ...] 
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/r \<Dir >|指定されたディレクトリから始まる再帰検索を示します。|
|/q|一致するファイルの一覧を表示せずに、終了コード (成功の場合は**0** 、失敗の場合は**1** ) を返します。|
|/f|**Where**コマンドの結果を引用符で囲んで表示します。|
|/t|ファイルのサイズと、一致した各ファイルの最終更新日時を表示します。|
|[$\<ENV >:\|\<パス >:]\<パターン > [...]|一致するファイルの検索パターンを指定します。 少なくとも1つのパターンが必要であり、パターンには **&#42;** ワイルドカード文字 (と **?** ) を含めることができます。 既定では、は、現在のディレクトリと PATH 環境変数で指定されているパス**を検索し**ます。 別のパスを指定するには、$*env*:*pattern* ( *ENV*は1つ以上のパスを含む既存の環境変数) を使用するか、 *path*:*pattern*という形式を使用します (ここで、 *path*は検索するディレクトリパスです)。 これらの省略可能な形式は、 **/r**コマンドラインオプションと共に使用することはできません。|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="remarks"></a>コメント

-   ファイル名拡張子を指定しない場合、PATHEXT 環境変数に記載されている拡張子が既定でパターンに追加されます。
-   では、再帰的な検索を実行したり、日付やサイズなどのファイル情報を表示したり、ローカルコンピューター上のパスの代わりに環境変数を使用し**たりできます**。

## <a name="examples"></a><a name=BKMK_examples></a>例

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

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)