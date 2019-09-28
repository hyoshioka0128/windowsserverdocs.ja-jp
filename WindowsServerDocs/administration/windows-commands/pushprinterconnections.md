---
title: pushprinterconnections
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c30afb97-b149-478f-a4b9-2cbc25361818 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fe25a29af34f78ebe161dc0d07c5edf64257f5c2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371958"
---
# <a name="pushprinterconnections"></a>pushprinterconnections



展開されたプリンター接続設定をグループポリシーから読み取り、必要に応じてプリンター接続を展開または削除します。

## <a name="syntax"></a>構文

```
pushprinterconnections <-log> <-?>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|<-ログ >|書き込み、%temp、または書き込みをデバッグ ログ ファイルをユーザーごと、windir%\temp をデバッグ ログをコンピューターごとです。|
|<-? >|コマンド プロンプトでヘルプを表示します。|

## <a name="remarks"></a>コメント

このユーティリティは、マシンの起動またはユーザーのログオン スクリプトで使用し、コマンドラインから実行するか。

#### <a name="additional-references"></a>その他の参照情報

-   [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [グループポリシーを使用してプリンターを展開する](https://go.microsoft.com/fwlink/?LinkId=230627)