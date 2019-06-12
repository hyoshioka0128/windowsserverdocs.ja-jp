---
title: driverquery
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 88a59f9da9927bb923418695bc760303c0fb00b0
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439479"
---
# <a name="driverquery"></a>driverquery



管理者はインストールされているデバイス ドライバーとそのプロパティの一覧を表示できます。 パラメーターを指定せずに使用されている場合**driverquery**ローカル コンピューター上で実行します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
driverquery [/s <System> [/u [<Domain>\]<Username> [/p <Password>]]] [/fo {table | list | csv}] [/nh] [/v | /si]
```

## <a name="parameters"></a>パラメーター

|         パラメーター         |                                                                                                                                         説明                                                                                                                                          |
|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       /s\<システム >        |                                                                                      名前またはリモート コンピューターの IP アドレスを指定します。 円記号を使用しないでください。 既定はローカル コンピュータです。                                                                                       |
| /u [\<ドメイン >\]<Username> | 指定されたユーザー アカウントの資格情報でコマンドを実行*ユーザー*または*ドメイン*\*ユーザー<em>します。既定では、 \* \*/s</em> \*が現在のコマンドを発行しているコンピューターにログオンしたユーザーの資格情報を使用します。 **/u**いなければ使用できません **/s**を指定します。 |
|      /p\<パスワード >       |                                                                           指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。 **/p**いなければ使用できません **/u**を指定します。                                                                            |
|        /fo {テーブル         |                                                                                                                                             list                                                                                                                                             |
|            /nh            |                                                                                      ヘッダー行を表示するドライバー情報を省略します。 有効でない場合、 **/fo**にパラメーターが設定されている**一覧**します。                                                                                      |
|            /v             |                                                                                                               詳細な出力が表示されます。 **/v**は署名されたドライバーは無効です。                                                                                                               |
|            /si            |                                                                                                                          署名されたドライバーに関する情報を提供します。                                                                                                                          |
|            /?             |                                                                                                                             コマンド プロンプトにヘルプを表示します。                                                                                                                             |

## <a name="BKMK_examples"></a>例

ローカル コンピューターにインストールされているデバイス ドライバーの一覧を表示するには、次のように入力します。
```
driverquery 
```
コンマ区切り値 (CSV) 形式で出力を表示するには、次のように入力します。
```
driverquery /fo csv 
```
出力でヘッダー行を非表示には、次のように入力します。
```
driverquery /nh 
```
使用する、 **driverquery**という名前のリモート サーバーでコマンド**server1**ローカル コンピューターの現在の資格情報を使用して、入力します。
```
driverquery /s server1
```
使用する、 **driverquery**という名前のリモート サーバーでコマンド**server1**の資格情報を使用して**user1**ドメイン**maindom**種類。
```
driverquery /s server1 /u maindom\user1 /p p@ssw3d
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)