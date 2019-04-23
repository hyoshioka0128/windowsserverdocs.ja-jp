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
ms.openlocfilehash: eabcc5cacdcc5f7f4de7178b5afeff2acc89d7a8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862813"
---
#<a name="bitsadmin-getpeercachingflags"></a>bitsadmin getpeercachingflags

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
[コマンドライン構文キー](command-line-syntax-key.md)


