---
title: bdehdcfg 再起動
description: Windows コマンド」のトピックの bdehdcfg restart - 示します bdehdcfg ドライブの準備が完了した後にコンピューターを再起動する必要があります。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a98b76bb-36f1-4790-b337-7dc35f606bc6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0f361db8fdf33bd414556575de75241f7dbd9327
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879463"
---
# <a name="bdehdcfg-restart"></a>bdehdcfg: restart



ドライブの準備が完了した後にコンピューターを再起動する必要があります、Bdehdcfg コマンド ライン ツールを通知します。 このコマンドの使用方法の例は、次を参照してください。[例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink|<DriveLetter> merge} -restart
```

### <a name="parameters"></a>パラメーター

このコマンドは、追加のパラメーターを受け取りません。

## <a name="remarks"></a>注釈

他のユーザーがコンピューターにログオンしている場合、 **quiet**コマンドが指定されていない、コンピューターを再起動する必要があることを確認するプロンプトが表示されます。

## <a name="BKMK_Examples"></a>例

次の例を使用して、**再起動**コマンド。
```
bdehdcfg -target default -restart
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンドライン構文キー](command-line-syntax-key.md)
-   [Bdehdcfg](bdehdcfg.md)