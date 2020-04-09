---
title: bdehdcfg restart
description: '**Bdehdcfg restart**の Windows コマンドに関するトピックでは、ドライブの準備が完了した後にコンピューターを再起動する必要があることを bdehdcfg に指示しています。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a98b76bb-36f1-4790-b337-7dc35f606bc6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9ae6f8d31c09feddf8f994c28d34e4e1b08cc322
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851035"
---
# <a name="bdehdcfg-restart"></a>bdehdcfg: 再起動

ドライブの準備が完了した後にコンピューターを再起動する必要があることを Bdehdcfg コマンドラインツールに通知します。 このコマンドを使用する方法の例については、「[例](#BKMK_Examples)」を参照してください。

## <a name="syntax"></a>構文

```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink|<DriveLetter> merge} -restart
```

#### <a name="parameters"></a>パラメーター

このコマンドは、追加のパラメーターを受け取りません。

## <a name="remarks"></a>コメント

他のユーザーがコンピューターにログオンしていて、 **quiet**コマンドが指定されていない場合は、コンピューターを再起動するかどうかを確認するプロンプトが表示されます。

## <a name="examples"></a><a name="BKMK_Examples"></a>例

次の例は、 **restart**コマンドの使用方法を示しています。

```
bdehdcfg -target default -restart
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [Bdehdcfg](bdehdcfg.md)