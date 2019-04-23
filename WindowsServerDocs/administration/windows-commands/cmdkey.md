---
title: cmdkey
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5fcd68ee-a14a-4b71-9300-c3f5c5d31e8e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7080a3ae28fed722f17cf8311aa1e2fd3bece41f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854613"
---
# <a name="cmdkey"></a>cmdkey

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

保存されたユーザー名とパスワードのほか、資格情報の作成、一覧表示、削除を行います。

## <a name="syntax"></a>構文
```
cmdkey [{/add:<TargetName>|/generic:<TargetName>}] {/smartcard|/user:<UserName> [/pass:<Password>]} [/delete{:<TargetName>|/ras}] /list:<TargetName>
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/を追加します。<TargetName>|ユーザー名とパスワードを一覧に追加します。<br /><br />パラメーターが必要です<TargetName>このエントリの関連付けられているコンピューターまたはドメイン名を識別します。|
|/generic:<TargetName>|汎用の資格情報を一覧に追加します。<br /><br />パラメーターが必要です<TargetName>このエントリの関連付けられているコンピューターまたはドメイン名を識別します。|
|/smartcard|スマート カードから資格情報を取得します。|
|/user:<UserName>|このエントリに格納するには、ユーザーまたはアカウント名を指定します。 場合*UserName*が指定されていないことが要求されます。|
|/pass:<Password>|このエントリに格納するためのパスワードを指定します。 場合*パスワード*が指定されていないことが要求されます。|
|/delete{:<TargetName> &#124; /ras}|一覧からユーザー名とパスワードを削除します。 場合*TargetName*エントリが削除されることを指定します。 /Ras が指定されている場合は、保存されているリモート アクセス エントリが削除されます。|
|/list:<TargetName>|保存されたユーザー名と資格情報を一覧表示します。 場合*TargetName*が指定すると、保存されているすべてのユーザー名と資格情報を一覧表示されます。|
|/?|コマンド プロンプトにヘルプを表示します。|
## <a name="remarks"></a>注釈
-   /smartcard コマンド ライン オプションを使用する場合に、システムでは、複数のスマート カードが検出された場合**cmdkey**使用可能なすべてのスマート カードに関する情報が表示され、ユーザーを指定するメッセージが表示されます。
-   格納されていると、パスワードは表示されません。
## <a name="BKMK_examples"></a>例
すべてのユーザー名と保存されている資格情報の一覧を表示するには、次のように入力します。
```
cmdkey /list
```
Kleo パスワードを使用してアクセス コンピューター Server01 にユーザー名とユーザー Mikedan のパスワードを追加するに次のように入力します。
```
cmdkey /add:server01 /user:mikedan /pass:Kleo
```
Server01 がアクセスされるたびに、ユーザー名と Mikedan コンピューター Server01 にアクセスするユーザーのパスワードとパスワードのプロンプトを追加するに次のように入力します。
```
cmdkey /add:server01 /user:mikedan
```
リモート アクセスが格納されている資格情報を削除するには、次のように入力します。
```
cmdkey /delete /ras
```
Server01 に格納されている資格情報を削除するには、次のように入力します。
```
cmdkey /delete:Server01
```
## <a name="additional-references"></a>その他の参照
[コマンドライン構文キー](command-line-syntax-key.md)
