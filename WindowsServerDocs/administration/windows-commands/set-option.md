---
title: SET オプション
description: シャドウコピーの作成のオプションを設定する Set オプションのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4d8d4921-9fdd-4a3c-bb0f-9df5458c4b84
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a4aba049e29cd74450467cf28057a2ff4e4a7094
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721902"
---
# <a name="set-option"></a>SET オプション

シャドウ コピーの作成のオプションを設定します。 パラメーターを指定せずに使用する場合 **オプション設定** コマンド プロンプトでヘルプを表示します。

## <a name="syntax"></a>構文

```
set option {[differential | plex] [transportable] [[rollbackrecover] [txfrecover] | [noautorecover]]}
```

### <a name="parameters"></a>パラメーター

|     パラメーター     |                                                                                                  [説明]                                                                                                  |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   [差分   |                                                                                                     p                                                                                                     |
|  転送可能な  |                       シャドウ コピーがまだインポートすることを示します。 メタデータの .cab ファイルは、同じまたは別のコンピューターにシャドウ コピーをインポートする後で使用できます。                       |
| [rollbackrecover] |                     通知を使用するライター *自動* 中に、 **PostSnapshot** イベントです。 これは、シャドウコピーがロールバックに使用される場合 (たとえば、データマイニングを使用する場合) に役立ちます。                      |
|   [txfrecover]    |                                                               VSS の要求の作成時にトランザクション上の一貫性のシャドウ コピーを作成します。                                                                |
|  [noautorecover 回復]  | 停止ライターと影に回復変更を加えるからファイル システムは、トランザクション一貫性のある状態にコピーします。 **Noautorecover** では使用できません **txfrecover** または **rollbackrecover**します。 |

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)