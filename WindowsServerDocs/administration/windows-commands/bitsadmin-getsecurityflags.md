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
ms.openlocfilehash: 97d889b54c4b0de0230c50e1d7c8d21617ea881a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835853"
---
#<a name="bitsadmin-getsecurityflags"></a>bitsadmin getsecurityflags

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
[コマンドライン構文キー](command-line-syntax-key.md)


