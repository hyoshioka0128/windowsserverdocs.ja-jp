---
title: bitsadmin getdisplayname
description: Windows コマンド」のトピック**bitsadmin getdisplayname** -指定したジョブの表示名を取得します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e5c0e76c-4cc6-42d8-ac30-30bf3dc11b9b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c1ef16f54b7b825e4293a3870d8181985b83843b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857603"
---
# <a name="bitsadmin-getdisplayname"></a>bitsadmin getdisplayname



指定したジョブの表示名を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetDisplayName <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例

次の例では、という名前のジョブの表示名を取得する*myDownloadJob*します。
```
C:\>bitsadmin /GetDisplayName myDownloadJob
```
その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)