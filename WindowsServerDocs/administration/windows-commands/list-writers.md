---
title: ライターの一覧表示
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: d00eebe4e562764e97794b3eb1b76ea96c2dc47c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374720"
---
# <a name="list-writers"></a>ライターの一覧表示



システム上のライターを一覧表示します。 パラメーターを指定せず**に使用**する場合は、リスト**メタデータ**の出力が既定で表示されます。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
list writers [metadata | detailed | status]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|メタデータ (metadata)|ライターの id とステータスを一覧表示し、コンポーネントの詳細や除外されたファイルなどのメタデータを表示します。 これは、既定のパラメーターです。|
|detailed|**メタデータ**と同じ情報を一覧表示しますが、**詳細**についてはすべてのコンポーネントの完全なファイルリストを参照してください。|
|status|登録されているライターの id と状態のみを一覧表示します。|

## <a name="BKMK_examples"></a>例

ライターの id と状態のみを一覧表示するには、次のように入力します。
```
list writers status
```
次のような出力が表示されます。
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

[コマンド ライン構文の記号](command-line-syntax-key.md)