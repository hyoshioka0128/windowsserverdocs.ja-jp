---
title: bitsadmin ピアキャッシュと getconfigurationflags
description: '**Bitsadmin ピアキャッシュと getconfigurationflags**に関する Windows コマンドトピックでは、コンピューターがピアにコンテンツを提供し、ピアからコンテンツをダウンロードできるかどうかを決定する構成フラグを取得します。'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 94c7eb1a115fe9152b149b8cf65765b179080cc3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381092"
---
# <a name="bitsadmin-peercaching-and-getconfigurationflags"></a>bitsadmin ピアキャッシュと getconfigurationflags



コンピューターがピアにコンテンツを提供し、ピアからコンテンツをダウンロードできるかどうかを決定する構成フラグを取得します。

## <a name="syntax"></a>構文

```
bitsadmin /PeerCaching /GetConfigurationFlags <Job> 
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例

次の例では、 *Myjob*という名前のジョブの構成フラグを取得します。
```
C:\> Bitsadmin /PeerCaching /GetConfigurationFlags myJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)