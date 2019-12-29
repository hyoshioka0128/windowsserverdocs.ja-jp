---
title: tsdiscon
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 577ff8ee672583b85c907642bd21256124aa8034
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71369867"
---
# <a name="tsdiscon"></a>tsdiscon

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

セッションをリモートデスクトップセッションホスト (rd セッションホスト) サーバーから切断します。
このコマンドの使用方法の例については、「[例](#BKMK_examples)」を参照してください。

> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 最新バージョンの新機能については、Windows Server TechNet ライブラリの[Windows Server 2012 のリモートデスクトップサービスの新機能](https://technet.microsoft.com/library/hh831527) を参照してください。

## <a name="syntax"></a>構文
```
tsdiscon [<SessionID> | <SessionName>] [/server:<ServerName>] [/v]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------|--------|
|\<SessionId >|切断するセッションの ID を指定します。|
|\<のセッション >|切断するセッションの名前を指定します。|
|/server:\<ServerName >|切断するセッションを含むターミナルサーバーを指定します。 それ以外の場合は、現在の rd セッションホストサーバーが使用されます。|
|/v|実行されているアクションに関する情報を表示します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈
-   別のユーザーをセッションから切断するには、フルコントロールアクセス許可を持っているか、特殊なアクセス許可を切断する必要があります。
-   セッション ID またはセッション名が指定されていない場合、 **tsdiscon**は現在のセッションを切断します。
-   セッションを切断したときに実行されていたアプリケーションは、データを失うことなくそのセッションに再接続すると、自動的に実行されます。 **リセットセッション**を使用して、切断されたセッションの実行中のアプリケーションを終了します。ただし、セッションでデータが失われる可能性があることに注意してください。
-   **/Server**パラメーターは、リモートサーバーから**tsdiscon**を使用する場合にのみ必要です。
-   コンソールセッションを切断できません。

## <a name="BKMK_examples"></a>例
- 現在のセッションを切断するには、次のように入力します。
  ```
  tsdiscon
  ```
- セッション10を切断するには、次のように入力します。
  ```
  tsdiscon 10
  ```
- TERM04 という名前のセッションを切断するには、次のように入力します。
  ```
  tsdiscon TERM04
  ```
  #### <a name="additional-references"></a>その他の参照情報
  [コマンドライン構文キー](command-line-syntax-key.md)
  [リモート デスクトップ サービスと&#40;です。ターミナル サービスと&#41;です。コマンドのリファレンス](remote-desktop-services-terminal-services-command-reference.md)
