---
title: bitsadmin nowrap
description: '**Bitsadmin nowrap**の Windows コマンドに関するトピックでは、コマンドウィンドウの右端を超えて拡張される出力テキストの行をすべて切り捨てます。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 85a47b90-783a-41e4-96f2-81f26ae8ca93
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f9f1db370d8a8917aa03a414a27623a1024df192
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850185"
---
# <a name="bitsadmin-nowrap"></a>bitsadmin nowrap

コマンドウィンドウの右端を超えて拡張する出力テキストの行をすべて切り捨てます。 既定では、**モニター**スイッチを除くすべてのスイッチが出力をラップします。 他のスイッチの前に、 **nowrap**スイッチを指定します。

## <a name="syntax"></a>構文

```
bitsadmin /nowrap
```

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、 *Mydownloadjob*という名前のジョブの状態を取得し、出力をラップしません。

```
C:\>bitsadmin /nowrap /getstate myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)