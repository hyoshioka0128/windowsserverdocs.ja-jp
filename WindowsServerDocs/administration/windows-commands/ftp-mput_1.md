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
ms.openlocfilehash: ca0b72fce2ce9408fa04e948c8116a0b9e153268
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86957644"
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

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [ftp ascii コマンド](ftp-ascii.md)

- [ftp バイナリコマンド](ftp-binary.md)

- [追加の FTP ガイダンス](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
