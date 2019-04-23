---
title: bitsadmin reset
description: Windows コマンド」のトピック**bitsadmin リセット**-現在のユーザーが所有する、転送キュー内のすべてのジョブを取り消します。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: b7c29aac55393cd87145583814b3ffa8f0a2c3b3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59874253"
---
# <a name="bitsadmin-reset"></a>bitsadmin reset

現在のユーザーが所有する転送キュー内のすべてのジョブをキャンセルします。

**1.5 およびそれ以前の BITSAdmin**: 管理者特権がある場合 **リセット** キュー内のすべてのジョブが取り消されます。 /AllUsers オプションがサポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /Reset [/AllUsers]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|AllUsers|省略可能なキュー内のすべてのジョブをキャンセルします。|

## <a name="remarks"></a>注釈

使用する管理者特権が必要、 **AllUsers**パラメーター。

> [!NOTE]
> 管理者は、ローカル システムによって作成されたジョブをリセットできません。 タスク スケジューラを使用して、ローカル システム資格情報を使用して、タスクとしてこのコマンドをスケジュールします。

## <a name="BKMK_examples"></a>例

次の例では、現在のユーザーの転送キュー内のすべてのジョブをキャンセルします。
```
C:\>bitsadmin /Reset
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)