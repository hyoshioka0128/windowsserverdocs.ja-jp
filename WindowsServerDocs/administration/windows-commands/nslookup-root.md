---
title: nslookup root
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9c29edc3-ec49-43f2-bc49-86bf0612d816
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3eb3375df3a109685fc8dc5d23f0c5008339d09e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373390"
---
# <a name="nslookup-root"></a>nslookup root

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ドメインネームシステム (DNS) のドメイン名空間のルートに対して、既定のサーバーをサーバーに変更します。
## <a name="syntax"></a>構文
```
root 
```
## <a name="parameters"></a>パラメーター

|    パラメーター    |                      説明                      |
|-----------------|-------------------------------------------------------|
| {ヘルプ&#124; ?} | **Nslookup**サブコマンドの簡単な概要を表示します。 |

## <a name="remarks"></a>コメント
- 現時点では、ns.nic.ddn.mil ネームサーバーが使用されています。 このコマンドは、lserver ns.nic.ddn.mil のシノニムです。 ルートサーバーの名前を変更するには、**ルートの設定**コマンドを使用します。
  ## <a name="additional-references"></a>その他の参照情報
  [コマンドライン構文のキー](command-line-syntax-key.md)
  [nslookup set root](nslookup-set-root.md)
