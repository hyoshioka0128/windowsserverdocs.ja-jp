---
title: driverquery
description: Driverquery コマンドの参照記事。管理者は、インストールされているデバイスドライバーとそのプロパティの一覧を表示できます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 92ca4b84-e4e2-405b-9f31-bf6db9f66839
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8ad0a028217e07d8c15b59dc96e31c8f236dd743
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931462"
---
# <a name="driverquery"></a>driverquery

インストールされているデバイスドライバーとそのプロパティの一覧を管理者が表示できるようにします。 パラメーターを指定せずに使用した場合、 **driverquery**はローカルコンピューター上で実行されます。

## <a name="syntax"></a>構文

```
driverquery [/s <system> [/u [<domain>\]<username> [/p <password>]]] [/fo {table | list | csv}] [/nh] [/v | /si]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- |------------ |
| /s`<system>` | 名前またはリモート コンピューターの IP アドレスを指定します。 円記号を使用しないでください。 既定値はローカル コンピューターです。 |
| /u`[<domain>]<username>` | *ユーザー*または*ドメイン \*ユーザーによって指定されたユーザーアカウントの資格情報でコマンドを実行します。 既定では、 */s*は、コマンドを発行しているコンピューターに現在ログオンしているユーザーの資格情報を使用します。 **/s**が指定されている場合を除き、 **/u**は使用できません。 |
| /p`<password>` | 指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。 **/p**は、 **/u**が指定されている場合には使用できません。 |
| /fo テーブル | 出力を表として書式設定します。 既定値です。 |
| /fo リスト | 出力を一覧として書式設定します。 |
| /fo csv | 出力にコンマ区切りの値を設定します。 |
| /nh | 表示されているドライバー情報からヘッダー行を除外します。 **/Fo**パラメーターが**list**に設定されている場合は無効です。 |
| /v | 詳細出力を表示します。 **/v**は、署名されたドライバーでは無効です。 |
| /si | 署名されたドライバーに関する情報を提供します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

### <a name="examples"></a>例

ローカルコンピューターにインストールされているデバイスドライバーの一覧を表示するには、次のように入力します。

```
driverquery
```

出力をコンマ区切り値 (CSV) 形式で表示するには、次のように入力します。

```
driverquery /fo csv
```

出力のヘッダー行を非表示にするには、次のように入力します。

```
driverquery /nh
```

ローカルコンピューター上の現在の資格情報を使用して、 *server1*というリモートサーバーで**driverquery**コマンドを使用するには、次のように入力します。

```
driverquery /s server1
```

*Server1*という名前のリモートサーバーで**driverquery**コマンドを使用するには、ドメイン*maindom*で*user1*の資格情報を使用し、次のように入力します。

```
driverquery /s server1 /u maindom\user1 /p p@ssw3d
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)