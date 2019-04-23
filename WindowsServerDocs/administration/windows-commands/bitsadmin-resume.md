---
title: bitsadmin resume
description: Windows コマンド」のトピック**bitsadmin 再開**-転送キューに新しいまたは中断されたジョブがアクティブになります。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c7540a9-a11a-4910-923a-2a2a61cbf11d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 76027ac927f8a9bb2558e3ce6d75e4f6692e56e7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842033"
---
# <a name="bitsadmin-resume"></a>bitsadmin resume



転送キューに新しいまたは中断されたジョブを有効にします。

## <a name="syntax"></a>構文

```
bitsadmin /Resume <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例

次の例では、という名前のジョブを再開します。 *myDownloadJob*します。
```
C:\>bitsadmin /Resume myDownloadJob
```
その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)