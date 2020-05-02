---
title: reg インポート
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0be103de-08fc-4f02-b590-361782680b3e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3e7e033091752f97086fd27fcb94e62469f0cced
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722550"
---
# <a name="reg-import"></a>reg インポート



コピーを含むファイルの内容は、ローカル コンピューターのレジストリにレジストリ キー、エントリ、および値をエクスポートします。



## <a name="syntax"></a>構文

```
Reg import FileName
```

### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|\<ファイル名>|ローカル コンピューターのレジストリにコピーされるコンテンツを含むファイルのパスと名前を指定します。 使用してこのファイルを事前に作成する必要があります **reg エクスポート**します。|
|/?|ヘルプを表示 **reg インポート** コマンド プロンプト。|

## <a name="remarks"></a>Remarks

次の表に、戻り値の **reg インポート** 操作します。

|値|[説明]|
|-----|-----------|
|0|Success|
|1|障害|

## <a name="examples"></a>例

レジストリ エントリ AppBkUp.reg という名前のファイルからをインポートするには、次のように入力します。
```
reg import AppBkUp.reg
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)