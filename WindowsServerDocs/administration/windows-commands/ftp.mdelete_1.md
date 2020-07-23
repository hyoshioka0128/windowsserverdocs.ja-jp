---
title: ftp mdelete
description: Ftp mdelete コマンドの参照記事で、リモートコンピューター上のファイルを削除します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8a80a8f5-e880-40a8-abc9-29a41836844f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0e763a1989ba820e4a4bb19842432368e17f1044
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86957284"
---
# <a name="ftp-mdelete"></a>ftp mdelete

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートコンピューター上のファイルを削除します。

## <a name="syntax"></a>構文
```
mdelete <remotefile>[...]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<remotefile>` | 削除するリモートファイルを指定します。 |

### <a name="examples"></a>例

*a.exe*と*b.exe*のリモートファイルを削除するには、次のように入力します。

```
mdelete a.exe b.exe
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [追加の FTP ガイダンス](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
