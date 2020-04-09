---
title: nslookup set root
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8ad5393c-d4fd-4594-8187-576b1dcde60a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ea2c34bbf7c9323c948d57ac2a838c22aea1008e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80838315"
---
# <a name="nslookup-set-root"></a>nslookup set root

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

クエリに使用するルートサーバーの名前を変更します。
## <a name="syntax"></a>構文
```
set root=<RootServer>
```
### <a name="parameters"></a>パラメーター

|    パラメーター    |                                   説明                                    |
|-----------------|----------------------------------------------------------------------------------|
|  <RootServer>   | ルートサーバーの新しい名前を指定します。 既定値は ns.nic.ddn.mil です。 |
| {ヘルプ&#124; ?} |              **Nslookup**サブコマンドの簡単な概要を表示します。               |

## <a name="remarks"></a>コメント
- **Set root**サブコマンドは、**ルート**サブコマンドに影響します。
  ## <a name="additional-references"></a>その他の参照情報
  - [コマンドライン構文のキー](command-line-syntax-key.md)
  [nslookup root](nslookup-root.md)
