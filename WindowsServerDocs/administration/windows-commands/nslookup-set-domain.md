---
title: nslookup set domain
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9d4d28e8-6e88-42cc-801f-94e9d8e051f4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d1af9f30dd2c44111adecb477a6469333f4f7685
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436771"
---
# <a name="nslookup-set-domain"></a>nslookup set domain

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

既定のドメイン ネーム システム (DNS) ドメイン名を指定した名前に変更します。
## <a name="syntax"></a>構文
```
set domain=<DomainName>
```
## <a name="parameters"></a>パラメーター

|    パラメーター    |                                           説明                                           |
|-----------------|-------------------------------------------------------------------------------------------------|
|  <DomainName>   | 既定の DNS ドメイン名の新しい名前を指定します。 既定のドメイン名は、ホスト名です。 |
| {help &#124; ?} |                      簡単な概要を表示します。 **nslookup**サブコマンドします。                      |

## <a name="remarks"></a>注釈
- 既定の DNS ドメイン名がの状態によって検索要求に追加されます、 **defname**と**検索**オプション。 ドメインの DNS 検索リストには、名前に、少なくとも 2 つのコンポーネントがある場合の既定の DNS ドメインの親が含まれています。 たとえば、mfg.widgets.com の場合は、既定の DNS ドメイン検索リストの名前は mfg.widgets.com と widgets.com の両方。 使用、 **srchlist 設定**別のリストを指定するコマンドと**すべて設定**コマンド一覧を表示します。
  ## <a name="additional-references"></a>その他の参照
  [コマンドライン構文のポイント](command-line-syntax-key.md)
  [nslookup 設定 srchlist](nslookup-set-srchlist.md)
  [すべて nslookup 設定](nslookup-set-all.md)
