---
title: bootcfg copy
description: '**Bootcfg copy**の Windows コマンドに関するトピックでは、既存のブートエントリのコピーを作成します。これには、コマンドラインオプションを追加できます。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2a236c2a-8675-444d-b695-9cbc9aff643b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 42a408443cbe6722c25780f7c27d70b05da7eb8e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380121"
---
# <a name="bootcfg-copy"></a>bootcfg copy

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

既存のブートエントリのコピーを作成します。これには、コマンドラインオプションを追加できます。

## <a name="syntax"></a>構文
```
bootcfg /copy [/s <computer> [/u <Domain>\<User> /p <Password>]] [/d <Description>] [/id <OSEntryLineNum>]
```
## <a name="parameters"></a>パラメーター

|      パラメーター       |                                                                                             説明                                                                                             |
|----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /s <computer>     |                                         名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定はローカル コンピュータです。                                          |
| /u <Domain>\\<User>  | <User>または <Domain>\\<User>によって指定されたユーザーのアカウントアクセス許可を使用してコマンドを実行します。 既定値は、コマンドを実行しているコンピューターの現在のログオンユーザーのアクセス許可です。 |
|    /p <Password>     |                                                        指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。                                                        |
|   /d <Description>   |                                                                    新しいオペレーティングシステムエントリの説明を指定します。                                                                    |
| /id <OSEntryLineNum> |         コピーする Boot.ini ファイルの [オペレーティングシステム] セクションにあるオペレーティングシステムエントリの行番号を指定します。 [オペレーティングシステム] セクションヘッダーの後の最初の行は1です。         |
|          /?          |                                                                                コマンド プロンプトにヘルプを表示します。                                                                                 |

## <a name="BKMK_examples"></a>例
次の例では、 **bootcfg/copy**コマンドを使用してブートエントリ1をコピーし、説明として「\ ABC Server\\」と入力する方法を示します。
```
bootcfg /copy /d "\ABC Server\" /id 1
```
#### <a name="additional-references"></a>その他の参照情報
[コマンド ライン構文の記号](command-line-syntax-key.md)
