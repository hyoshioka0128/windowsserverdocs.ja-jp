---
title: ftp put
description: FTP put の Windows コマンドに関するトピック
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 95cc1e3f-523d-4374-98b8-16e6c276b2ca vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/30/2020
ms.openlocfilehash: 019a81364dbedb443a3a23d5c5a6f8db1496d83d
ms.sourcegitcommit: 479ad84a0d6c7c7b8308122b8bac8308cb36fe9b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/30/2020
ms.locfileid: "80391725"
---
# <a name="ftp-put"></a>ftp: put

> 適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

現在のファイル転送の種類を使用して、ローカルファイルをリモートコンピューターにコピーします。
## <a name="syntax"></a>構文
```
put <LocalFile> [<remoteFile>]
```
### <a name="parameters"></a>パラメーター

|    パラメーター     |                    説明                    |
|------------------|---------------------------------------------------|
|   `<LocalFile>`  |         コピーするローカル ファイルを指定します。         |
| `[<remoteFile>]` | リモート コンピューターで使用する名前を指定します。 |

## <a name="remarks"></a>コメント
- **配置** コマンドと同じ、 **送信** コマンドです。
- *Remotefile*が指定されていない場合、ファイルには*LocalFile*という名前が付けられます。
  ## <a name="examples"></a><a name="BKMK_Examples"></a>例
  ローカルファイル**test.txt**をコピーし、リモートコンピューター上に「 **test1** 」という名前を指定します。
  ```
  put test.txt test1.txt
  ```
  ローカルファイルの**setup.exe**をリモートコンピューターにコピーします。
  ```
  put program.exe
  ```
  ## <a name="additional-references"></a>その他の参照情報
- [ftp: ascii](ftp-ascii.md)
- [ftp: バイナリ](ftp-binary.md)
- [コマンド ライン構文の記号](command-line-syntax-key.md)
