---
title: bitsadmin getcustomheaders
description: Windows コマンド」のトピック**bitsadmin getcustomheaders** -ジョブからカスタムの HTTP ヘッダーを取得します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1f0d38d3-e865-4474-81e8-773d65c3d1cc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2f5959541f0e3190e26bbb298a9cd7c63ab32cae
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812093"
---
# <a name="bitsadmin-getcustomheaders"></a>bitsadmin getcustomheaders



ジョブからカスタムの HTTP ヘッダーを取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetCustomHeaders <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例

次の例では、カスタム ヘッダーを取得という名前のジョブ*myDownloadJob*します。
```
C:\>bitsadmin /GetCustomHeaders myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)