---
title: bitsadmin getreplyfilename
description: '**Bitsadmin getreplyfilename**の Windows コマンドに関するトピックでは、サーバーの応答を含むファイルのパスを取得します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 85447184-1732-4816-a365-2e3599551bf8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 96b77e9bd19cdc094e6b025e143b05aff7bc60d5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381268"
---
# <a name="bitsadmin-getreplyfilename"></a>bitsadmin getreplyfilename

サーバー応答を格納しているファイルのパスを取得します。

**BITS 1.2 以前**: サポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /GetReplyFileName <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="remarks"></a>コメント

アップロード/応答ジョブに対してのみ有効です。

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブの応答ファイル名を取得します。
```
C:\>bitsadmin /GetReplyFileName myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)