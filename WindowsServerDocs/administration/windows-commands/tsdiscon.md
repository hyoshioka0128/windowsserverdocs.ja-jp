---
title: tsdiscon
description: Tsdiscon の Windows コマンドに関するトピックでは、リモートデスクトップセッションホストサーバーからセッションを切断します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 13139674-7dee-4965-8cac-32f4928e8b9a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b008fa920290043b64e7421e91a545123634f1e7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80832515"
---
# <a name="tsdiscon"></a>tsdiscon

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

セッションをリモートデスクトップセッションホストサーバーから切断します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

> [!NOTE]
> Windows Server 2008 R2 では、ターミナル サービスはリモート デスクトップ サービスという名前に変更されました。 最新バージョンの新機能については、Windows Server TechNet ライブラリの「 [Windows server 2012 のリモートデスクトップサービスの新機能](https://technet.microsoft.com/library/hh831527)」を参照してください。

## <a name="syntax"></a>構文
```
tsdiscon [<SessionID> | <SessionName>] [/server:<ServerName>] [/v]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------|--------|
|\<SessionId >|切断するセッションの ID を指定します。|
|\<のセッション >|切断するセッションの名前を指定します。|
|/server:\<ServerName >|切断するセッションを含むターミナルサーバーを指定します。 それ以外の場合は、現在の rd セッションホストサーバーが使用されます。|
|/v|実行されているアクションに関する情報を表示します。|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="remarks"></a>コメント
-   別のユーザーをセッションから切断するには、フルコントロールアクセス許可を持っているか、特殊なアクセス許可を切断する必要があります。
-   セッション ID またはセッション名が指定されていない場合、 **tsdiscon**は現在のセッションを切断します。
-   セッションを切断したときに実行されていたアプリケーションは、データを失うことなくそのセッションに再接続すると、自動的に実行されます。 **リセットセッション**を使用して、切断されたセッションの実行中のアプリケーションを終了します。ただし、セッションでデータが失われる可能性があることに注意してください。
-   **/Server**パラメーターは、リモートサーバーから**tsdiscon**を使用する場合にのみ必要です。
-   コンソールセッションを切断できません。

## <a name="examples"></a><a name=BKMK_examples></a>例
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
  ## <a name="additional-references"></a>その他の参照情報
  - [コマンドライン構文のキー](command-line-syntax-key.md)
  [リモートデスクトップサービス (ターミナルサービス) のコマンドリファレンス](remote-desktop-services-terminal-services-command-reference.md)
