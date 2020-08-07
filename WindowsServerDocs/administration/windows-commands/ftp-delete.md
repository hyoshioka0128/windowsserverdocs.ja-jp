---
title: ftp delete
description: Ftp delete コマンドの参照記事。リモートコンピューター上のファイルを削除します。
ms.topic: article
ms.assetid: 067c45f3-e4e8-4450-b8b6-836994f6adfe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 315a73f0ebfbefdf4a7033f42c2cad02e2ab77bc
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87889521"
---
# <a name="ftp-delete"></a>ftp delete

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートコンピューター上のファイルを削除します。

## <a name="syntax"></a>構文

```
delete <remotefile>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<remotefile>` | 削除するファイルを指定します。 |

### <a name="examples"></a>例

リモートコンピューター上の*test.txt*ファイルを削除するには、次のように入力します。

```
delete test.txt
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [追加の FTP ガイダンス](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
