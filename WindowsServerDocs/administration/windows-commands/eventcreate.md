---
title: eventcreate
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f2b1b26d-a70e-49a6-832b-91eb5a1a159a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 80d575364adbeba9d9ea4da75a0a866bcc02acea
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818713"
---
# <a name="eventcreate"></a>eventcreate



管理者は、指定されたイベント ログにカスタム イベントを作成できます。 このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
eventcreate [/s <Computer> [/u <Domain\User> [/p <Password>]] {[/l {APPLICATION|SYSTEM}]|[/so <SrcName>]} /t {ERROR|WARNING|INFORMATION|SUCCESSAUDIT|FAILUREAUDIT} /id <EventID> /d <Description>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/s\<コンピューター >|名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定はローカル コンピュータです。|
|/u \<Domain\User>|指定されたユーザーのアカウント権限でコマンドを実行\<ユーザー > または < domain \user >。 既定では現在のコマンドを実行するコンピューターのユーザー ログオンのアクセス許可です。|
|/p\<パスワード >|指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。|
|/l {アプリケーション\|システム}|イベントを作成するイベント ログの名前を指定します。 有効なログ名は、アプリケーションおよびシステムです。|
|/so \<SrcName>|イベントに使用するソースを指定します。 有効なソースは、任意の文字列と、アプリケーションまたはイベントを生成するコンポーネントを表す必要があります。|
|/t {エラー\|警告\|情報\|</br>SUCCESSAUDIT\|FAILUREAUDIT}|作成するイベントの種類を指定します。 有効な型は、エラー、警告、情報、SUCCESSAUDIT、および failureaudit です。|
|/id \<EventID>|イベントのイベント ID を指定します。 有効な ID は、1 から 1000 の任意の数です。|
|/d\<説明 >|新しく作成されたイベントに使用する説明を指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

-   カスタム イベントは、セキュリティ ログに書き込むことはできません。

## <a name="BKMK_examples"></a>例

次の例では、eventcreate コマンドを使用する方法を示します。
```
eventcreate /t error /id 100 /l application /d "Create event in application log"
eventcreate /t information /id 1000 /so winmgmt /d "Create event in WinMgmt source"
eventcreate /t error /id 2001 /so winword /l application /d "new src Winword in application log"
eventcreate /s server /t error /id 100 /l application /d "Remote machine without user credentials"
eventcreate /s server /u user /p password /id 100 /t error /l application /d "Remote machine with user credentials"
eventcreate /s server1 /s server2 /u user /p password /id 100 /t error /so winmgmt /d "Creating events on Multiple remote machines"
eventcreate /s server /u user /id 100 /t warning /so winmgmt /d "Remote machine with partial user credentials"
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)
