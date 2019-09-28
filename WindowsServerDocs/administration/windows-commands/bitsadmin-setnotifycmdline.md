---
title: bitsadmin setnotifycmdline
description: Windows コマンドのトピック * * * *-bitsadmin setnotifycmdlineSets、ジョブがデータの転送を終了したとき、またはジョブが状態に入ったときに実行されるコマンドラインコマンドを設定します。
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 415ae6ef-8549-48b2-9693-2368a6e24075
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7a307fe552e7d8ec5852de953a3a439cb02246ec
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380480"
---
# <a name="bitsadmin-setnotifycmdline"></a>bitsadmin setnotifycmdline

ジョブがデータの転送を終了したとき、またはジョブが状態に入ったときに実行されるコマンドラインコマンドを設定します。

**BITS 1.2 以前**: サポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /SetNotifyCmdLine <Job> <ProgramName> [ProgramParameters]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|ProgramName|ジョブの完了時に実行するコマンドの名前。|
|ProgramParameters|*ProgramName*に渡すパラメーター。|

## <a name="remarks"></a>コメント

*ProgramName*と*PROGRAMPARAMETERS*には NULL を指定できます。 *ProgramName*が null の場合、 *PROGRAMPARAMETERS*は null である必要があります。

> [!IMPORTANT]
> *Programparameters*が NULL でない場合、 *programparameters*の最初のパラメーターは*ProgramName*と一致する必要があります。

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブが完了したときに、メモ帳を実行するためにサービスによって使用されるコマンドラインコマンドを設定します。
```
C:\>bitsadmin /SetNotifyCmdLine myDownloadJob c:\winnt\system32\notepad.exe NULL
```
```
C:\>bitsadmin /SetNotifyCmdLine myDownloadJob c:\winnt\system32\notepad.exe "notepad c:\eula.txt"
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)