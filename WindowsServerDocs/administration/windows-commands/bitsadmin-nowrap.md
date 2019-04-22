---
title: bitsadmin nowrap
description: Windows コマンド」のトピック**bitsadmin nowrap** -任意のコマンド ウィンドウの右端の位置を超える出力テキストを拡張する行を切り捨てます。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 85a47b90-783a-41e4-96f2-81f26ae8ca93
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4130f606a6b1874e1ea31952160de44d6e09c6b6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822923"
---
# <a name="bitsadmin-nowrap"></a>bitsadmin nowrap

コマンド ウィンドウの右端の位置を超える出力テキストを拡張する任意の行を切り捨てます。

## <a name="syntax"></a>構文

```
bitsadmin /NoWrap
```

## <a name="remarks"></a>注釈

既定ですべてのスイッチを除く、**モニター**スイッチ、出力をラップします。 指定、 **NoWrap**他のスイッチの前に切り替えます。

## <a name="BKMK_examples"></a>例

次の例では、という名前のジョブの状態を取得する*myDownloadJob*出力は折り返されません
```
C:\>bitsadmin /NoWrap /GetState myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)