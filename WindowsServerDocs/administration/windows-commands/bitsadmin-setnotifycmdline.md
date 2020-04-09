---
title: bitsadmin setnotifycmdline
description: Bitsadmin setnotifycmdline の Windows コマンドトピックでは、ジョブがデータの転送を終了したとき、またはジョブが状態になったときに実行されるコマンドラインコマンドを設定します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 415ae6ef-8549-48b2-9693-2368a6e24075
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 761a7003e44e8dc15cb2dd2f1ce5a1a23be53286
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849335"
---
# <a name="bitsadmin-setnotifycmdline"></a>bitsadmin setnotifycmdline

ジョブがデータの転送を終了したとき、またはジョブが状態に入ったときに実行されるコマンドラインコマンドを設定します。

**BITS 1.2 以前**: サポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /SetNotifyCmdLine <Job> <ProgramName> [ProgramParameters]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|ProgramName|ジョブの完了時に実行するコマンドの名前。|
|ProgramParameters|*ProgramName*に渡すパラメーター。|

## <a name="remarks"></a>コメント

*ProgramName*と*PROGRAMPARAMETERS*には NULL を指定できます。 *ProgramName*が null の場合、 *PROGRAMPARAMETERS*は null である必要があります。

> [!IMPORTANT]
> *Programparameters*が NULL でない場合、 *programparameters*の最初のパラメーターは*ProgramName*と一致する必要があります。

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、 *Mydownloadjob*という名前のジョブが完了したときに、メモ帳を実行するためにサービスによって使用されるコマンドラインコマンドを設定します。
```
C:\>bitsadmin /SetNotifyCmdLine myDownloadJob c:\winnt\system32\notepad.exe NULL
```
```
C:\>bitsadmin /SetNotifyCmdLine myDownloadJob c:\winnt\system32\notepad.exe notepad c:\eula.txt
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)