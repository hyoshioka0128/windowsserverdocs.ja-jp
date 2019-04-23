---
title: bitsadmin geterror
description: Windows コマンド」のトピック**bitsadmin geterror** -詳細の指定したジョブのエラー情報を取得します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cbe5bca1-d2dd-4ce6-903f-f85de4a2ec6a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 10a3373c0c8f290ff1f5f26ef38531fbc7745890
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889973"
---
# <a name="bitsadmin-geterror"></a>bitsadmin geterror



指定したジョブの詳細なエラー情報を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetError <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例

次の例では、という名前のジョブのエラー情報を取得する*myDownloadJob*します。
```
C:\>bitsadmin /GetError myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)