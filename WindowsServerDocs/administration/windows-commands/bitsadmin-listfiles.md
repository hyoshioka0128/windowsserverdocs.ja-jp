---
title: bitsadmin listfiles
description: Windows コマンド」のトピック**bitsadmin/listfiles という**-指定したジョブ内のファイルを一覧表示されます。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ad0d1eaa-3bd8-45e5-8f72-4da7366f0d59
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4f0f86a7e176c601c51dbdf403baf51f70e53dc4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852973"
---
# <a name="bitsadmin-listfiles"></a>bitsadmin listfiles



指定したジョブ内のファイルを一覧表示します。

## <a name="syntax"></a>構文

```
bitsadmin /ListFiles <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例

次の例では、という名前のジョブのファイルの一覧を取得する*myDownloadJob*します。
```
C:\>bitsadmin /GetNotifyFlags myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)