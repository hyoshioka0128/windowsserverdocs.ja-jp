---
title: bootcfg timeout
description: Windows コマンド」のトピック**bootcfg タイムアウト**-オペレーティング システムのタイムアウト値を変更します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aa858eac-2bb7-4a27-a9bc-3e4a6eb8b2c6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1fc33d2d20d6d2532c5ed1f33e27a768935d1e85
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434641"
---
# <a name="bootcfg-timeout"></a>bootcfg timeout

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

オペレーティング システムのタイムアウト値を変更します。

## <a name="syntax"></a>構文
```
bootcfg /timeout <timeOutValue> [/s <computer> [/u <Domain\User>/p <Password>]]
```
## <a name="parameters"></a>パラメーター

|        パラメーター        |                                                                                                                                                                                  説明                                                                                                                                                                                   |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /timeout <timeOutValue> | [ブート ローダー] セクションでは、タイムアウト値を指定します。 <timeOutValue>は、ユーザーは、NTLDR が既定値を読み込む前に、ブート ローダーの画面から、オペレーティング システムを選択する必要があります秒数です。 有効な範囲<timeOutValue>は 0 ~ 999 です。 値が 0 の場合、NTLDR はブート ローダーの画面を表示せずに、既定のオペレーティング システムをすぐに起動します。 |
|      /s <computer>      |                                                                                                                               名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定はローカル コンピュータです。                                                                                                                               |
|    /u <Domain\User>     |                                                                                       指定されたユーザーのアカウント権限でコマンドを実行<User>または < domain \user >。 既定では現在のコマンドを実行するコンピューターのユーザー ログオンのアクセス許可です。                                                                                        |
|      /p <Password>      |                                                                                                                                            指定します、<Password>で指定されているユーザー アカウントの **/u**パラメーター。                                                                                                                                             |
|           /?            |                                                                                                                                                                      コマンド プロンプトにヘルプを表示します。                                                                                                                                                                      |

## <a name="BKMK_examples"></a>例
次の例を使用する方法、 **bootcfg/timeout**コマンド。
```
bootcfg /timeout 30
bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /timeout 50
```
#### <a name="additional-references"></a>その他の参照
[コマンド ライン構文の記号](command-line-syntax-key.md)
