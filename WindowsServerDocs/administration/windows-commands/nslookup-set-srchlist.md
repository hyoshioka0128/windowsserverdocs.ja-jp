---
title: nslookup set srchlist
description: Nslookup set srchlist コマンドのリファレンストピック。これにより、既定のドメインネームシステム (DNS) のドメイン名と検索リストが変更されます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8486266d-22ac-4ce5-aad6-1cd0c08110a2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ed9bbce1910324c4cae5da4228a6d3d1f269d050
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721402"
---
# <a name="nslookup-set-srchlist"></a>nslookup set srchlist

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

既定のドメインネームシステム (DNS) のドメイン名と検索一覧を変更します。 このコマンドは、 [nslookup set domain](nslookup-set-domain.md)コマンドの既定の DNS ドメイン名と検索リストを上書きします。

## <a name="syntax"></a>構文

```
set srchlist=<domainname>[/...]
```

### <a name="parameters"></a>パラメーター

| パラメーター | Description |
| --------- | ----------- |
| `<domainname>` | 既定の DNS ドメインと検索リストの新しい名前を指定します。 既定のドメイン名の値は、ホスト名に基づいています。 最大6つの名前をスラッシュ (/) で区切って指定できます。 |
| /? | コマンド プロンプトにヘルプを表示します。 |
| /help | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>注釈

- [Nslookup set all](nslookup-set-all.md)コマンドを使用して一覧を表示します。

### <a name="examples"></a>例

DNS ドメインを*mfg.widgets.com*に設定し、検索リストを3つの名前に設定するには、次のようにします。

```
set srchlist=mfg.widgets.com/mrp2.widgets.com/widgets.com
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [nslookup set domain](nslookup-set-domain.md)

- [nslookup set all](nslookup-set-all.md)
