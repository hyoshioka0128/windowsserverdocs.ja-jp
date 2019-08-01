---
title: tsdiscon
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 13139674-7dee-4965-8cac-32f4928e8b9a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a1b5fca329864ebed9eab66671a17493f0fc3ca8
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440914"
---
# <a name="tsdiscon"></a>tsdiscon

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモート デスクトップ セッション ホスト (rd セッション ホスト) サーバーからセッションを切断します。
このコマンドを使用する方法の例については、次を参照してください。[例](#BKMK_examples)します。

> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 最新バージョンの新機能については、Windows Server TechNet ライブラリの[Windows Server 2012 のリモートデスクトップサービスの新機能](https://technet.microsoft.com/library/hh831527) を参照してください。

## <a name="syntax"></a>構文
```
tsdiscon [<SessionID> | <SessionName>] [/server:<ServerName>] [/v]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------|--------|
|\<SessionId>|切断するセッションの ID を指定します。|
|\<SessionName>|切断するセッションの名前を指定します。|
|/server:\<ServerName >|切断するセッションを格納しているターミナル サーバーを指定します。 それ以外の場合、現在の rd セッション ホスト サーバーが使用されます。|
|/v|実行する操作についての情報を表示します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈
-   フル コントロール権限を持っているか、別のユーザー セッションから切断する特別なアクセス許可を切断する必要があります。
-   セッション ID または名前が指定されていない場合**tsdiscon**現在のセッションを切断します。
-   セッションを切断するときに実行されていたすべてのアプリケーションは、データの損失なしでそのセッションに再接続したときに自動的に実行しています。 使用**セッションをリセット**切断されたセッションの実行中のアプリケーションを終了するセッションでのデータが失われる可能性があることに注意してください。
-   **/Server**パラメーターは、使用する場合にのみ必要**tsdiscon**リモート サーバーからです。
-   コンソール セッションは切断されることはできません。

## <a name="BKMK_examples"></a>例
- 現在のセッションを切断するには、次のように入力します。
  ```
  tsdiscon
  ```
- 10 のセッションを切断するには、次のように入力します。
  ```
  tsdiscon 10
  ```
- TERM04 をという名前のセッションを切断するには、次のように入力します。
  ```
  tsdiscon TERM04
  ```
  #### <a name="additional-references"></a>その他の参照情報
  [コマンドライン構文キー](command-line-syntax-key.md)
  [リモート デスクトップ サービス &#40;ターミナル サービス&#41; コマンドのリファレンス](remote-desktop-services-terminal-services-command-reference.md)
