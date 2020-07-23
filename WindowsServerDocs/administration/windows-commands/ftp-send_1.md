---
title: ftp send
description: Ftp 送信コマンドの参照記事。現在のファイル転送の種類を使用してローカルファイルをリモートコンピューターにコピーします。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 000aa80a-60a0-4b51-815f-3237a4f3e0f4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5a734e20e2650a064b6dc293bae96a013b6e1f22
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86957404"
---
# <a name="ftp-send"></a>ftp send

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

現在のファイル転送の種類を使用して、ローカルファイルをリモートコンピューターにコピーします。

> [!NOTE]
> このコマンドは、 [ftp put コマンド](ftp-put.md)と同じです。

## <a name="syntax"></a>構文

```
send <localfile> [<remotefile>]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<localfile>` | コピーするローカル ファイルを指定します。 |
| `<remotefile>` | リモート コンピューターで使用する名前を指定します。 *Remotefile*を指定しない場合、ファイルによって*localfile*名が取得されます。 |

### <a name="examples"></a>例

ローカルファイル*test.txt*をコピーし、リモートコンピューターで*test1.txt*という名前を指定するには、次のように入力します。

```
send test.txt test1.txt
```

ローカルファイル*program.exe*をリモートコンピューターにコピーするには、次のように入力します。

```
send program.exe
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [追加の FTP ガイダンス](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
