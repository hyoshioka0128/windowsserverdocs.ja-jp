---
title: tskill
description: リモートデスクトップセッションホストサーバー上のセッションで実行されているプロセスを終了する tskill のリファレンス記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 08986e6a-6900-4ece-85a1-8f73b14db1b3 Lizap
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b5e4e32bada68b8c7d931b8603fbf09eba45791d
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86954884"
---
# <a name="tskill"></a>tskill

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートデスクトップセッションホストサーバー上のセッションで実行されているプロセスを終了します。


> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 最新バージョンの新機能については、Windows Server TechNet ライブラリの「 [Windows server 2012 のリモートデスクトップサービスの新機能](/previous-versions/orphan-topics/ws.11/hh831527(v=ws.11))」を参照してください。

## <a name="syntax"></a>構文
```
tskill {<ProcessID> | <ProcessName>} [/server:<ServerName>] [/id:<SessionID> | /a] [/v]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------|--------|
|\<ProcessID>|終了するプロセスの ID を指定します。|
|\<ProcessName>|終了するプロセスの名前を指定します。 このパラメーターには、ワイルドカード文字を含めることができます。|
|/server:\<ServerName>|終了するプロセスを含むターミナルサーバーを指定します。 **/Server**が指定されていない場合は、現在の RD セッションホストサーバーが使用されます。|
|/id\<SessionID>|指定されたセッションで実行されているプロセスを終了します。|
|/a|すべてのセッションで実行されているプロセスを終了します。|
|/v|実行されているアクションに関する情報を表示します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈
- **Tskill**を使用すると、管理者でない限り、自分に属しているプロセスのみを終了できます。 管理者は、すべての**tskill**関数にフルアクセスでき、他のユーザーセッションで実行されているプロセスを終了できます。
- セッション内で動作しているすべてのプロセスが終了すると、セッションも終了します。
- *ProcessName*パラメーターと **/server:**<em>ServerName</em>パラメーターを使用する場合は、 **/id:**<em>SessionID</em>または **/a**パラメーターも指定する必要があります。

## <a name="examples"></a>例
- プロセス6543を終了するには、次のように入力します。
  ```
  tskill 6543
  ```
- セッション5で実行されているプロセスエクスプローラーを終了するには、次のように入力します。
  ```
  tskill explorer /id:5
  ```
  ## <a name="additional-references"></a>その他のリファレンス
  - [コマンドライン構文のキー](command-line-syntax-key.md) 
  [リモートデスクトップサービス (ターミナルサービス) のコマンドリファレンス](remote-desktop-services-terminal-services-command-reference.md)
