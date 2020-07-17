---
title: bitsadmin util および version
description: BITS サービスのバージョンを表示する bitsadmin util と version コマンドのリファレンス記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 98f17328-dfbd-4cbb-93c1-b8d424bc3f0a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9b0a1a6b6c866acafa8eaccd6ade170abd58bf01
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927290"
---
# <a name="bitsadmin-util-and-version"></a>bitsadmin util および version

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

BITS サービスのバージョンを表示します。

```
bitsadmin /util /version
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin util コマンド](bitsadmin-util.md)

- [bitsadmin コマンド](bitsadmin.md)
