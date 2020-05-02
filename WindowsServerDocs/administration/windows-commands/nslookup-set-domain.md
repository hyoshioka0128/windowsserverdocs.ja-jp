---
title: nslookup set domain
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9d4d28e8-6e88-42cc-801f-94e9d8e051f4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f6ee52cd5ad35dcfc6da1cd3885f66124338d62f
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723615"
---
# <a name="nslookup-set-domain"></a>nslookup set domain

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

既定のドメインネームシステム (DNS) のドメイン名を、指定された名前に変更します。
## <a name="syntax"></a>構文
```
set domain=<DomainName>
```
### <a name="parameters"></a>パラメーター

|    パラメーター    |                                           [説明]                                           |
|-----------------|-------------------------------------------------------------------------------------------------|
|  <DomainName>   | 既定の DNS ドメイン名の新しい名前を指定します。 既定のドメイン名は、ホスト名です。 |
| {help &#124;?} |                      **Nslookup**サブコマンドの簡単な概要を表示します。                      |

## <a name="remarks"></a>Remarks
- 既定の DNS ドメイン名は、 **defname**と**検索**オプションの状態に応じて、参照要求に追加されます。 DNS ドメインの検索一覧には、その名前に少なくとも2つのコンポーネントがある場合の既定の DNS ドメインの親が含まれます。 たとえば、既定の DNS ドメインが mfg.widgets.com の場合、検索リストには mfg.widgets.com と widgets.com の両方の名前が付けられます。 **Set srchlist**コマンドを使用して別のリストを指定し、 **set all**コマンドを使用して一覧を表示します。
  ## <a name="additional-references"></a>その他のリファレンス
  - [コマンドライン構文のキー](command-line-syntax-key.md)
  [nslookup set srchlist](nslookup-set-srchlist.md)
  [nslookup set all](nslookup-set-all.md)
