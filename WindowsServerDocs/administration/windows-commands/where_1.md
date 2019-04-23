---
title: パラメーターの説明
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: ff50405dd53ee383abc8e13f67befecf73e37c1d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832453"
---
# <a name="where"></a>パラメーターの説明



指定した検索パターンに一致するファイルの場所が表示されます。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
where [/r <Dir>] [/q] [/f] [/t] [$<ENV>:|<Path>:]<Pattern>[ ...] 
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/r \<Dir >|以降では、指定されたディレクトリを再帰的な検索を示します。|
|/q|終了コードを返します (**0**成功**1**エラーの) 一致するファイルの一覧を表示せずします。|
|/f|結果が表示されます、**場所**引用符で囲まれたコマンド。|
|/t|ファイルのサイズと、最終更新日と一致する各ファイルの時刻が表示されます。|
|[$\<ENV >:\|\<パス >:]\<パターン > [...]|一致するファイルの検索パターンを指定します。 少なくとも 1 つのパターンが必要であり、パターンは、ワイルドカード文字を含めることができます (**&#42;** と **?**)。 既定では、**場所**現在のディレクトリと、PATH 環境変数で指定されているパスを検索します。 形式 $ を使用して検索する別のパスを指定することができます*ENV*:*パターン*(場所*ENV*は 1 つまたは複数のパスを格納している既存の環境変数) を使用して、または形式*パス*:*パターン*(場所*パス*に検索するディレクトリ パス)。 これらの省略可能な形式は使用できません、 **/r**コマンド ライン オプション。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

-   ファイル名拡張子を指定しない場合、PATHEXT 環境変数である拡張機能は既定では、パターンに追加されます。
-   **場所**再帰検索を実行、サイズ、日付などのファイル情報を表示およびローカル コンピューター上のパスの代わりに環境変数を受け入れることができます。

## <a name="BKMK_examples"></a>例

現在のコンピューターとそのサブディレクトリの C ドライブのテストをという名前のすべてのファイルを検索するには、次のように入力します。
```
where /r c:\ test 
```
パブリック ディレクトリのすべてのファイルを一覧表示するには、次のように入力します。
```
where $public:*.*
```
リモート コンピューターで、Computer1 とそのサブディレクトリのドライブ C でメモ帳をという名前のすべてのファイルを検索するには、次のように入力します。
```
where /r \\computer1\c notepad.*
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)