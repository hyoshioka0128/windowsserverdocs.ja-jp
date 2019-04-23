---
title: bitsadmin removeclientcertificate
description: Windows コマンド」のトピック**bitsadmin removeclientcertificate** -ジョブからクライアント証明書を削除します。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 7b720800fe80037f38ff01ac3a90d5cbb41a6ec8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868663"
---
# <a name="bitsadmin-removeclientcertificate"></a>bitsadmin removeclientcertificate



ジョブからクライアント証明書を削除します。

## <a name="syntax"></a>構文

```
bitsadmin /RemoveClientCertificate <Job> 
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例

次の例では、クライアント証明書を削除という名前のジョブから*myJob*します。
```
C:\>Bitsadmin /RemoveClientCertificate myJob 
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)