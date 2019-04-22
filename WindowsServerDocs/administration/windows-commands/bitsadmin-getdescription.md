---
title: bitsadmin getdescription
description: Windows コマンド」のトピック**bitsadmin getdescription** -指定したジョブの説明を取得します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f3974603-ebbe-4d31-8217-040fe2d90c85
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ee20dd808cdbc8b76f44b7b14c9fd65b313a74e5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813133"
---
# <a name="bitsadmin-getdescription"></a>bitsadmin getdescription



指定したジョブの説明を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetDescription <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例

次の例では、という名前のジョブの説明を取得する*myDownloadJob*します。
```
C:\>bitsadmin /GetDescription myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)