---
title: bitsadmin util および version
description: Bitsadmin util と version コマンドのリファレンストピックでは、BITS サービスのバージョンが表示されます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 98f17328-dfbd-4cbb-93c1-b8d424bc3f0a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 20c3db6e6fcd5ef3d00287f36c9f9624ab5224dd
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82707592"
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

| パラメーター | [説明] |
| --------- | ----------- |
| /verbose | このスイッチを使用して、BITS 関連の各 DLL のファイルバージョンを表示し、BITS サービスを開始できるかどうかを確認します。|

## <a name="examples"></a>例

BITS サービスのバージョンを表示します。

```
bitsadmin /util /version
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin util コマンド](bitsadmin-util.md)

- [bitsadmin コマンド](bitsadmin.md)
