---
title: ftp put
description: Ftp put コマンドの参照記事。現在のファイル転送の種類を使用してローカルファイルをリモートコンピューターにコピーします。
ms.topic: article
ms.assetid: 95cc1e3f-523d-4374-98b8-16e6c276b2ca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/30/2020
ms.openlocfilehash: e0794c12d7e613f92546903586fe14d23319185a
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87889126"
---
# <a name="ftp-put"></a>ftp put

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

現在のファイル転送の種類を使用して、ローカルファイルをリモートコンピューターにコピーします。

> [!NOTE]
> このコマンドは、 [ftp の send コマンド](ftp-send_1.md)と同じです。

## <a name="syntax"></a>構文

```
put <localfile> [<remotefile>]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<localfile>` | コピーするローカル ファイルを指定します。 |
| `[<remotefile>]` | リモート コンピューターで使用する名前を指定します。 *Remotefile*を指定しない場合、ファイルには*localfile*という名前が付けられます。|

### <a name="examples"></a>例

ローカルファイル*test.txt*をコピーし、リモートコンピューターで*test1.txt*という名前を指定するには、次のように入力します。

```
put test.txt test1.txt
```

ローカルファイル*program.exe*をリモートコンピューターにコピーするには、次のように入力します。

```
put program.exe
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [ftp ascii コマンド](ftp-ascii.md)

- [ftp バイナリコマンド](ftp-binary.md)

- [追加の FTP ガイダンス](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
