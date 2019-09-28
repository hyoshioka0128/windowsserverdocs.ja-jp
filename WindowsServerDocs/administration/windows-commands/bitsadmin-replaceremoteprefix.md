---
title: bitsadmin replaceremoteprefix
description: '**Bitsadmin replaceremoteprefix**の Windows コマンドに関するトピックでは、リモート URL が*oldprefix*で始まるジョブ内のすべてのファイルが、 *newprefix*を使用するように変更されています。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d0e0abb1-bdb4-4c74-abbc-16c809f5fd81
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ee896a337b571487797967d3ce0bf1f1b17e7507
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380798"
---
# <a name="bitsadmin-replaceremoteprefix"></a>bitsadmin replaceremoteprefix

リモート URL が*oldprefix*で始まるジョブ内のすべてのファイルは、 *newprefix*を使用するように変更されます。

## <a name="syntax"></a>構文

```
bitsadmin /ReplaceRemotePrefix <Job> <OldPrefix> <NewPrefix
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|OldPrefix|既存の URL プレフィックス|
|NewPrefix|新しい URL プレフィックス|

## <a name="examples"></a>使用例

次の例では、 *Mydownloadjob*という名前のジョブ内のすべてのファイルを変更します。この場合、リモート URL は *http://stageserver* から *http://prodserver* で始まります。

```
C:\>bitsadmin /ReplaceRemotePrefix myDownloadJob http://stageserver http://prodserver
```

## <a name="additional-information"></a>追加情報

[コマンド ライン構文の記号](command-line-syntax-key.md)