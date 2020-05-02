---
title: nslookup root
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9c29edc3-ec49-43f2-bc49-86bf0612d816
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bdfbe40443cf8f2fec2f81608bb93603cd74937f
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723691"
---
# <a name="nslookup-root"></a>nslookup root

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ドメインネームシステム (DNS) のドメイン名空間のルートに対して、既定のサーバーをサーバーに変更します。
## <a name="syntax"></a>構文
```
root 
```
### <a name="parameters"></a>パラメーター

|    パラメーター    |                      [説明]                      |
|-----------------|-------------------------------------------------------|
| {help &#124;?} | **Nslookup**サブコマンドの簡単な概要を表示します。 |

## <a name="remarks"></a>Remarks
- 現時点では、ns.nic.ddn.mil ネームサーバーが使用されています。 このコマンドは、lserver ns.nic.ddn.mil のシノニムです。 ルートサーバーの名前を変更するには、**ルートの設定**コマンドを使用します。
  ## <a name="additional-references"></a>その他のリファレンス
  - [コマンドライン構文キー](command-line-syntax-key.md)
  [nslookup set root](nslookup-set-root.md)
