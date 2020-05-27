---
title: ftp mdir
description: Ftp mdir コマンドのリファレンストピック。リモートディレクトリ内のファイルとサブディレクトリのディレクトリ一覧を表示します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 90eec45b-558b-4b8d-bbe4-b56d98e1ca70
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b192e6de23105fcc696d8369ce0280167a201e20
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820222"
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

*Dir1*と*dir2*の結合されたディレクトリの一覧を*dirlist .txt*という名前のローカルファイルに保存するには、次のように入力します。

```
mdir dir1 dir2 dirlist.txt
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [追加の FTP ガイダンス](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
