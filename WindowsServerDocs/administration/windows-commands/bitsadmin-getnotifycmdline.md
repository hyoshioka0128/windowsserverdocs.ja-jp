---
title: bitsadmin getnotifycmdline
description: '**Bitsadmin getnotifycmdline**の Windows コマンドトピックでは、ジョブがデータの転送を終了したときに実行されるコマンドラインコマンドを取得します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 90fa33e6-aca5-4a23-82bd-19a9f13f8416
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b91d2c71ad4bedaac65e23041ca78a70ade99977
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381490"
---
# <a name="bitsadmin-getnotifycmdline"></a>bitsadmin getnotifycmdline

ジョブがデータの転送を終了したときに実行するコマンドラインコマンドを取得します。

**BITS 1.2 以前**: サポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /GetNotifyCmdLine <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブが完了すると、サービスによって使用されるコマンドラインコマンドを取得します。
```
C:\>bitsadmin /GetNotifyCmdLine myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)