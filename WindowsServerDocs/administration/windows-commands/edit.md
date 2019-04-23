---
title: 編集
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4e0ff2e8-3518-47c1-8c69-5e93f895fa0e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 096632005b3e42dd941ccc7c72c08ead1d291b53
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873153"
---
# <a name="edit"></a>編集



MS-DOS エディターで作成され、ASCII テキスト ファイルの変更を開始します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
edit [/b] [/h] [/r] [/s] [/<NNN>] [[<Drive>:][<Path>]<FileName> [<FileName2> [...]]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[\<Drive>:][<Path>]<FileName> [<FileName2> [...]]|1 つまたは複数の ASCII テキスト ファイルの名前と場所を指定します。 ファイルが存在しない場合は、MS-DOS エディター作成されます。 ファイルが存在する場合は MS-DOS 開かれ、画面にその内容を表示します。 *ファイル名*ワイルドカード文字を含めることができます (**&#42;** と **?**)。 複数のファイル名を空白で区切ります。|
|/b|強制的にモノクロ モード、MS-DOS エディターに白と黒で表示できるようにします。|
|/h|現在のモニターには、可能な行の最大数を表示します。|
|/r|読み取り専用モードでファイルを読み込みます。|
|/s|短いファイル名の使用を強制します。|
|\<NNN>|行の折り返しのバイナリ ファイルを読み込みます*NNN*文字分の幅。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

-   詳細については、MS-DOS のエディターを開き、F1 キーを押します。
-   いくつかのモニターは、既定でショートカット キーの表示をサポートしています。 モニターがショートカット キーが表示されない場合は、使用 **/b**します。

## <a name="BKMK_examples"></a>例

MS-DOS のエディターを開くには、次のように入力します。
```
edit
```
作成して、現在のディレクトリに newtextfile.txt という名前のファイルを編集する、次のように入力します。
```
edit newtextfile.txt
```