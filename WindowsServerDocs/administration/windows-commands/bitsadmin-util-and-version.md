---
title: bitsadmin util とバージョン
description: Windows コマンド」のトピック**bitsadmin util とバージョン**-BITS サービスのバージョンが表示されます。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98f17328-dfbd-4cbb-93c1-b8d424bc3f0a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2e768ec5ae43fc17c480b9deede698cca01c6291
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882873"
---
# <a name="bitsadmin-util-and-version"></a>bitsadmin util とバージョン

BITS サービス (2.0 など) のバージョンが表示されます。

**1.5 およびそれ以前の BITSAdmin**: サポートされません。

## <a name="syntax"></a>構文

```
bitsadmin /Util /Version [/Verbose]
```

## <a name="remarks"></a>注釈

**Verbose**スイッチは、次を実行します。
-   関連する DLL をビットごとのファイルのバージョンを表示します。
-   BITS サービスを開始できることを確認します。
-   グループ ポリシーのビット値 (Windows Vista のみ) が表示されます。

## <a name="BKMK_examples"></a>例

次の例の BITS サービス バージョン。
```
C:\>bitsadmin /Util /Version
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)