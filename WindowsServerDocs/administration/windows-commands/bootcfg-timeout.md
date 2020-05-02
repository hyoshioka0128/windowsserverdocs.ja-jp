---
title: bootcfg timeout
description: Bootcfg timeout コマンドのリファレンストピック。オペレーティングシステムのタイムアウト値を変更します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: aa858eac-2bb7-4a27-a9bc-3e4a6eb8b2c6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e10ccab69ca58a6cef260546e965f90eecfc8beb
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82708943"
---
# <a name="bootcfg-timeout"></a>bootcfg timeout

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

オペレーティングシステムのタイムアウト値を変更します。

## <a name="syntax"></a>構文

```
bootcfg /timeout <timeoutvalue> [/s <computer> [/u <domain>\<user> /p <password>]]
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| --------- | ----------- |
| `/timeout <timeoutvalue>` | [ブートローダー] セクションのタイムアウト値を指定します。 は`<timeoutvalue>` 、NTLDR が既定値を読み込む前に、ユーザーがブートローダー画面からオペレーティングシステムを選択する必要がある秒数です。 の`<timeoutvalue>`有効な範囲は0-999 です。 値が0の場合、NTLDR はブートローダー画面を表示せずに、既定のオペレーティングシステムを直ちに開始します。 |
| `/s <computer>` | リモートコンピューターの名前または IP アドレスを指定します (円記号は使用しないでください)。 既定はローカル コンピュータです。 |
| `/u <domain>\<user>`  | または`<user>` `<domain>\<user>`によって指定されたユーザーのアカウントアクセス許可を使用してコマンドを実行します。 既定値は、コマンドを実行しているコンピューターの現在のログオンユーザーのアクセス許可です。 |
| `/p <password>` | 指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

## <a name="examples"></a>例

**Bootcfg/timeout**コマンドを使用するには、次のようにします。

```
bootcfg /timeout 30
bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /timeout 50
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bootcfg コマンド](bootcfg.md)
