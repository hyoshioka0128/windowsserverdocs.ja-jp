---
title: プロバイダーの一覧表示
description: '[プロバイダーの一覧表示] コマンドのリファレンストピックでは、システムに現在登録されているシャドウコピープロバイダーの一覧を示します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 844b4036-c0b9-449d-8347-7d58ef9bf16d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 98615dfa92c24b91babb55ae3545065834887e5d
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83817242"
---
# <a name="list-providers"></a>プロバイダーの一覧表示

システムに現在登録されているシャドウコピープロバイダーの一覧を表示します。

## <a name="syntax"></a>構文

```
list providers
```

### <a name="examples"></a>例

現在登録されているシャドウコピープロバイダーの一覧を表示するには、次のように入力します。

```
list providers
```

次のような出力が表示されます。

```
* ProviderID: {b5946137-7b9f-4925-af80-51abd60b20d5}
        Type: [1] VSS_PROV_SYSTEM
        Name: Microsoft Software Shadow Copy provider 1.0
        Version: 1.0.0.7
        CLSID: {65ee1dba-8ff4-4a58-ac1c-3470ee2f376a}
1 provider registered.
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)