---
title: bitsadmin setreplyfilename
description: '**Bitsadmin setreplyfilename**の Windows コマンドのトピック-サーバーの応答を含むファイルのパスを指定します。'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: a490b5bc565549d096b6f43f42758f77570fcb26
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380416"
---
# <a name="bitsadmin-setreplyfilename"></a>bitsadmin setreplyfilename

サーバーの応答を含むファイルのパスを指定します。

**BITS 1.2 以前**: サポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /SetReplyFileName <Job> <Path>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|パス|サーバー応答を配置する場所|

## <a name="remarks"></a>コメント

アップロード/応答ジョブに対してのみ有効です。

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブに応答ファイル名 pathfor 設定します。
```
C:\>bitsadmin /SetReplyFileName myDownloadJob c:\reply
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)