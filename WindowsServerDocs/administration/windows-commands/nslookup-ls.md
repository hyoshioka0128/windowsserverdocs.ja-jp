---
title: nslookup ls
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f15f06fe-67e7-41a9-93b5-192ab14ab380
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8357208406c0fca5d68da419baa2092d94fa9ec9
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723702"
---
# <a name="nslookup-ls"></a>nslookup ls

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ドメインネームシステム (DNS) ドメインの情報を一覧表示します。
## <a name="syntax"></a>構文
```
ls [<Option>] <DNSDomain> [{[>] <FileName>|[>>] <FileName>}]
```
### <a name="parameters"></a>パラメーター

|    パラメーター    |                                                                                                                                                                                                                                                                                                               [説明]                                                                                                                                                                                                                                                                                                                |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <Option>     | 有効なオプションの一覧を次の表に示します。<p>--t: 指定した種類のすべてのレコードを一覧表示します。 の<querytype>詳細については、「 **setquerytype** in 追加の参照」を参照してください。<br />--a: DNS ドメイン内のコンピューターのエイリアスを一覧表示します。 このパラメーターは **、-t CNAME**のシノニムです。<br />--d: DNS ドメインのすべてのレコードを一覧表示します。 このパラメーターは、 **-t**のシノニムです。<br />--h: DNS ドメインの CPU とオペレーティングシステムの情報を一覧表示します。 このパラメーターは **、-t HINFO**のシノニムです<br />--s: DNS ドメイン内のコンピューターの既知のサービスを一覧表示します。 このパラメーターは **、-t WKS**のシノニムです。 |
|   <DNSDomain>   |                                                                                                                                                                                                                                                                                         情報を必要とする DNS ドメインを指定します。                                                                                                                                                                                                                                                                                         |
|   <FileName>    |                                                                                                                                                                                                                                 出力を保存するファイル名を指定します。 大なり (>) と2文字以上 (>>) の文字を使用すると、通常の方法で出力をリダイレクトできます。                                                                                                                                                                                                                                  |
| {help &#124;?} |                                                                                                                                                                                                                                                                                          **Nslookup**サブコマンドの簡単な概要を表示します。                                                                                                                                                                                                                                                                                           |

## <a name="remarks"></a>Remarks
- 既定の出力には、コンピューター名とその IP アドレスが含まれています。 出力がファイルに送られると、サーバーから受信した50レコードごとにハッシュマークが出力されます。
  ## <a name="additional-references"></a>その他のリファレンス
  - [コマンドライン構文のキー](command-line-syntax-key.md)
  [nslookup set querytype](nslookup-set-querytype.md)
