---
title: tscon
description: リモートデスクトップセッションホスト (rd セッションホスト) サーバー上の別のセッションに接続する tscon のリファレンス記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 315a9793-cd10-4987-bb68-89a9d13f7fce
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 83f8778d73d022ed41fcab14795eb3cdf41dc6cf
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86954944"
---
# <a name="tscon"></a>tscon

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートデスクトップセッションホストサーバー上の別のセッションに接続します。



> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 最新バージョンの新機能については、Windows Server TechNet ライブラリの「 [Windows server 2012 のリモートデスクトップサービスの新機能](/previous-versions/orphan-topics/ws.11/hh831527(v=ws.11))」を参照してください。

## <a name="syntax"></a>構文
```
tscon {<SessionID> | <SessionName>} [/dest:<SessionName>] [/password:<pw> | /password:*] [/v]
```
### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------|--------|
|\<SessionID>|接続先のセッションの ID を指定します。 省略可能な **/dest:** < *SessionName*> パラメーターを使用すると、これは接続先のセッションの ID になります。|
|\<SessionName>|接続先のセッションの名前を指定します。|
|/dest\<SessionName>|現在のセッションの名前を指定します。 新しいセッションに接続すると、このセッションは切断されます。|
|/password\<pw>|接続先のセッションを所有するユーザーのパスワードを指定します。 このパスワードは、接続しているユーザーがセッションを所有していない場合に必要です。|
|/password: *|接続先のセッションを所有するユーザーのパスワードの入力を求めます。|
|/v|実行されているアクションに関する情報を表示します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈
-   別のセッションに接続するには、フルコントロールアクセス許可を持っているか、特殊なアクセス許可を接続している必要があります。
-   **/Dest:** < *SessionName*の> パラメーターを使用すると、別のユーザーのセッションを別のセッションに接続できます。
-   <*password*> パラメーターにパスワードを指定せず、ターゲットセッションが現在のセッション以外のユーザーに属している場合、 **tscon**は失敗します。
-   コンソールセッションに接続することはできません。

## <a name="examples"></a>例
- 現在の rd セッションホストサーバーのセッション12に接続し、現在のセッションを切断するには、次のように入力します。
  ```
  tscon 12
  ```
- 現在の rd セッションホストサーバーのセッション23に接続するには、パスワード mypass 使用して、現在のセッションを切断し、次のように入力します。
  ```
  tscon 23 /password:mypass
  ```
- TERM03 という名前のセッションを TERM05 という名前のセッションに接続し、セッション TERM05 を切断します。接続されている場合は、次のように入力します。
  ```
  tscon TERM03 /v /dest:TERM05
  ```
  ## <a name="additional-references"></a>その他のリファレンス
  - [コマンドライン構文のキー](command-line-syntax-key.md) 
  [リモートデスクトップサービス (ターミナルサービス) のコマンドリファレンス](remote-desktop-services-terminal-services-command-reference.md)
