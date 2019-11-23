---
title: bootcfg query
description: '**Bootcfg クエリ**の Windows コマンドに関するトピック-クエリを実行し、boot.ini の [ブートローダー] セクションと [オペレーティングシステム] セクションのエントリを表示します。'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: ae82357cfe178343872448c2ebd46c49a797b5a9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379913"
---
# <a name="bootcfg-query"></a>bootcfg query

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Boot.ini の [ブートローダー] セクションと [オペレーティングシステム] セクションのエントリを照会して表示します。

## <a name="syntax"></a>構文
```
bootcfg /query [/s <computer> [/u <Domain>\<User> /p <Password>]]
```
## <a name="parameters"></a>パラメーター

|        用語         |                                                                                             定義                                                                                              |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /s <computer>    |                                         名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定はローカル コンピュータです。                                          |
| /u <Domain>\\<User> | <User>または <Domain>\\<User>によって指定されたユーザーのアカウントアクセス許可を使用してコマンドを実行します。 既定値は、コマンドを実行しているコンピューターの現在のログオンユーザーのアクセス許可です。 |
|    /p <Password>    |                                                        指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。                                                        |
|         /?          |                                                                                コマンド プロンプトにヘルプを表示します。                                                                                 |

##### <a name="remarks"></a>注釈
- 次に、 **bootcfg/query**の出力の例を示します。
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
- **Bootcfg クエリ**出力のブートローダー設定部分では、boot.ini の [ブートローダー] セクションに各エントリが表示されます。
- **Bootcfg クエリ**出力のブートエントリの部分には、boot.ini の [オペレーティングシステム] セクションで、ブートエントリ ID、フレンドリ名、パス、OS 読み込みオプションの各オペレーティングシステムエントリについて、次の詳細が表示されます。
  ## <a name="BKMK_examples"></a>例
  次の例は、 **bootcfg/query**コマンドを使用する方法を示しています。
  ```
  bootcfg /query
  bootcfg /query /s srvmain /u maindom\hiropln /p p@ssW23
  bootcfg /query /u hiropln /p p@ssW23
  ```
  #### <a name="additional-references"></a>その他の参照情報
  [コマンド ライン構文の記号](command-line-syntax-key.md)
