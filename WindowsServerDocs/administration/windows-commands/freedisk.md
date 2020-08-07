---
title: freedisk
description: Freedisk コマンドの参照記事。インストールプロセスを続行する前に、指定された容量のディスク容量が使用可能かどうかを確認します。
ms.topic: article
ms.assetid: 91c15166-5baa-4b80-9e0c-4cd815d00530
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a6c5c09e35f852be9229180ae894356e127f8a03
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87890095"
---
# <a name="freedisk"></a>freedisk

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

インストールプロセスを続行する前に、指定された容量のディスク容量が使用可能かどうかを確認します。

## <a name="syntax"></a>構文

```
freedisk [/s <computer> [/u [<domain>\]<user> [/p [<password>]]]] [/d <drive>] [<value>]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| /s`<computer>` | 名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定値はローカル コンピューターです。 このパラメーターは、コマンドで指定されたすべてのファイルとフォルダーに適用されます。 |
| /u`[<domain>\]<user>` | 指定したユーザー アカウントのアクセス許可を持つ、スクリプトを実行します。 既定値はシステムのアクセス許可です。 |
| /p [<password>] | **/U**で指定したユーザーアカウントのパスワードを指定します。 |
| d`<drive>` | 空き領域の可用性を確認するドライブを指定します。 リモートコンピューターの場合は、を指定する必要があり `<drive>` ます。 |
| `<value>` | 特定の空きディスク領域があるかどうかを確認します。 `<value>`には、bytes、KB、MB、GB、TB、PB、EB、ZB、または YB を指定できます。 |

#### <a name="remarks"></a>Remarks

- **/S、** **/u**、および **/p**コマンドラインオプションは、 **/s**を使用する場合にのみ使用できます。 ユーザーのパスワードを指定するには、 **/u**で **/p**を使用する必要があります。

- 無人インストールの場合は、インストールバッチファイルで**freedisk**を使用して、インストールを続行する前に、前提条件となる空き領域を確認できます。

- バッチファイルで**freedisk**を使用すると、十分な領域がある場合は**0**が返され、十分な領域がない場合は**1**が返されます。

### <a name="examples"></a>例

ドライブ C: に 50 MB 以上の空き領域があるかどうかを確認するには、次のように入力します。

```
freedisk 50mb
```

画面には、次のような出力が表示されます。

```
INFO: The specified 52,428,800 byte(s) of free space is available on current drive.
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
