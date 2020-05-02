---
title: pushprinterconnections
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c30afb97-b149-478f-a4b9-2cbc25361818 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 94ba2d09a3e67248a393350e46e971aa8b24b00d
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722763"
---
# <a name="pushprinterconnections"></a>pushprinterconnections



展開されたプリンター接続設定をグループポリシーから読み取り、必要に応じてプリンター接続を展開または削除します。

## <a name="syntax"></a>構文

```
pushprinterconnections <-log> <-?>
```

#### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|<-ログ >|書き込み、%temp、または書き込みをデバッグ ログ ファイルをユーザーごと、windir%\temp をデバッグ ログをコンピューターごとです。|
|<-? >|コマンド プロンプトでヘルプを表示します。|

## <a name="remarks"></a>Remarks

このユーティリティは、マシンの起動またはユーザーのログオン スクリプトで使用し、コマンドラインから実行するか。

## <a name="additional-references"></a>その他のリファレンス

-   - [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [グループ ポリシーを使用してプリンターを展開します。](https://go.microsoft.com/fwlink/?LinkId=230627)