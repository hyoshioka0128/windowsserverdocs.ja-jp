---
title: nslookup set srchlist
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8486266d-22ac-4ce5-aad6-1cd0c08110a2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bbeb09501474ade670147a6021abd2bb25291d71
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80838285"
---
# <a name="nslookup-set-srchlist"></a>nslookup set srchlist

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

既定のドメインネームシステム (DNS) のドメイン名と検索一覧を変更します。

## <a name="syntax"></a>構文
```
Set srchlist=<DomainName>[/...]
```
### <a name="parameters"></a>パラメーター

|    パラメーター    |                                                                                        説明                                                                                        |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  <DomainName>   | 既定の DNS ドメインと検索リストの新しい名前を指定します。 既定のドメイン名の値は、ホスト名に基づいています。 最大6つの名前をスラッシュ (/) で区切って指定できます。 |
| {ヘルプ&#124; ?} |                                                                   **Nslookup**サブコマンドの簡単な概要を表示します。                                                                   |

## <a name="remarks"></a>コメント
- **Set srchlist**コマンドは、**ドメインの設定**コマンドの既定の DNS ドメイン名と検索リストを上書きします。 **[すべて設定]** コマンドを使用して一覧を表示します。
  ## <a name="examples"></a><a name=BKMK_examples></a>例
  次の例では、DNS ドメインを mfg.widgets.com に設定し、検索リストに3つの名前を設定します。
  ```
  set srchlist=mfg.widgets.com/mrp2.widgets.com/widgets.com
  ```
  ## <a name="additional-references"></a>その他の参照情報
  - [コマンドライン構文キー](command-line-syntax-key.md)
  [nslookup set domain](nslookup-set-domain.md)
  [nslookup set all](nslookup-set-all.md)
