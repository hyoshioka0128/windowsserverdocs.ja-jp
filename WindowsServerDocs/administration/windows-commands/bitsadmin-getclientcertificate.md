---
title: bitsadmin getclientcertificate
description: '**Bitsadmin getclientcertificate**の Windows コマンドトピックでは、ジョブからクライアント証明書を取得します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4fc8f408-085e-43a0-9fa8-3d798ef107b1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 613feafb442f63513d34e9038647c4dbeb278630
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381721"
---
# <a name="bitsadmin-getclientcertificate"></a>bitsadmin getclientcertificate



ジョブからクライアント証明書を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetClientCertificate <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブのクライアント証明書を取得します。
```
C:\>bitsadmin / GetClientCertificate myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)