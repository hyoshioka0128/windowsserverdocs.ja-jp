---
title: bitsadmin setnotifycmdline
description: Windows コマンド」のトピック * * *-bitsadmin setnotifycmdlineSets ジョブでは、データの転送が完了すると、またはジョブの状態になったときに実行するコマンド ライン コマンド。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: f1cea4e99cbaaf3881c6f436bdb932090ad6b006
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859073"
---
# <a name="bitsadmin-setnotifycmdline"></a>bitsadmin setnotifycmdline

ジョブは、データの転送が完了すると、またはジョブの状態になったときに実行するコマンド ライン コマンドを設定します。

**1.2 およびそれ以前の BITS**: サポートされません。

## <a name="syntax"></a>構文

```
bitsadmin /SetNotifyCmdLine <Job> <ProgramName> [ProgramParameters]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|プログラム名|ジョブの完了時に実行するコマンドの名前。|
|ProgramParameters|渡すパラメーター *ProgramName*します。|

## <a name="remarks"></a>注釈

場合は NULL を指定する*ProgramName*と*ProgramParameters*します。 場合*ProgramName*が null の場合、 *ProgramParameters* NULL にする必要があります。

> [!IMPORTANT]
> 場合*ProgramParameters* null の場合、その後の最初のパラメーターでない*ProgramParameters*と一致する必要があります*ProgramName*します。

## <a name="BKMK_examples"></a>例

次の例では、という名前のジョブは、メモ帳を実行するサービスによって使用されるコマンド ライン コマンド*myDownloadJob*が完了するとします。
```
C:\>bitsadmin /SetNotifyCmdLine myDownloadJob c:\winnt\system32\notepad.exe NULL
```
```
C:\>bitsadmin /SetNotifyCmdLine myDownloadJob c:\winnt\system32\notepad.exe "notepad c:\eula.txt"
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)