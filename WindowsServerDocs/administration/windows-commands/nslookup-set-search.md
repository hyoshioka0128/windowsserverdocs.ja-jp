---
title: nslookup set search
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 064ac660-8b04-4af9-8b2c-e4e0549771b8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bf952a0337e23c0426265c6c0a4a8387a6ab45e1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816993"
---
# <a name="nslookup-set-search"></a>nslookup set search



応答が受信されるまでは、ドメインの DNS 検索リストにドメイン ネーム システム (DNS) ドメイン名、要求に追加します。 これは、セット、検索要求を少なくとも 1 つのピリオドを含めるときに適用されますが、末尾のピリオドで終わらない。

## <a name="syntax"></a>構文

```
set [no]search
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|**nosearch**|要求にドメインの DNS 検索リストにドメイン ネーム システム (DNS) ドメイン名を追加することを停止します。|
|**search**|応答が受信されるまでは、ドメインの DNS 検索リストにドメイン ネーム システム (DNS) ドメイン名、要求に追加します。 既定の構文は**検索**します。|
|{0} のヘルプ | ?}|簡単な概要を表示します。 **nslookup**サブコマンドします。|

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)