---
title: bitsadmin util と enableanalytics のチャネル
description: BITS クライアント分析チャネルを有効または無効にする bitsadmin util および enableanalytics のチャネルに関する Windows コマンドのトピック。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0d7645aa-b91b-4ed7-b630-a1e1be6f6ae9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7302c9368649d47cd65110f4a515b527d3df2aac
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848985"
---
# <a name="bitsadmin-util-and-enableanalyticchannel"></a>bitsadmin util と enableanalytics のチャネル

BITS クライアント分析チャネルを有効または無効にします。

## <a name="syntax"></a>構文

```
bitsadmin /Util /EnableAnalyticChannel TRUE|FALSE
```

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、BITS クライアント分析チャネルを有効にします。
```
C:\>bitsadmin /Util / EnableAnalyticChannel TRUE
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)