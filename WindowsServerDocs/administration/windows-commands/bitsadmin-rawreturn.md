---
title: bitsadmin rawreturn
description: Windows コマンド」のトピック**bitsadmin rawreturn** -を解析するための適切なデータを返します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bbe97130-26f6-4cdd-84f1-baf530ce38b7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4e12c8e621021d35ac618b4592515fe38c36be0e
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434891"
---
# <a name="bitsadmin-rawreturn"></a>bitsadmin rawreturn

解析するための適切なデータを返します。

## <a name="syntax"></a>構文

```
bitsadmin /RawReturn
```

## <a name="remarks"></a>注釈

ストリップの改行文字と、出力の書式設定します。

組み合わせてこのコマンドを使用する、通常、**作成**と**取得\\** * 値のみを受け取るスイッチ。 その他のスイッチの前に、このスイッチを指定する必要があります。

## <a name="BKMK_examples"></a>例

次の例は、という名前のジョブの状態の生データを取得*myDownloadJob*します。
```
C:\>bitsadmin /RawReturn /GetState myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)