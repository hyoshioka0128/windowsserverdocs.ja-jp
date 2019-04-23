---
title: bitsadmin replaceremoteprefix
description: Windows コマンド」のトピック**bitsadmin replaceremoteprefix** -ジョブのすべてのファイルをリモート URL が始まる*OldPrefix*を使用する変更は*NewPrefix*。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 3d3eba4f62842fa7f862cd4eaea6830e6a08397a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868133"
---
# <a name="bitsadmin-replaceremoteprefix"></a>bitsadmin replaceremoteprefix



ジョブのすべてのファイルをリモート URL が始まる*OldPrefix*を使用する変更は*NewPrefix*します。

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

## <a name="BKMK_examples"></a>例

次の例では、という名前のジョブのすべてのファイルを変更する*myDownloadJob*リモート URL から始まりますが*http://stageserver*に *http://prodserver*します。
```
C:\>bitsadmin /ReplaceRemotePrefix myDownloadJob http://stageserver http://prodserver
```

## <a name="additional-information"></a>追加情報

[コマンドライン構文キー](command-line-syntax-key.md)