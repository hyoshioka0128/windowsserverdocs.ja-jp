---
title: bitsadmin util とバージョン
description: '**Bitsadmin util と version**の Windows コマンドに関するトピックでは、BITS サービスのバージョンが表示されます。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 98f17328-dfbd-4cbb-93c1-b8d424bc3f0a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2c2518eb7a8f15d9a592ed9a77dd67a6f8d8afac
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122473"
---
# <a name="bitsadmin-util-and-version"></a>bitsadmin util とバージョン

BITS サービスのバージョン (2.0 など) を表示します。

> [!NOTE]
> このコマンドは、BITS 1.5 以前ではサポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /util /version [/verbose]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| /verbose | このスイッチを使用して、BITS 関連の各 DLL のファイルバージョンを表示し、BITS サービスを開始できるかどうかを確認します。|

## <a name="examples"></a>例

次の例では、BITS サービスのバージョンを示しています。

```
C:\>bitsadmin /util /version
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)