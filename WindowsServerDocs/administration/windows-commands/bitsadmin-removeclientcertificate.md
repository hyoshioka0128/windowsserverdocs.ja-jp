---
title: bitsadmin removeclientcertificate
description: '**Bitsadmin removeclientcertificate**の Windows コマンドのトピックでは、クライアント証明書をジョブから削除します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b417c3e5-aadd-4fcc-968f-45d8b67ca516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c664ba9b26f3511dedf35477a1cd393db709337e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381045"
---
# <a name="bitsadmin-removeclientcertificate"></a>bitsadmin removeclientcertificate



クライアント証明書をジョブから削除します。

## <a name="syntax"></a>構文

```
bitsadmin /RemoveClientCertificate <Job> 
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例

次の例では、 *Myjob*という名前のジョブからクライアント証明書を削除します。
```
C:\>Bitsadmin /RemoveClientCertificate myJob 
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)