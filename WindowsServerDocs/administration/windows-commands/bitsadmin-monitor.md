---
title: bitsadmin monitor
description: '**Bitsadmin monitor**の Windows コマンドに関するトピックでは、現在のユーザーが所有している転送キュー内のジョブを監視します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2c424d27-e011-49c2-b579-a2c235467c39
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bda268afd5fda24bba2afb04b32bac9cda9a05bb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850215"
---
# <a name="bitsadmin-monitor"></a>bitsadmin monitor

現在のユーザーが所有している転送キュー内のジョブを監視します。

## <a name="syntax"></a>構文

```
bitsadmin /monitor [/allusers] [/refresh <seconds>]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| /allusers | 省略可。 すべてのユーザーのジョブを監視します。 このパラメーターを使用するには、管理者特権が必要です。 |
| /更新 | 省略可。 `<seconds>`によって指定された間隔でデータを更新します。 既定の更新間隔は5秒です。 更新を停止するには、CTRL + C キーを押します。 |

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、現在のユーザーが所有しているジョブの転送キューを監視し、60秒ごとに情報を更新します。

```
C:\>bitsadmin /monitor /refresh 60
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)