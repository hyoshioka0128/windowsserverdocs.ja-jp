---
title: bitsadmin getnotifycmdline
description: Windows コマンド」のトピック**bitsadmin getnotifycmdline** -データを転送するジョブの完了時に実行されるコマンド ライン コマンドを取得します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 90fa33e6-aca5-4a23-82bd-19a9f13f8416
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3ca7b2e67c0b5672733a25465fba89d1bd69d07a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817293"
---
# <a name="bitsadmin-getnotifycmdline"></a>bitsadmin getnotifycmdline

データを転送するジョブの終了時に実行するコマンド ライン コマンドを取得します。

**1.2 およびそれ以前の BITS**: サポートされません。

## <a name="syntax"></a>構文

```
bitsadmin /GetNotifyCmdLine <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例

次の例では、ジョブは、名前付きサービスで使用するコマンド ライン コマンド*myDownloadJob*が完了するとします。
```
C:\>bitsadmin /GetNotifyCmdLine myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)