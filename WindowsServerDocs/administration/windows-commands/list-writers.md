---
title: ライターの一覧
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1c30cbc4-f568-4fa7-b564-66c41d3ca82d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6fbab6644d46dbb352a5d5a51abefb293f3ffe6f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866743"
---
# <a name="list-writers"></a>ライターの一覧



ライターは、システム上にあるを一覧表示します。 パラメーターを指定せずに使用されている場合**一覧**の出力が表示されます**メタデータを一覧表示**既定。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
list writers [metadata | detailed | status]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|メタデータ (metadata)|Id とライターの状態を一覧表示し、コンポーネントの詳細とファイルの除外などのメタデータを表示します。 これは、既定のパラメーターです。|
|詳細|同じ情報を一覧表示**メタデータ**が**詳細**のすべてのコンポーネント ファイルの完全一覧が含まれています。|
|status|Id と登録されているライターの状態を一覧表示します。|

## <a name="BKMK_examples"></a>例

Id とライターの状態を一覧表示するには、次のように入力します。
```
list writers status
```
次のような出力:
```
Listing writer status ...
* WRITER "System Writer"
        - Status: 5 (VSS_WS_WAITING_FOR_BACKUP_COMPLETE)
        - Writer Failure code: 0x00000000 (S_OK)
        - Writer ID: {e8132975-6f93-4464-a53e-1050253ae220}
        - Instance ID: {7e631031-c695-4229-9da1-a7de057e64cb}
* WRITER "Shadow Copy Optimization Writer"
        - Status: 1 (VSS_WS_STABLE)
        - Writer Failure code: 0x00000000 (S_OK)
        - Writer ID: {4dc3bdd4-ab48-4d07-adb0-3bee2926fd7f}
        - Instance ID: {9e362607-9794-4dd4-a7cd-b3d5de0aad20}
...
...
...
* WRITER "Registry Writer"
        - Status: 1 (VSS_WS_STABLE)
        - Writer Failure code: 0x00000000 (S_OK)
        - Writer ID: {afbab4a2-367d-4d15-a586-71dbb18f8485}
        - Instance ID: {e87ba7e3-f8d8-42d8-b2ee-c76ae26b98e8}
8 writers listed. 
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)