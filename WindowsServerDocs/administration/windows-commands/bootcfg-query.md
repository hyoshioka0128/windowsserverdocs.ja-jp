---
title: bootcfg query
description: Bootcfg クエリコマンドのリファレンストピックでは、boot.ini からブートローダーとオペレーティングシステムのセクションエントリを照会して表示します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a4cacfd1-10a6-4a11-b0c5-f8abde72bfc8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 44c5ce60f55618d16e80d1f1efde3af1cbf6c609
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82709333"
---
# <a name="bootcfg-query"></a>bootcfg query

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Boot.ini の [ブートローダー] セクションと [オペレーティングシステム] セクションのエントリを照会して表示します。

## <a name="syntax"></a>構文

```
bootcfg /query [/s <computer> [/u <domain>\<user> /p <password>]]
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| --------- | ----------- |
| `/s <computer>` | リモートコンピューターの名前または IP アドレスを指定します (円記号は使用しないでください)。 既定はローカル コンピュータです。 |
| `/u <domain>\<user>`  | または`<user>` `<domain>\<user>`によって指定されたユーザーのアカウントアクセス許可を使用してコマンドを実行します。 既定値は、コマンドを実行しているコンピューターの現在のログオンユーザーのアクセス許可です。 |
| `/p <password>` | 指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="sample-output"></a>サンプル出力

**Bootcfg/query**コマンドのサンプル出力を次に示します。
  
```
Boot Loader Settings
----------
timeout: 30
default: multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
Boot Entries
------
Boot entry ID:   1
Friendly Name:
path: multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
OS Load Options: /fastdetect /debug /debugport=com1:
```

- ブート**ローダーの設定**領域には、boot.ini の [ブートローダー] セクションの各エントリが表示されます。

- ブート**エントリ**領域には、boot.ini の [オペレーティングシステム] セクションの各オペレーティングシステムエントリの詳細が表示されます。

## <a name="examples"></a>例

**Bootcfg/query**コマンドを使用するには、次のようにします。

```
bootcfg /query
bootcfg /query /s srvmain /u maindom\hiropln /p p@ssW23
bootcfg /query /u hiropln /p p@ssW23
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bootcfg コマンド](bootcfg.md)
