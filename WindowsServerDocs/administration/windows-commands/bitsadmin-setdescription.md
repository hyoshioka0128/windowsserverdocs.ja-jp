---
title: bitsadmin setdescription
description: Windows コマンド」のトピック**bitsadmin setdescription** -指定したジョブの説明を設定します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1e46a5dd-4637-4a2e-b88f-d3f85b177db8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8e3323c20eebc8ba633ccfd478daa0753e506f46
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830753"
---
# <a name="bitsadmin-setdescription"></a>bitsadmin setdescription



指定したジョブの説明を設定します。

## <a name="syntax"></a>構文

```
bitsadmin /SetDescription <Job> <Description>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|説明|ジョブの記述に使用するテキスト。|

## <a name="BKMK_examples"></a>例

次の例では、という名前のジョブの説明を取得する*myDownloadJob*します。
```
C:\>bitsadmin /SetDescription myDownloadJob "Music Downloads"
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)