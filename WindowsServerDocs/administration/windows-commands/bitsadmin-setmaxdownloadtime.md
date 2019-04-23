---
title: bitsadmin setmaxdownloadtime
description: Windows コマンド」のトピック**bitsadmin setmaxdownloadtime** -ダウンロード タイムアウトを秒単位で設定します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 16b96cf1-5738-415c-9b9d-c4ea8d5e4fec
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f13b44429bec2718af1a648f273fead18d4e9e08
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830993"
---
# <a name="bitsadmin-setmaxdownloadtime"></a>bitsadmin setmaxdownloadtime



ダウンロード タイムアウトを秒単位で設定します。

## <a name="syntax"></a>構文

```
bitsadmin /SetMaxDownloadTime <Job> <Timeout>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|Timeout|タイムアウト (秒)|

## <a name="remarks"></a>注釈

-   なし

## <a name="BKMK_examples"></a>例

次の例では、という名前のジョブのタイムアウトを設定する*myDownloadJob*を 10 秒にします。
```
C:\>bitsadmin /SetMaxDownloadTime myDownloadJob 10
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)