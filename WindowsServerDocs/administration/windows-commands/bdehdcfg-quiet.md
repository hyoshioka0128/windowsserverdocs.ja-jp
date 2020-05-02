---
title: bdehdcfg quiet
description: Bdehdcfg quiet コマンドのリファレンストピック。すべてのアクションとエラーを表示しないように bdehdcfg に指示します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7f75b702-890b-4ff9-805c-edf5cadd8822
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: afb7a73899259b0f3823941ece014ea85568a4ce
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718638"
---
# <a name="bdehdcfg-quiet"></a>bdehdcfg: quiet

Bdehdcfg コマンドラインツールに、すべてのアクションとエラーがコマンドラインインターフェイスに表示されないことを通知します。 ドライブの準備中に表示される [はい/いいえ] (Y/N) プロンプトでは、"Yes" という答えが想定されます。 ドライブの準備中に発生したエラーを表示するには、 **DrivePreparationTool**イベントプロバイダーの下にあるシステムイベントログを確認します。

## <a name="syntax"></a>構文

```
bdehdcfg -target {default|unallocated|<drive_letter> shrink|<drive_letter> merge} -quiet
```

#### <a name="parameters"></a>パラメーター

このコマンドには追加のパラメーターはありません。

## <a name="examples"></a>例

**Quiet**コマンドを使用するには、次のようにします。

```
bdehdcfg -target default -quiet
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bdehdcfg](bdehdcfg.md)
