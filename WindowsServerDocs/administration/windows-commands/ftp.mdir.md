---
title: ftp mdir
description: Ftp mdir コマンドの参照記事。リモートディレクトリ内のファイルとサブディレクトリのディレクトリ一覧を表示します。
ms.topic: article
ms.assetid: 90eec45b-558b-4b8d-bbe4-b56d98e1ca70
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ddd4a5adb282464d2b5a202ea8ed2838be7a4676
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87888724"
---
# <a name="ftp-mdir"></a>ftp mdir

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートディレクトリ内のファイルとサブディレクトリのディレクトリ一覧を表示します。

## <a name="syntax"></a>構文

```
mdir <remotefile>[...] <localfile>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<remotefile>` | 一覧を表示するディレクトリまたはファイルを指定します。 複数の*remotefiles*を指定できます。 リモートコンピューター上の現在の作業ディレクトリを使用するには、ハイフン (-) を入力します。 |
| `<localfile>` | 一覧を格納するローカルファイルを指定します。 このパラメーターは必須です。 画面に一覧を表示するには、ハイフン (-) を入力します。 |

### <a name="examples"></a>例

*Dir1*と*dir2*のディレクトリ一覧を画面に表示するには、次のように入力します。

```
mdir dir1 dir2 -
```

*Dir1*と*dir2*の結合されたディレクトリの一覧を*dirlist.txt*という名前のローカルファイルに保存するには、次のように入力します。

```
mdir dir1 dir2 dirlist.txt
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [追加の FTP ガイダンス](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
