---
title: nslookup set srchlist
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: fb93a9f7cf969161536e88bec929b7e6ba0f0e5d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372771"
---
# <a name="nslookup-set-srchlist"></a>nslookup set srchlist

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

既定のドメインネームシステム (DNS) のドメイン名と検索一覧を変更します。

## <a name="syntax"></a>構文
```
Set srchlist=<DomainName>[/...]
```
## <a name="parameters"></a>パラメーター

|    パラメーター    |                                                                                        説明                                                                                        |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  <DomainName>   | 既定の DNS ドメインと検索リストの新しい名前を指定します。 既定のドメイン名の値は、ホスト名に基づいています。 最大6つの名前をスラッシュ (/) で区切って指定できます。 |
| {ヘルプ&#124; ?} |                                                                   **Nslookup**サブコマンドの簡単な概要を表示します。                                                                   |

## <a name="remarks"></a>コメント
- **Set srchlist**コマンドは、**ドメインの設定**コマンドの既定の DNS ドメイン名と検索リストを上書きします。 **[すべて設定]** コマンドを使用して一覧を表示します。
  ## <a name="BKMK_examples"></a>例
  次の例では、DNS ドメインを mfg.widgets.com に設定し、検索リストに3つの名前を設定します。
  ```
  set srchlist=mfg.widgets.com/mrp2.widgets.com/widgets.com
  ```
  ## <a name="additional-references"></a>その他の参照情報
  [コマンドライン構文のキー](command-line-syntax-key.md)
  [nslookup set domain](nslookup-set-domain.md)
  [nslookup set all](nslookup-set-all.md)
