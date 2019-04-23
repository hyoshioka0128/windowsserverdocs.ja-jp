---
title: bitsadmin getclientcertificate
description: Windows コマンド」のトピック**bitsadmin getclientcertificate** -ジョブからクライアント証明書を取得します。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 113d733d1deb9fbb1c89231495cb7af668a444d5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869043"
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

次の例では、という名前のジョブの クライアント証明書を取得する*myDownloadJob*します。
```
C:\>bitsadmin / GetClientCertificate myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)