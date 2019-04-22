---
title: bitsadmin geterrorcount
description: Windows コマンド」のトピック**bitsadmin geterrorcount** -指定したジョブの一時的なエラーが発生回数の合計数を取得します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8840ae78-52b0-4c7e-b592-0547359a237e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 91045372931efec0e3189132a275eeacab584de4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818373"
---
# <a name="bitsadmin-geterrorcount"></a>bitsadmin geterrorcount



指定したジョブの一時的なエラーが発生回数の合計数を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetErrorCount <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例

次の例は、という名前のジョブのエラー数の情報を取得*myDownloadJob*します。
```
C:\>bitsadmin /GetErrorCount myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)