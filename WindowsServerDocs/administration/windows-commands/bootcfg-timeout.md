---
title: bootcfg timeout
description: '**Bootcfg timeout**の Windows コマンドに関するトピック-オペレーティングシステムのタイムアウト値を変更します。'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 94bc2de43dd179117c7a44747961213d12741a09
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379871"
---
# <a name="bootcfg-timeout"></a>bootcfg timeout

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

オペレーティングシステムのタイムアウト値を変更します。

## <a name="syntax"></a>構文
```
bootcfg /timeout <timeOutValue> [/s <computer> [/u <Domain\User>/p <Password>]]
```
## <a name="parameters"></a>パラメーター

|        パラメーター        |                                                                                                                                                                                  説明                                                                                                                                                                                   |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /timeout <timeOutValue> | [ブートローダー] セクションのタイムアウト値を指定します。 <timeOutValue> は、NTLDR が既定値を読み込む前に、ユーザーがブートローダー画面からオペレーティングシステムを選択する必要がある秒数です。 <timeOutValue> の有効な範囲は0-999 です。 値が0の場合、NTLDR はブートローダー画面を表示せずに、既定のオペレーティングシステムを直ちに開始します。 |
|      /s <computer>      |                                                                                                                               名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定はローカル コンピュータです。                                                                                                                               |
|    /u < Domain\User >     |                                                                                       <User> または < Domain\User > で指定したユーザーのアカウントアクセス許可を使用してコマンドを実行します。 既定値は、コマンドを実行しているコンピューターの現在のログオンユーザーのアクセス許可です。                                                                                        |
|      /p <Password>      |                                                                                                                                            **/U**パラメーターで指定したユーザーアカウントの <Password> を指定します。                                                                                                                                             |
|           /?            |                                                                                                                                                                      コマンド プロンプトにヘルプを表示します。                                                                                                                                                                      |

## <a name="BKMK_examples"></a>例
次の例は、 **bootcfg/timeout**コマンドを使用する方法を示しています。
```
bootcfg /timeout 30
bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /timeout 50
```
#### <a name="additional-references"></a>その他の参照情報
[コマンド ライン構文の記号](command-line-syntax-key.md)
