---
title: bdehdcfg サイズ
description: Windows コマンド」のトピックでは、新しいシステム ドライブを作成するときに、システム パーティションのサイズを指定します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 80f55b1d-a28d-4edf-9997-1fb918b7b5a1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d024bb4092f93782300d6afb9053cee1da32629a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817523"
---
# <a name="bdehdcfg-size"></a>bdehdcfg: サイズ



新しいシステム ドライブを作成するときは、システム パーティションのサイズを指定します。 このコマンドの使用方法の例は、次を参照してください。[例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink} -size <SizeinMB>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<SizeinMB >|メガバイト (MB) を使用して、新しいパーティションの数を示します。|

## <a name="remarks"></a>注釈

サイズを指定しない場合、ツールは 300 MB の既定値を使用します。 システム ドライブの最小サイズは、100 MB です。 システム パーティションには、システムの回復またはその他のシステム ツールを保存する、する場合は、それに応じてサイズを増やす必要があります。

> [!NOTE]
> **サイズ**コマンドと組み合わせることはできません、**ターゲット**\<ドライブ文字 >**マージ**コマンド。

## <a name="BKMK_Examples"></a>例

次の例を使用して、**サイズ**に 500 MB を既定のシステム ドライブに割り当てるコマンド。
```
bdehdcfg -target default -size 500
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンドライン構文キー](command-line-syntax-key.md)
-   [Bdehdcfg](bdehdcfg.md)