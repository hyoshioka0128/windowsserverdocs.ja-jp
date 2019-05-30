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
ms.openlocfilehash: 848c57736c3530e296cffb970237149b4634de67
ms.sourcegitcommit: d84dc3d037911ad698f5e3e84348b867c5f46ed8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2019
ms.locfileid: "66266519"
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

## <a name="examples"></a>例

次の例では、という名前のジョブのすべてのファイルを変更する*myDownloadJob*リモート URL から始まりますが *http://stageserver* に *http://prodserver* します。
```
C:\>bitsadmin /ReplaceRemotePrefix myDownloadJob http://stageserver http://prodserver
```

## <a name="additional-information"></a>追加情報

[コマンド ライン構文の記号](command-line-syntax-key.md)