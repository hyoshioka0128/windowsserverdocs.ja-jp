---
title: bitsadmin setreplyfilename
description: Windows コマンド」のトピック**bitsadmin setreplyfilename** -サーバーの応答を含むファイルのパスを指定します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c26d3342-0533-40b1-a13e-e09678232b25
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b86d4137f661e9953d6d397b2fbc890393bbd8a0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852873"
---
# <a name="bitsadmin-setreplyfilename"></a>bitsadmin setreplyfilename

サーバー応答を含むファイルのパスを指定します。

**1.2 およびそれ以前の BITS**: サポートされません。

## <a name="syntax"></a>構文

```
bitsadmin /SetReplyFileName <Job> <Path>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|パス|サーバー応答を配置する場所|

## <a name="remarks"></a>注釈

アップロード応答ジョブに対してのみ有効です。

## <a name="BKMK_examples"></a>例

次の例では、設定、応答ファイル名 pathfor という名前のジョブ*myDownloadJob*します。
```
C:\>bitsadmin /SetReplyFileName myDownloadJob c:\reply
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)