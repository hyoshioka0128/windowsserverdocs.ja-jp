---
title: pushprinterconnections
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c30afb97-b149-478f-a4b9-2cbc25361818 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5941b1eba55ce7524946f3257c093d409ef7d773
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80837075"
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

## <a name="remarks"></a>コメント

このユーティリティは、マシンの起動またはユーザーのログオン スクリプトで使用し、コマンドラインから実行するか。

## <a name="additional-references"></a>その他の参照情報

-   - [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [グループポリシーを使用してプリンターを展開する](https://go.microsoft.com/fwlink/?LinkId=230627)