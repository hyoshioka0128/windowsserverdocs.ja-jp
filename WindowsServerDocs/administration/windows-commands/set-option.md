---
title: SET オプション
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4d8d4921-9fdd-4a3c-bb0f-9df5458c4b84
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9b9174f219654e99eb9441abe3342c31b5089ef5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384047"
---
# <a name="set-option"></a>SET オプション



シャドウ コピーの作成のオプションを設定します。 パラメーターを指定せずに使用する場合 **オプション設定** コマンド プロンプトでヘルプを表示します。

## <a name="syntax"></a>構文

```
set option {[differential | plex] [transportable] [[rollbackrecover] [txfrecover] | [noautorecover]]}
```

## <a name="parameters"></a>パラメーター

|     パラメーター     |                                                                                                  説明                                                                                                  |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   [差分   |                                                                                                     p                                                                                                     |
|  転送可能な  |                       シャドウ コピーがまだインポートすることを示します。 メタデータの .cab ファイルは、同じまたは別のコンピューターにシャドウ コピーをインポートする後で使用できます。                       |
| [rollbackrecover] |                     通知を使用するライター *自動* 中に、 **PostSnapshot** イベントです。 これは、シャドウコピーがロールバックに使用される場合 (たとえば、データマイニングを使用する場合) に役立ちます。                      |
|   [txfrecover]    |                                                               VSS の要求の作成時にトランザクション上の一貫性のシャドウ コピーを作成します。                                                                |
|  [noautorecover 回復]  | 停止ライターと影に回復変更を加えるからファイル システムは、トランザクション一貫性のある状態にコピーします。 **Noautorecover** では使用できません **txfrecover** または **rollbackrecover**します。 |

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)