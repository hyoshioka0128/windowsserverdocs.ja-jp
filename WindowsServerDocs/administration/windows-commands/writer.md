---
title: ライター
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7cf98295-411d-4705-8573-f898ff45c140
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6c00f6067cd5f6cf741cddbd6d62c5bcbb1f37a9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361859"
---
# <a name="writer"></a>ライター



ライターまたはコンポーネントが含まれていること、または backup または restore プロシージャからライターまたはコンポーネントが除外されていることを確認します。 パラメーターを指定せずに使用した場合、**ライター**はコマンドプロンプトでヘルプを表示します。

## <a name="syntax"></a>構文

```
writer verify [<Writer> | <Component>]
writer exclude [<Writer> | <Component>]
```

## <a name="parameters"></a>パラメーター

| パラメーター  |                                                                                      説明                                                                                      |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   verify   | 指定されたライターまたはコンポーネントが、バックアップまたは復元の手順に含まれていることを確認します。 ライターまたはコンポーネントが含まれていない場合、バックアップまたは復元の手順は失敗します。 |
|  exclude   |                                                   指定されたライターまたはコンポーネントをバックアップまたは復元の手順から除外します。                                                    |
| [\<Writer > |                                                                                     <Component>]                                                                                      |

## <a name="BKMK_examples"></a>例

GUID (この例では 4dc3bdd4-ab48-4d07-adb0-3bee2926fd7f) を指定してライターを確認するには、次のように入力します。
```
writer verify {4dc3bdd4-ab48-4d07-adb0-3bee2926fd7f}
```
"システムライター" という名前のライターを除外するには、次のように入力します。
```
writer exclude "System Writer"
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)