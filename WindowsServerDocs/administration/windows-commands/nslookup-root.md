---
title: nslookup root
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9c29edc3-ec49-43f2-bc49-86bf0612d816
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d11179ff3cd22acd9df67261e7ab752aa159201a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80838645"
---
# <a name="nslookup-root"></a>nslookup root

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ドメインネームシステム (DNS) のドメイン名空間のルートに対して、既定のサーバーをサーバーに変更します。
## <a name="syntax"></a>構文
```
root 
```
### <a name="parameters"></a>パラメーター

|    パラメーター    |                      説明                      |
|-----------------|-------------------------------------------------------|
| {ヘルプ&#124; ?} | **Nslookup**サブコマンドの簡単な概要を表示します。 |

## <a name="remarks"></a>コメント
- 現時点では、ns.nic.ddn.mil ネームサーバーが使用されています。 このコマンドは、lserver ns.nic.ddn.mil のシノニムです。 ルートサーバーの名前を変更するには、**ルートの設定**コマンドを使用します。
  ## <a name="additional-references"></a>その他の参照情報
  - [コマンドライン構文のキー](command-line-syntax-key.md)
  [nslookup](nslookup-set-root.md)によるルートの設定
