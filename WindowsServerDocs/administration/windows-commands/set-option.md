---
title: SET オプション
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 81678768bb2b5fcfd7f2f2d067562e78e93dc549
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848853"
---
# <a name="set-option"></a>SET オプション



シャドウ コピーの作成のオプションを設定します。 パラメーターを指定せずに使用する場合 **オプション設定** コマンド プロンプトでヘルプを表示します。

## <a name="syntax"></a>構文

```
set option {[differential | plex] [transportable] [[rollbackrecover] [txfrecover] | [noautorecover]]}
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[差分 | プレックス]|プロバイダーを作成するためのシャドウ コピーの種類を指定します。|
|[転送]|シャドウ コピーがまだインポートすることを示します。 メタデータの .cab ファイルは、同じまたは別のコンピューターにシャドウ コピーをインポートする後で使用できます。|
|[rollbackrecover]|通知を使用するライター *自動* 中に、 **PostSnapshot** イベントです。 これは、シャドウ コピーが (たとえば、データ マイニング) でロールバックのために使用される場合に役立ちます。|
|[txfrecover]|VSS の要求の作成時にトランザクション上の一貫性のシャドウ コピーを作成します。|
|[noautorecover]|停止ライターと影に回復変更を加えるからファイル システムは、トランザクション一貫性のある状態にコピーします。 **Noautorecover** では使用できません **txfrecover** または **rollbackrecover**します。|

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)