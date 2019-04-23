---
title: bitsadmin setpriority
description: Windows コマンド」のトピック**bitsadmin setpriority** -指定したジョブの優先順位を設定します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 90788363-01a2-4d7c-a560-a3eba45b5e9e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 072f22ae8c928d427104062b8cbf0f8f42ac4416
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882213"
---
# <a name="bitsadmin-setpriority"></a>bitsadmin setpriority



指定したジョブの優先順位を設定します。

## <a name="syntax"></a>構文

```
bitsadmin /SetPriority <Job> <Priority>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|Priority|次のいずれかの値です。</br>前景色</br>-高</br>-標準</br>-低|

## <a name="BKMK_examples"></a>例

次の例では、という名前のジョブの優先順位を設定する*myDownloadJob*通常にします。
```
C:\>bitsadmin /SetPriority myDownloadJob NORMAL
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)