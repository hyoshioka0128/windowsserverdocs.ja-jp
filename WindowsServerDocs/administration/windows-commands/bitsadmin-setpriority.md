---
title: bitsadmin setpriority
description: Bitsadmin setpriority の Windows コマンドに関するトピックでは、指定されたジョブの優先順位を設定します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 90788363-01a2-4d7c-a560-a3eba45b5e9e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7d007c62402a3d70910e1c79fab5c406295a63a5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849215"
---
# <a name="bitsadmin-setpriority"></a>bitsadmin setpriority

指定されたジョブの優先順位を設定します。

## <a name="syntax"></a>構文

```
bitsadmin /SetPriority <Job> <Priority>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|優先順位|次のいずれかの値です。</br>-前景</br>-高</br>-通常</br>-低|

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、 *Mydownloadjob*という名前のジョブの優先順位を normal に設定します。
```
C:\>bitsadmin /SetPriority myDownloadJob NORMAL
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)