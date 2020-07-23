---
title: ftp mls
description: Ftp mls コマンドの参照記事。リモートディレクトリにあるファイルとサブディレクトリの省略形の一覧を表示します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4738fd49-0e80-4bdf-a773-0f973db3a710
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2f3d5c6b595cf6f8261a4af742cef60d0c9e3abd
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86957654"
---
# <a name="ftp-mls"></a>ftp mls

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモート ディレクトリにファイルとサブディレクトリの省略版リストを表示します。

## <a name="syntax"></a>構文

```
mls <remotefile>[ ] <localfile>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<remotefile>` | 一覧を表示するファイルを指定します。 *Remotefiles*を指定する場合は、ハイフンを使用してリモートコンピューター上の現在の作業ディレクトリを表します。 |
| `<localfile>` | 一覧を格納するローカル ファイルを指定します。 *Localfile*を指定する場合は、ハイフンを使用して画面に一覧表示します。 |

### <a name="examples"></a>例

*Dir1*と*dir2*のファイルとサブディレクトリの省略された一覧を表示するには、次のように入力します。

```
mls dir1 dir2 -
```

*Dir1*と*dir2*のファイルとサブディレクトリの省略リストをローカルファイル*dirlist.txt*に保存するには、次のように入力します。

```
mls dir1 dir2 dirlist.txt
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [追加の FTP ガイダンス](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
