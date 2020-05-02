---
title: eventcreate
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f2b1b26d-a70e-49a6-832b-91eb5a1a159a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 797298622ba1021caef3d04e2f2f06f016ef6a70
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725759"
---
# <a name="eventcreate"></a>eventcreate



管理者が、指定されたイベントログにカスタムイベントを作成できるようにします。 

## <a name="syntax"></a>構文

```
eventcreate [/s <Computer> [/u <Domain\User> [/p <Password>]] {[/l {APPLICATION|SYSTEM}]|[/so <SrcName>]} /t {ERROR|WARNING|INFORMATION|SUCCESSAUDIT|FAILUREAUDIT} /id <EventID> /d <Description>
```

### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|/s \<コンピューター>|名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定はローカル コンピュータです。|
|/u \<Domain\User>|ユーザー> によって\<指定されたユーザーのアカウントアクセス許可を使用してコマンドを実行するか、Domain\User> <します。 既定値は、コマンドを実行しているコンピューターの現在のログオンユーザーのアクセス許可です。|
|/p \<パスワード>|指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。|
|/l {アプリケーション\|システム}|イベントが作成されるイベントログの名前を指定します。 有効なログ名は、アプリケーションとシステムです。|
|/so \<SrcName>|イベントに使用するソースを指定します。 有効なソースは任意の文字列にすることができ、イベントを生成しているアプリケーションまたはコンポーネントを表す必要があります。|
|/t {エラー\|警告\|情報\|</br>SUCCESSAUDIT\|FAILUREAUDIT}|作成するイベントの種類を指定します。 有効な種類は、ERROR、WARNING、INFORMATION、SUCCESSAUDIT、および FAILUREAUDIT です。|
|/id \<EventID>|イベントのイベント ID を指定します。 有効な ID は、1 ~ 1000 の任意の数です。|
|/d \<説明>|新しく作成されたイベントに使用する説明を指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>Remarks

-   カスタムイベントをセキュリティログに書き込むことはできません。

## <a name="examples"></a>例

次の例は、eventcreate コマンドを使用する方法を示しています。
```
eventcreate /t error /id 100 /l application /d Create event in application log
eventcreate /t information /id 1000 /so winmgmt /d Create event in WinMgmt source
eventcreate /t error /id 2001 /so winword /l application /d new src Winword in application log
eventcreate /s server /t error /id 100 /l application /d Remote machine without user credentials
eventcreate /s server /u user /p password /id 100 /t error /l application /d Remote machine with user credentials
eventcreate /s server1 /s server2 /u user /p password /id 100 /t error /so winmgmt /d Creating events on Multiple remote machines
eventcreate /s server /u user /id 100 /t warning /so winmgmt /d Remote machine with partial user credentials
```

#### <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
