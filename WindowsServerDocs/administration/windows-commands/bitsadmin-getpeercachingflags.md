---
title: bitsadmin getpeercachingflags
description: '**Bitsadmin getpeercachingflags**の Windows コマンドトピックでは、ジョブのファイルをキャッシュしてピアに提供できるかどうか、BITS がピアからジョブのコンテンツをダウンロードできるかどうかを決定するフラグを取得します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3c3c9f28-4c04-4c49-a23a-dee5bbcc8981
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6b86214b5289a59e8db2ecff065ab3b8cd17007e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381437"
---
# <a name="bitsadmin-getpeercachingflags"></a>bitsadmin getpeercachingflags

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ジョブのファイルをキャッシュしてピアに提供できるかどうか、および BITS がピアからジョブのコンテンツをダウンロードできるかどうかを決定するフラグを取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetPeerCachingFlags <Job> 
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------|--------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例
次の例では、 *myjob*という名前のジョブのフラグを取得します。

```
C:\>bitsadmin /GetPeerCachingFlags myJob
```

## <a name="additional-references"></a>その他の参照情報
[コマンド ライン構文の記号](command-line-syntax-key.md)


