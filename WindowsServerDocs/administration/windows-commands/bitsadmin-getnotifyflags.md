---
title: bitsadmin getnotifyflags
description: '**Bitsadmin getnotifyflags**の Windows コマンドトピックでは、指定したジョブの通知フラグを取得します。'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 56ee3a30050b6cc934b35bab24e9508911ea250e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381480"
---
# <a name="bitsadmin-getnotifyflags"></a>bitsadmin getnotifyflags



指定されたジョブの通知フラグを取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetNotifyFlags <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="remarks"></a>コメント

ジョブには、次の1つ以上の通知フラグを含めることができます。

|-----|-----| | 0x001 |ジョブ内のすべてのファイルが転送されたときにイベントを生成します |。| 0x002 |エラーが発生したときにイベントを生成します |。| 0x004 |通知を無効にします |。| 0x008 |ジョブが変更されたとき、または転送の進行状況が発生したときにイベントを生成します |。

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブの通知フラグを取得します。
```
C:\>bitsadmin /GetNotifyFlags myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)