---
title: nfsstat
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: da7a9768-44bd-404b-97ee-c388d00dc395
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9db8b903d4c3681b2b3bae3424f8af83696ae2c7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853293"
---
# <a name="nfsstat"></a>nfsstat



使用する **nfsstat** を表示または nfs サーバーへの呼び出しのカウントをリセットします。

## <a name="syntax"></a>構文

```
nfsstat [-z]
```

## <a name="description"></a>説明

せずに使用すると、 **~ z** オプション、 **nfsstat** コマンド ライン ユーティリティは、サービスの開始時、またはを使用して、カウンターがリセットされたときに、カウンターが 0 に設定された後にサーバーに加えられた NFS V2、NFS V3 およびマウント V3 の呼び出しの数を表示 **nfsstat z**します。