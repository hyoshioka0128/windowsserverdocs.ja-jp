---
title: bitsadmin getsecurityflags
description: '**Bitsadmin getsecurityflags**の Windows コマンドトピックでは、転送中にサーバー証明書に対して実行される URL リダイレクトとチェックの HTTP セキュリティフラグを報告します。'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: fb53664a6366b411ae1eb9b0fe7c93392d60b542
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381461"
---
# <a name="bitsadmin-getsecurityflags"></a>bitsadmin getsecurityflags

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

転送中にサーバー証明書に対して実行された URL リダイレクトおよび確認の HTTP セキュリティフラグを報告します。

## <a name="syntax"></a>構文

```
bitsadmin /GetSecurityFlags <Job> 
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------|--------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例
次の例では、 *Myjob*という名前のジョブから securitly フラグを取得します。

```
C:\>bitsadmin /GetSecurityFlags myJob 
```

## <a name="additional-references"></a>その他の参照情報
[コマンド ライン構文の記号](command-line-syntax-key.md)


