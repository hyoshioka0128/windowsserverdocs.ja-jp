---
title: bdehdcfg quiet
description: Windows コマンド」のトピック bdehdcfg quiet - すべてのアクションおよびエラーを表示しない bdehdcfg を示します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7f75b702-890b-4ff9-805c-edf5cadd8822
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0f0d98f6ae76e9bf6357689c97e091766b9645c2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865753"
---
# <a name="bdehdcfg-quiet"></a>bdehdcfg: quiet



すべての操作やエラーは、コマンド ライン インターフェイスに表示される、Bdehdcfg コマンド ライン ツールを通知します。 このコマンドの使用方法の例は、次を参照してください。[例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink|<DriveLetter> merge} -quiet
```

### <a name="parameters"></a>パラメーター

このコマンドは、追加のパラメーターを受け取りません。

## <a name="remarks"></a>注釈

場合、[はい]/(Y/N) プロンプトが表示されていますないドライブの準備中に、"Yes"の応答が使用されます。 ドライブの準備中に発生したエラーを表示するには、システム イベント ログを確認、 **Microsoft Windows BitLocker DrivePreparationTool**イベント プロバイダー。

## <a name="BKMK_Examples"></a>例

次の例を使用して、 **quiet**コマンド。
```
bdehdcfg -target default -quiet
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンドライン構文キー](command-line-syntax-key.md)
-   [Bdehdcfg](bdehdcfg.md)