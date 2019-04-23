---
title: bitsadmin getnoprogresstimeout
description: Windows コマンド」のトピック**bitsadmin getnoprogresstimeout** -一時的なエラーが発生した後に、ファイルを転送しようとするサービスを秒単位での時間の長さを取得します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9cd9b19b-cbb4-4352-8419-978080f016b6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9563b68b8012a49471b56e3b8f2fbd60d1c69756
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850803"
---
# <a name="bitsadmin-getnoprogresstimeout"></a>bitsadmin getnoprogresstimeout



一時的なエラーが発生した後に、ファイルを転送しようとするサービスを秒単位での時間の長さを取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetNoProgressTimeout <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例

次の例では、という名前のジョブの進行状況のタイムアウト値を取得する*myDownloadJob*します。
```
C:\>bitsadmin /GetNoProgressTimeout myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)