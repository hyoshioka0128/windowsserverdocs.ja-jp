---
title: bitsadmin reset
description: '**Bitsadmin reset**の Windows コマンドトピック-現在のユーザーが所有している転送キュー内のすべてのジョブをキャンセルします。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e4f9d1d-072c-493f-8d7a-f6d713c3ef29
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: adc6b07a7b5d1414c733fe6a3ac05eba7cb3029e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380814"
---
# <a name="bitsadmin-reset"></a>bitsadmin reset

現在のユーザーが所有している転送キュー内のすべてのジョブをキャンセルします。

**BITSAdmin 1.5 以前**: 管理者特権を持っている場合は、  **リセット**すると、キュー内のすべてのジョブが取り消されます。 /AllUsers オプションはサポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /Reset [/AllUsers]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|AllUsers|省略可能: キュー内のすべてのジョブを取り消します。|

## <a name="remarks"></a>注釈

**AllUsers**パラメーターを使用するには、管理者特権が必要です。

> [!NOTE]
> 管理者は、ローカルシステムによって作成されたジョブをリセットできません。 タスクスケジューラを使用して、ローカルシステムの資格情報を使用して、このコマンドをタスクとしてスケジュールします。

## <a name="BKMK_examples"></a>例

次の例では、現在のユーザーの転送キューにあるすべてのジョブを取り消します。
```
C:\>bitsadmin /Reset
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)