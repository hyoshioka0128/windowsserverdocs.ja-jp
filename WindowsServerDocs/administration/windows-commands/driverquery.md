---
title: driverquery
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 92ca4b84-e4e2-405b-9f31-bf6db9f66839
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5d44a1be300b7178bc2271187344c2fc4ab8815e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377649"
---
# <a name="driverquery"></a>driverquery



インストールされているデバイスドライバーとそのプロパティの一覧を管理者が表示できるようにします。 パラメーターを指定せずに使用した場合、 **driverquery**はローカルコンピューター上で実行されます。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
driverquery [/s <System> [/u [<Domain>\]<Username> [/p <Password>]]] [/fo {table | list | csv}] [/nh] [/v | /si]
```

## <a name="parameters"></a>パラメーター

|         パラメーター         |                                                                                                                                         説明                                                                                                                                          |
|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       /s @no__t 0System >        |                                                                                      名前またはリモート コンピューターの IP アドレスを指定します。 円記号を使用しないでください。 既定はローカル コンピュータです。                                                                                       |
| /u [\<Domain > \] @ no__t | *ユーザー*または*ドメイン*\*user @ no__t-3 によって指定されたユーザーアカウントの資格情報でコマンドを実行します。既定では、\* @ no__t-1/s @ no__t @ no__t は、コマンドを発行しているコンピューターに現在ログオンしているユーザーの資格情報を使用します。 **/s**が指定されている場合を除き、 **/u**は使用できません。 |
|      /p \<パスワード >       |                                                                           指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。 **/p**は、 **/u**が指定されている場合には使用できません。                                                                            |
|        /fo {テーブル         |                                                                                                                                             list                                                                                                                                             |
|            /nh            |                                                                                      表示されているドライバー情報からヘッダー行を除外します。 **/Fo**パラメーターが**list**に設定されている場合は無効です。                                                                                      |
|            /v             |                                                                                                               詳細出力を表示します。 **/v**は、署名されたドライバーでは無効です。                                                                                                               |
|            /si            |                                                                                                                          署名されたドライバーに関する情報を提供します。                                                                                                                          |
|            /?             |                                                                                                                             コマンド プロンプトにヘルプを表示します。                                                                                                                             |

## <a name="BKMK_examples"></a>例

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
ローカルコンピューター上の現在の資格情報を使用して、 **server1**というリモートサーバーで**driverquery**コマンドを使用するには、次のように入力します。
```
driverquery /s server1
```
**Server1**という名前のリモートサーバーで**driverquery**コマンドを使用するには、ドメイン**maindom**で**user1**の資格情報を使用し、次のように入力します。
```
driverquery /s server1 /u maindom\user1 /p p@ssw3d
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)