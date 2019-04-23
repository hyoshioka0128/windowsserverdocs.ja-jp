---
title: bitsadmin setnotifyflags
description: Windows コマンド」のトピック**bitsadmin setnotifyflags** -イベントの指定したジョブの通知フラグを設定します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d5763d95-94a6-45ca-9e03-891c20047e06
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bc817e03e0f1916ea392830d14985a7a1377d69a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868793"
---
# <a name="bitsadmin-setnotifyflags"></a>bitsadmin setnotifyflags

イベントの指定したジョブの通知フラグを設定します。

## <a name="syntax"></a>構文

```
bitsadmin /SetNotifyFlags <Job> <NotifyFlags>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|NotifyFlags|「解説」を参照してください。|

## <a name="remarks"></a>注釈

**NotifyFlags**パラメーターは、次の通知フラグの 1 つ以上含めることができます。

|---|---| | 1 |ジョブのすべてのファイルが転送されたときにイベントを生成します |。| 2 |エラーが発生したときにイベントを生成します |。| 4 |通知を無効にします |。

## <a name="BKMK_examples"></a>例

次の例は、転送用に通知フラグを設定して、という名前のジョブのジョブのエラー イベント*myDownloadJob*します。
```
C:\>bitsadmin /SetNotifyFlags myDownloadJob 3
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)