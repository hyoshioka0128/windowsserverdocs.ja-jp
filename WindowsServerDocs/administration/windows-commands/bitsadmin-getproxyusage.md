---
title: bitsadmin getproxyusage
description: '**Bitsadmin getproxyusage**の Windows コマンドトピックでは、指定されたジョブのプロキシ使用法の設定を取得します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f940a70e-3b02-497e-a47f-b37b905c299e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ea9a22f4fb35af3436d02d9f23b62ce0888a26b0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381291"
---
# <a name="bitsadmin-getproxyusage"></a>bitsadmin getproxyusage



指定したジョブのプロキシ使用法の設定を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetProxyUsage <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="remarks"></a>コメント

設定できる値は次のとおりです。
-   PRECONFIG —所有者の Internet Explorer の既定値を使用します。
-   NO_PROXY —プロキシサーバーを使用しません。
-   OVERRIDE —明示的なプロキシリストを使用します。
-   自動検出—プロキシ設定を自動的に検出します。

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブのプロキシの使用状況を取得します。
```
C:\>bitsadmin /GetProxyUsage myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)