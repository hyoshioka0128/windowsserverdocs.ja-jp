---
title: nslookup set srchlist
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8486266d-22ac-4ce5-aad6-1cd0c08110a2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 39b28e7d43df2427caae46d323cd30f03b6b484c
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436575"
---
# <a name="nslookup-set-srchlist"></a>nslookup set srchlist

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

既定のドメイン ネーム システム (DNS) ドメイン名と検索一覧を変更します。

## <a name="syntax"></a>構文
```
Set srchlist=<DomainName>[/...]
```
## <a name="parameters"></a>パラメーター

|    パラメーター    |                                                                                        説明                                                                                        |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  <DomainName>   | 既定の DNS ドメインと検索一覧の新しい名前を指定します。 既定のドメイン名の値は、ホスト名に基づきます。 スラッシュ (/) で区切られた 6 つの名の最大数を指定できます。 |
| {help &#124; ?} |                                                                   簡単な概要を表示します。 **nslookup**サブコマンドします。                                                                   |

## <a name="remarks"></a>注釈
- **設定 srchlist**コマンドの既定 DNS ドメイン名と検索リストよりも優先されます、**セット ドメイン**コマンド。 使用して、**すべて設定**コマンド一覧を表示します。
  ## <a name="BKMK_examples"></a>例
  次の例では、mfg.widgets.com と 3 つの名前を検索リストに DNS ドメインを設定します。
  ```
  set srchlist=mfg.widgets.com/mrp2.widgets.com/widgets.com
  ```
  ## <a name="additional-references"></a>その他の参照
  [コマンドライン構文のポイント](command-line-syntax-key.md)
  [nslookup でドメインを設定](nslookup-set-domain.md)
  [すべて nslookup 設定](nslookup-set-all.md)
