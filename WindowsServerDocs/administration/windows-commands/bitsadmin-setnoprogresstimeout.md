---
title: bitsadmin setnoprogresstimeout
description: Windows コマンド」のトピック**bitsadmin setnoprogresstimeout** -一時的なエラーが発生した後に、ファイルを転送しようとするサービスを秒単位で時間の長さを設定します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7fac50d9-cc6b-46a4-a96f-fab751ee1756
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 45dd8a7ddfae877984a98db66c742e0af4d18f0d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873773"
---
# <a name="bitsadmin-setnoprogresstimeout"></a>bitsadmin setnoprogresstimeout

最初の一時的なエラーが発生した後に、ファイルを転送しようとするビットを秒単位で時間の長さを設定します。

## <a name="syntax"></a>構文

```
bitsadmin /SetNoProgressTimeout <Job> <TimeOutvalue>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|TimeOutvalue|秒単位で表された数値。|

## <a name="remarks"></a>注釈

-   なしの進行状況のタイムアウト間隔は、一時的なエラーを検出すると、ジョブを開始します。
-   タイムアウト間隔が停止またはバイトのデータが正常に転送されるときにリセットします。
-   進行状況のタイムアウト間隔がない場合、 *TimeOutvalue*ジョブが致命的なエラー状態で保存されます。

## <a name="BKMK_examples"></a>例

次の例では、という名前のジョブのない進行状況のタイムアウト値が設定*myDownloadJob*を 20 秒
```
C:\>bitsadmin /SetNoProgressTimeout myDownloadJob 20
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)