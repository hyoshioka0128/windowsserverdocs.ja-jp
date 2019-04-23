---
title: bitsadmin getreplyprogress
description: Windows コマンド」のトピック**bitsadmin getreplyprogress** -サーバーの応答の進行状況とサイズを取得します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7f7cb0b4-ad95-44fd-a35d-0ddf5fc0b0d0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: aafecfb5873392ef86e6f7cceb139091b15e3b99
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852933"
---
# <a name="bitsadmin-getreplyprogress"></a>bitsadmin getreplyprogress

サーバー応答の進行状況とサイズを取得します。

**1.2 およびそれ以前の BITS**: サポートされません。

## <a name="syntax"></a>構文

```
bitsadmin /GetReplyProgress <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="remarks"></a>注釈

アップロード応答ジョブに対してのみ有効です。

## <a name="BKMK_examples"></a>例

次の例は、という名前のジョブ応答の進行状況を取得*myDownloadJob*します。
```
C:\>bitsadmin /GetReplyProgress myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)