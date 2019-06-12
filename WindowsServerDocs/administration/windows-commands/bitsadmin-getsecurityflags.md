---
title: bitsadmin getsecurityflags
description: Windows コマンド」のトピック**bitsadmin getsecurityflags** - URL のリダイレクトの HTTP セキュリティ フラグをレポートし、転送中に実行されるサーバーの証明書を確認します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c2e73519-34f4-487b-af11-97d5d08ef9bb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6e1db167b12d47afccb8842da617f1e9fe72acff
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434962"
---
# <a name="bitsadmin-getsecurityflags"></a>bitsadmin getsecurityflags

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

URL リダイレクトとチェックのレポート、HTTP セキュリティ フラグは、転送中にサーバー証明書に対して実行します。

## <a name="syntax"></a>構文

```
bitsadmin /GetSecurityFlags <Job> 
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------|--------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例
次の例では、securitly フラグを取得という名前のジョブから*myJob*します。

```
C:\>bitsadmin /GetSecurityFlags myJob 
```

## <a name="additional-references"></a>その他の参照
[コマンド ライン構文の記号](command-line-syntax-key.md)


