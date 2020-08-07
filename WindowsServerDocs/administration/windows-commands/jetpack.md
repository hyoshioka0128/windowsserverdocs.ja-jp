---
title: jetpack
description: Windows インターネットネームサービス (WINS) または動的ホスト構成プロトコル (DHCP) データベースを圧縮する、jetpack コマンドのリファレンス記事です。
ms.topic: article
ms.assetid: 82a2b7ef-0db5-4575-a028-8acb0bf6c7ba
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6850c7d00f11278bbc904f7ad7d2e7edaf30d229
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87888194"
---
# <a name="jetpack"></a>jetpack

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows インターネットネームサービス (WINS) または動的ホスト構成プロトコル (DHCP) データベースを圧縮します。 30 MB に近づくときは、WINS データベースを圧縮することをお勧めします。

Jetpack.exe は、次の方法でデータベースを圧縮します。

1. データベース情報を一時データベースファイルにコピーしています。

2. 元のデータベースファイル (WINS または DHCP) を削除しています。

3. 一時データベースファイルの名前を元のファイル名に変更します。

## <a name="syntax"></a>構文

```
jetpack.exe <database_name> <temp_database_name>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ------- | -------- |
| `<database_name>` | 元のデータベースファイルの名前を指定します。 |
| `<temp_database_name>` | jetpack.exe によって作成される一時データベースファイルの名前を指定します。<p>注: この一時ファイルは、コンパクトプロセスが完了すると削除されます。 このコマンドを正常に動作させるには、一時ファイル名が一意であること、およびその名前のファイルが存在しないことを確認する必要があります。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

### <a name="examples"></a>例

WINS データベースを圧縮するには、次のように指定します。この場合、 **.tmp**は一時データベースで、 **wins**は wins データベースです。

```
cd %SYSTEMROOT%\SYSTEM32\WINS
NET STOP WINS
jetpack Wins.mdb Tmp.mdb
NET start WINS
```

DHCP データベースを圧縮するには、 **.tmp**が一時データベースで、 **dhcp**データベースである場合は、次のように入力します。

```
cd %SYSTEMROOT%\SYSTEM32\DHCP
NET STOP DHCPSERVER
jetpack Dhcp.mdb Tmp.mdb
NET start DHCPSERVER
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
