---
title: bitsadmin ピアキャッシュと getconfigurationflags
description: Windows コマンド」のトピック**bitsadmin ピアキャッシュと getconfigurationflags** - コンピューターがピアにコンテンツを処理するかどうかを決定する構成フラグを取得し、ピアからコンテンツをダウンロードすることができます。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 124ddc15-3444-4bd5-96e5-c6bfabe4f9c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6afa39993cf90b2d71b6b681680c3b4e1fd9b56b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826353"
---
# <a name="bitsadmin-peercaching-and-getconfigurationflags"></a>bitsadmin ピアキャッシュと getconfigurationflags



コンピューターがピアにコンテンツの提供し、ピアからコンテンツをダウンロードすることができるかどうかを決定する構成フラグを取得します。

## <a name="syntax"></a>構文

```
bitsadmin /PeerCaching /GetConfigurationFlags <Job> 
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例

次の例では、という名前のジョブ構成フラグを取得する*myJob*します。
```
C:\> Bitsadmin /PeerCaching /GetConfigurationFlags myJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)