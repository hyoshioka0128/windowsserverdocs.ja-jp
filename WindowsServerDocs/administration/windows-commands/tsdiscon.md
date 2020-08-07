---
title: tsdiscon
description: Tsdiscon のリファレンス記事。リモートデスクトップセッションホストサーバーからセッションを切断します。
ms.topic: article
ms.assetid: 13139674-7dee-4965-8cac-32f4928e8b9a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e81a1c7f68af0bb1d16ce64bb4985e3ddb8d18f2
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87897076"
---
# <a name="tsdiscon"></a>tsdiscon

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

セッションをリモートデスクトップセッションホストサーバーから切断します。



> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 最新バージョンの新機能については、Windows Server TechNet ライブラリの「 [Windows server 2012 のリモートデスクトップサービスの新機能](/previous-versions/orphan-topics/ws.11/hh831527(v=ws.11))」を参照してください。

## <a name="syntax"></a>構文
```
tsdiscon [<SessionID> | <SessionName>] [/server:<ServerName>] [/v]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------|--------|
|\<SessionId>|切断するセッションの ID を指定します。|
|\<SessionName>|切断するセッションの名前を指定します。|
|/server:\<ServerName>|切断するセッションを含むターミナルサーバーを指定します。 それ以外の場合は、現在の rd セッションホストサーバーが使用されます。|
|/v|実行されているアクションに関する情報を表示します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>Remarks
-   別のユーザーをセッションから切断するには、フルコントロールアクセス許可を持っているか、特殊なアクセス許可を切断する必要があります。
-   セッション ID またはセッション名が指定されていない場合、 **tsdiscon**は現在のセッションを切断します。
-   セッションを切断したときに実行されていたアプリケーションは、データを失うことなくそのセッションに再接続すると、自動的に実行されます。 **リセットセッション**を使用して、切断されたセッションの実行中のアプリケーションを終了します。ただし、セッションでデータが失われる可能性があることに注意してください。
-   **/Server**パラメーターは、リモートサーバーから**tsdiscon**を使用する場合にのみ必要です。
-   コンソールセッションを切断できません。

## <a name="examples"></a>例
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
