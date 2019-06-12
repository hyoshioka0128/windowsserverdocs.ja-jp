---
title: bitsadmin getpeercachingflags
description: Windows コマンド」のトピック**bitsadmin getpeercachingflags** -ジョブのファイルをキャッシュして、ピアに提供し、BITS では、ジョブのコンテンツをピアからダウンロードできる場合を決定するフラグを取得します。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 28f248bab3e3cc3f5c7dd4f5f878f0b6d776029b
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434920"
---
# <a name="bitsadmin-getpeercachingflags"></a>bitsadmin getpeercachingflags

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ジョブのファイルをキャッシュして、ピアに提供し、BITS では、ジョブのコンテンツをピアからダウンロードできる場合を決定するフラグを取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetPeerCachingFlags <Job> 
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------|--------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例
次の例では、という名前のジョブのフラグを取得する*myJob*します。

```
C:\>bitsadmin /GetPeerCachingFlags myJob
```

## <a name="additional-references"></a>その他の参照
[コマンド ライン構文の記号](command-line-syntax-key.md)


