---
title: 編集
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4e0ff2e8-3518-47c1-8c69-5e93f895fa0e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4dfffefbe113bc5df242a00357c769aaa9c1c787
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80845225"
---
# <a name="edit"></a>編集



ASCII テキストファイルを作成および変更する MS-DOS エディターを起動します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
edit [/b] [/h] [/r] [/s] [/<NNN>] [[<Drive>:][<Path>]<FileName> [<FileName2> [...]]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[\<ドライブ >:][<Path>]<FileName> [<FileName2> [...]]|1つ以上の ASCII テキストファイルの場所と名前を指定します。 ファイルが存在しない場合は、MS-DOS エディターによって作成されます。 ファイルが存在する場合は、MS-DOS エディターが開き、その内容が画面に表示されます。 *ファイル名*にはワイルドカード **&#42;** 文字 (および **?** ) を含めることができます。 複数のファイル名をスペースで区切ります。|
|/b|白黒モードで、MS-DOS エディターが白黒で表示されるようにします。|
|/h|現在のモニターで使用できる最大行数を表示します。|
|/r|読み取り専用モードでファイルを読み込みます。|
|/s|短いファイル名の使用を強制します。|
|\<NNN >|バイナリファイルを読み込み、行を*NNN*文字幅に折り返します。|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="remarks"></a>コメント

-   追加のヘルプを表示するには、MS-DOS エディターを開き、F1 キーを押します。
-   一部のモニターは、既定ではショートカットキーの表示をサポートしていません。 モニターにショートカットキーが表示されない場合は、 **/b**を使用します。

## <a name="examples"></a><a name=BKMK_examples></a>例

MS-DOS エディターを開くには、次のように入力します。
```
edit
```
現在のディレクトリに newtextfile という名前のファイルを作成して編集するには、次のように入力します。
```
edit newtextfile.txt
```