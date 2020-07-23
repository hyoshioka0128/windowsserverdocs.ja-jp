---
title: ftp lcd
description: Ftp lcd コマンドの参照記事。ローカルコンピューター上の作業ディレクトリを変更します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 60a25808-6abb-408b-8373-0bbdcd0994b4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d98b300de74ec537dedd3f43ccc2404c7350ac0c
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86957784"
---
# <a name="ftp-lcd"></a>ftp lcd

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ローカルコンピューター上の作業ディレクトリを変更します。 既定では、作業ディレクトリは、 **ftp**コマンドが開始されたディレクトリです。

## <a name="syntax"></a>構文

```
lcd [<directory>]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `[<directory>]` | 変更するローカルコンピューター上のディレクトリを指定します。 *Directory*が指定されていない場合は、現在の作業ディレクトリが既定のディレクトリに変更されます。 |

### <a name="examples"></a>例

ローカルコンピューター上の作業ディレクトリを*c:\ dir1*に変更するには、次のように入力します。

```
lcd c:\dir1
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [追加の FTP ガイダンス](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
