---
title: bitsadmin getproxylist-指定したジョブのプロキシの一覧を取得します。
description: '**Bitsadmin getproxylist**の Windows コマンドトピックでは、指定されたジョブのプロキシ一覧を取得します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: eebfa727-d8f1-4ae3-9382-6d8ffe8c3df3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6f176d268c816725b183da0a948afcb25272b2fb
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381315"
---
# <a name="bitsadmin-getproxylist"></a>bitsadmin getproxylist

指定されたジョブのプロキシリストを取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetProxyList <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="remarks"></a>コメント

プロキシリストは、使用するプロキシサーバーの一覧です。 リストはコンマで区切られます。

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブのプロキシ一覧を取得します。
```
C:\>bitsadmin /GetProxyList myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)