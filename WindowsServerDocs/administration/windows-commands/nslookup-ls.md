---
title: nslookup ls
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 6a11867ff2ec69b1ef938149ac485ff8827b58de
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436921"
---
# <a name="nslookup-ls"></a>nslookup ls

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ドメイン ネーム システム (DNS) ドメインの情報を一覧表示します。
## <a name="syntax"></a>構文
```
ls [<Option>] <DNSDomain> [{[>] <FileName>|[>>] <FileName>}]
```
## <a name="parameters"></a>パラメーター

|    パラメーター    |                                                                                                                                                                                                                                                                                                               説明                                                                                                                                                                                                                                                                                                                |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <Option>     | 次の表には、有効なオプションが一覧表示します。<br /><br />--t:、指定した型のすべてのレコードが一覧表示します。 説明については<querytype>を参照してください**setquerytype**で参照を追加します。<br />--a: DNS ドメイン内のコンピューターのエイリアスを一覧表示します。 このパラメーターのシノニムは、 **-t CNAME**<br />--d:、DNS ドメインのすべてのレコードが一覧表示します。 このパラメーターのシノニムは、 **-t ANY**<br />--: %m: DNS ドメインの CPU およびオペレーティング システムの情報を一覧表示します。 このパラメーターのシノニムは、 **-t HINFO**<br />--%s: DNS ドメイン内のコンピューターの既知のサービスを一覧表示します。 このパラメーターのシノニムは、 **-t WKS**します。 |
|   <DNSDomain>   |                                                                                                                                                                                                                                                                                         情報の対象となる DNS ドメインを指定します。                                                                                                                                                                                                                                                                                         |
|   <FileName>    |                                                                                                                                                                                                                                 出力の保存先となるファイル名を指定します。 大なり (>) と二重を使用するより大きい (>>) 通常の方法で出力にリダイレクトする文字。                                                                                                                                                                                                                                  |
| {help &#124; ?} |                                                                                                                                                                                                                                                                                          簡単な概要を表示します。 **nslookup**サブコマンドします。                                                                                                                                                                                                                                                                                           |

## <a name="remarks"></a>注釈
- 既定の出力を含むコンピューターの名前とその IP アドレス。 出力ファイルに、ハッシュ マークは、サーバーから受信した 50 レコードごとに出力されます。
  ## <a name="additional-references"></a>その他の参照
  [コマンドライン構文のポイント](command-line-syntax-key.md)
  [nslookup querytype を設定します。](nslookup-set-querytype.md)
