---
title: nslookup ls
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f15f06fe-67e7-41a9-93b5-192ab14ab380
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ecc419a72599b661865af6283821129a7021938a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373093"
---
# <a name="nslookup-ls"></a>nslookup ls

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ドメインネームシステム (DNS) ドメインの情報を一覧表示します。
## <a name="syntax"></a>構文
```
ls [<Option>] <DNSDomain> [{[>] <FileName>|[>>] <FileName>}]
```
## <a name="parameters"></a>パラメーター

|    パラメーター    |                                                                                                                                                                                                                                                                                                               説明                                                                                                                                                                                                                                                                                                                |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <Option>     | 有効なオプションの一覧を次の表に示します。<br /><br />--t: 指定した種類のすべてのレコードを一覧表示します。 @No__t-0 の説明については、「 **setquerytype** in 追加の参照」を参照してください。<br />--a: DNS ドメイン内のコンピューターのエイリアスを一覧表示します。 このパラメーターは **、-t CNAME**のシノニムです。<br />--d: DNS ドメインのすべてのレコードを一覧表示します。 このパラメーターは、 **-t**のシノニムです。<br />--h: DNS ドメインの CPU とオペレーティングシステムの情報を一覧表示します。 このパラメーターは **、-t HINFO**のシノニムです<br />--s: DNS ドメイン内のコンピューターの既知のサービスを一覧表示します。 このパラメーターは **、-t WKS**のシノニムです。 |
|   <DNSDomain>   |                                                                                                                                                                                                                                                                                         情報を必要とする DNS ドメインを指定します。                                                                                                                                                                                                                                                                                         |
|   <FileName>    |                                                                                                                                                                                                                                 出力を保存するファイル名を指定します。 より大きい (>) 文字と2つのより大きい (> >) 文字を使用すると、通常の方法で出力をリダイレクトできます。                                                                                                                                                                                                                                  |
| {ヘルプ&#124; ?} |                                                                                                                                                                                                                                                                                          **Nslookup**サブコマンドの簡単な概要を表示します。                                                                                                                                                                                                                                                                                           |

## <a name="remarks"></a>コメント
- 既定の出力には、コンピューター名とその IP アドレスが含まれています。 出力がファイルに送られると、サーバーから受信した50レコードごとにハッシュマークが出力されます。
  ## <a name="additional-references"></a>その他の参照情報
  [コマンドライン構文のキー](command-line-syntax-key.md)
  [nslookup set querytype](nslookup-set-querytype.md)
