---
title: bitsadmin getfilestotal
description: Windows コマンド」のトピック**bitsadmin getfilestotal** -指定したジョブ内のファイルの数を取得します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c5de113e-f29c-4cd3-9392-0e300018d516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 21240cfa1f0fa1f8e8fc3d2acf83f5df80812816
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857463"
---
# <a name="bitsadmin-getfilestotal"></a>bitsadmin getfilestotal



指定したジョブ内のファイルの数を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetFilesTotal <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例

次の例では、という名前のジョブに含まれるファイルの数を取得する*myDownloadJob*します。
```
C:\>bitsadmin /GetFilesTotal myDownloadJob
```

##

[コマンドライン構文キー](command-line-syntax-key.md)も参照してください