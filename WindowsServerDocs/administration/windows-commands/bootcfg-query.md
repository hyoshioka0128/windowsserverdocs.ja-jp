---
title: bootcfg query
description: Windows コマンド」のトピック**bootcfg クエリ**-クエリと表示 [ブート ローダー] および [オペレーティング システム] セクション Boot.ini からのエントリ。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a4cacfd1-10a6-4a11-b0c5-f8abde72bfc8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e79acc100a9ec9955f2692a3c6ee812d0310b687
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434732"
---
# <a name="bootcfg-query"></a>bootcfg query

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

クエリを実行し、[ブート ローダー] を表示し、[オペレーティング システム] セクション Boot.ini からのエントリ。

## <a name="syntax"></a>構文
```
bootcfg /query [/s <computer> [/u <Domain>\<User> /p <Password>]]
```
## <a name="parameters"></a>パラメーター

|        項目         |                                                                                             定義                                                                                              |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /s <computer>    |                                         名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定はローカル コンピュータです。                                          |
| /u <Domain>\\<User> | 指定されたユーザーのアカウント権限でコマンドを実行<User>または<Domain> \\<User>します。 既定では現在のコマンドを実行するコンピューターのユーザー ログオンのアクセス許可です。 |
|    /p <Password>    |                                                        指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。                                                        |
|         /?          |                                                                                コマンド プロンプトにヘルプを表示します。                                                                                 |

##### <a name="remarks"></a>注釈
- 次のサンプルは、 **bootcfg/query**出力。
  ```
  Boot Loader Settings
  ----------
  timeout: 30
  default: multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
  Boot Entries
  ------
  Boot entry ID:   1
  Friendly Name:   ""
  path:            multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
  OS Load Options: /fastdetect /debug /debugport=com1:
  ```
- ブート ローダーの設定部分、 **bootcfg クエリ**出力には、Boot.ini の [ブート ローダー] セクションの各エントリが表示されます。
- ブート エントリの部分、 **bootcfg クエリ**出力には、Boot.ini の [operating systems] セクションの各オペレーティング システム エントリの次の詳細が表示されます。ブート エントリ ID、フレンドリ名、パス、および OS ロード オプション。
  ## <a name="BKMK_examples"></a>例
  次の例を使用する方法、 **bootcfg/query**コマンド。
  ```
  bootcfg /query
  bootcfg /query /s srvmain /u maindom\hiropln /p p@ssW23
  bootcfg /query /u hiropln /p p@ssW23
  ```
  #### <a name="additional-references"></a>その他の参照
  [コマンド ライン構文の記号](command-line-syntax-key.md)
