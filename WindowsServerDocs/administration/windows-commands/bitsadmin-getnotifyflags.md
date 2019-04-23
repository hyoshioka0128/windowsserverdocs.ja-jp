---
title: bitsadmin getnotifyflags
description: Windows コマンド」のトピック**bitsadmin getnotifyflags** -指定したジョブの通知フラグを取得します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d4657e6c-8959-4db7-a4af-e73d3f80ecf8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 690e94805c5e61d96603e4ade102fb3a4bda409e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889283"
---
# <a name="bitsadmin-getnotifyflags"></a>bitsadmin getnotifyflags



指定したジョブの通知フラグを取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetNotifyFlags <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="remarks"></a>注釈

ジョブは、次の通知フラグの 1 つ以上含めることができます。

|---|---| | 0x001 |ジョブのすべてのファイルが転送されたときにイベントを生成します |。| 0x002 |エラーが発生したときにイベントを生成します |。| 0x004 |通知を無効にします |。| 0x008 |ジョブを変更するか、転送の進捗状況が行われたときにイベントを生成します |。

## <a name="BKMK_examples"></a>例

次の例では、という名前のジョブの通知フラグを取得する*myDownloadJob*します。
```
C:\>bitsadmin /GetNotifyFlags myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)