---
title: 編集
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4e0ff2e8-3518-47c1-8c69-5e93f895fa0e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c77941d39118554b6b59e436e63d67a4a1f7c8cb
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720861"
---
# <a name="edit"></a>編集



ASCII テキストファイルを作成および変更する MS-DOS エディターを起動します。



## <a name="syntax"></a>構文

```
edit [/b] [/h] [/r] [/s] [/<NNN>] [[<Drive>:][<Path>]<FileName> [<FileName2> [...]]
```

### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|[\<ドライブ>:][<Path>]<FileName> [<FileName2> [...]]|1つ以上の ASCII テキストファイルの場所と名前を指定します。 ファイルが存在しない場合は、MS-DOS エディターによって作成されます。 ファイルが存在する場合は、MS-DOS エディターが開き、その内容が画面に表示されます。 *ファイル名*にはワイルドカード文字 (**&#42;** と **?**) を含めることができます。 複数のファイル名をスペースで区切ります。|
|/b|白黒モードで、MS-DOS エディターが白黒で表示されるようにします。|
|/h|現在のモニターで使用できる最大行数を表示します。|
|/r|読み取り専用モードでファイルを読み込みます。|
|/s|短いファイル名の使用を強制します。|
|\<NNN>|バイナリファイルを読み込み、行を*NNN*文字幅に折り返します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>Remarks

-   追加のヘルプを表示するには、MS-DOS エディターを開き、F1 キーを押します。
-   一部のモニターは、既定ではショートカットキーの表示をサポートしていません。 モニターにショートカットキーが表示されない場合は、 **/b**を使用します。

## <a name="examples"></a>例

MS-DOS エディターを開くには、次のように入力します。
```
edit
```
現在のディレクトリに newtextfile という名前のファイルを作成して編集するには、次のように入力します。
```
edit newtextfile.txt
```