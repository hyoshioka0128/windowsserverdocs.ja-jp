---
title: pushprinterconnections
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c30afb97-b149-478f-a4b9-2cbc25361818
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1ed83b51da5ad7ad0a6b4dc0afd1d6bc30803a98
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222045"
---
# <a name="pushprinterconnections"></a>pushprinterconnections



展開されたプリンター接続設定をグループポリシーから読み取り、必要に応じてプリンター接続を展開または削除します。

## <a name="syntax"></a>構文

```
pushprinterconnections <-log> <-?>
```

#### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|<-ログ >|書き込み、%temp、または書き込みをデバッグ ログ ファイルをユーザーごと、windir%\temp をデバッグ ログをコンピューターごとです。|
|<-? >|コマンド プロンプトでヘルプを表示します。|

## <a name="remarks"></a>解説

このユーティリティは、マシンの起動またはユーザーのログオン スクリプトで使用し、コマンドラインから実行するか。

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [グループ ポリシーを使用してプリンターを展開します。](https://go.microsoft.com/fwlink/?LinkId=230627)