---
title: pushprinterconnections
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: c571d3adffd0e6a28f63f6d821b2524dc055aa9a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873723"
---
# <a name="pushprinterconnections"></a>pushprinterconnections



グループ ポリシーから展開されたプリンター接続設定を読み取ります、必要に応じて、プリンター接続の展開/削除します。

## <a name="syntax"></a>構文

```
pushprinterconnections <-log> <-?>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|<-ログ >|書き込み、%temp、または書き込みをデバッグ ログ ファイルをユーザーごと、windir%\temp をデバッグ ログをコンピューターごとです。|
|<-?>|コマンド プロンプトでヘルプを表示します。|

## <a name="remarks"></a>注釈

このユーティリティは、マシンの起動またはユーザーのログオン スクリプトで使用し、コマンドラインから実行するか。

#### <a name="additional-references"></a>その他の参照情報

-   [コマンドライン構文キー](command-line-syntax-key.md)
-   [グループ ポリシーを使用してプリンターを展開します。](https://go.microsoft.com/fwlink/?LinkId=230627)