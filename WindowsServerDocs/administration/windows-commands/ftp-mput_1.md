---
title: ftp mput
description: Ftp mput コマンドの参照記事。現在のファイル転送の種類を使用してローカルファイルをリモートコンピューターにコピーします。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 980f15e7-7cf1-4813-9946-a8cc4edfb198
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 506a4d9a64f1dd9b4b37088a30926190d7675695
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925804"
---
# <a name="ftp-mput"></a>ftp mput

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

転送の種類を現在のファイルを使用してリモート コンピューターにローカル ファイルをコピーします。

## <a name="syntax"></a>構文

```
mput <localfile>[ ]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<localfile>` | リモート コンピューターにコピーするローカル ファイルを指定します。 |

### <a name="examples"></a>例

現在のファイル転送の種類を使用して*Program1.exe*および*Program2.exe*をリモートコンピューターにコピーするには、次のように入力します。

```
mput Program1.exe Program2.exe
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [ftp ascii コマンド](ftp-ascii.md)

- [ftp バイナリコマンド](ftp-binary.md)

- [追加の FTP ガイダンス](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
