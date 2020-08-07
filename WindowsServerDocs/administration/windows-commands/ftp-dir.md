---
title: ftp dir
description: Ftp dir コマンドの参照記事。リモートコンピューター上のディレクトリファイルとサブディレクトリの一覧を表示します。
ms.topic: article
ms.assetid: a29a92a5-7b79-4e6e-95cf-2ccb38bb6fb2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0a4f65cee67ec91b6871649fece4f580684c2e3f
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87889473"
---
# <a name="ftp-dir"></a>ftp dir

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートコンピューター上のディレクトリファイルとサブディレクトリの一覧を表示します。

## <a name="syntax"></a>構文

```
dir [<remotedirectory>] [<localfile>]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ------- | -------- |
| `[<remotedirectory>]` | 一覧を表示するディレクトリを指定します。 ディレクトリが指定されていない場合は、リモートコンピューター上の現在の作業ディレクトリが使用されます。 |
| `[<localfile>]` | ディレクトリの一覧を格納するローカルファイルを指定します。 ローカルファイルが指定されていない場合、結果は画面に表示されます。 |

### <a name="examples"></a>例

リモートコンピューター上の*dir1*のディレクトリ一覧を表示するには、次のように入力します。

```
dir dir1
```

リモートコンピューター上の現在のディレクトリの一覧をローカルファイル*dirlist.txt*に保存するには、次のように入力します。

```
dir . dirlist.txt
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [追加の FTP ガイダンス](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
