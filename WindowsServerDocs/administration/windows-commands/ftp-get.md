---
title: ftp get
description: Ftp get コマンドの参照記事。現在のファイル転送の種類を使用してリモートファイルをローカルコンピューターにコピーします。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d70355c4-58ef-43e0-916b-c7ecf77e6ee4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: de084813ee837ecea2f0871589218d3262b40bba
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925925"
---
# <a name="ftp-get"></a>ftp get

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

現在のファイル転送の種類を使用して、リモートファイルをローカルコンピューターにコピーします。

> [!NOTE]
> このコマンドは、 [ftp の recv コマンド](ftp-recv.md)と同じです。

## <a name="syntax"></a>構文

```
get <remotefile> [<localfile>]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<remotefile>` | コピーするリモートファイルを指定します。 |
| `[<localfile>]` | ローカルコンピューターで使用するファイルの名前を指定します。 *Localfile*が指定されていない場合、ファイルには*remotefile*の名前が付けられます。 |

### <a name="examples"></a>例

現在のファイル転送を使用して*test.txt*をローカルコンピューターにコピーするには、次のように入力します。

```
get test.txt
```

現在のファイル転送を使用して*test1.txt*としてローカルコンピューターに*test.txt*をコピーするには、次のように入力します。

```
get test.txt test1.txt
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [ftp の recv コマンド](ftp-recv.md)

- [ftp ascii コマンド](ftp-ascii.md)

- [ftp バイナリコマンド](ftp-binary.md)

- [追加の FTP ガイダンス](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
