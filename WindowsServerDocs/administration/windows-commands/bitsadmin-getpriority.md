---
title: bitsadmin getpriority
description: Windows コマンド」のトピック**bitsadmin getpriority** -指定したジョブの優先順位を取得します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 6be2461ed87b75144367b1bd74376381e4674b66
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841443"
---
# <a name="bitsadmin-getpriority"></a>bitsadmin getpriority

指定したジョブの優先順位を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetPriority <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="remarks"></a>注釈

優先順位があるか、**フォア グラウンド**、**高**、**標準**、**低**、または**不明な**します。

## <a name="BKMK_examples"></a>例

次の例では、という名前のジョブの優先順位を取得する*myDownloadJob*します。
```
C:\>bitsadmin /GetPriority myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)
