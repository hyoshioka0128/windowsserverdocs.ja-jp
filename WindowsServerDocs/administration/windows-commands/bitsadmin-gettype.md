---
title: bitsadmin gettype
description: Windows コマンド」のトピック**bitsadmin gettype** -指定したジョブのジョブの種類を取得します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bec16f04-3e95-4587-889e-3de6ad03c9c8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ff0118f14acbf4e9f37c02e660bd9c7f6e8d0f70
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879433"
---
# <a name="bitsadmin-gettype"></a>bitsadmin gettype



指定したジョブのジョブの種類を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetType <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="remarks"></a>注釈

型は、ダウンロード、アップロード/応答、または UNKNOWN をアップロードします。

## <a name="BKMK_examples"></a>例

次の例では、という名前のジョブのジョブの種類を取得する*myDownloadJob*します。
```
C:\>bitsadmin /GetType myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)