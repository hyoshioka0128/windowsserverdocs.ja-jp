---
title: nfsstat
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: da7a9768-44bd-404b-97ee-c388d00dc395
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 94eb389fdd694c08dcd1d77325f145a81e59ea0f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80838885"
---
# <a name="nfsstat"></a>nfsstat



使用する **nfsstat** を表示または nfs サーバーへの呼び出しのカウントをリセットします。

## <a name="syntax"></a>構文

```
nfsstat [-z]
```

## <a name="description"></a>説明

せずに使用すると、 **~ z** オプション、 **nfsstat** コマンド ライン ユーティリティは、サービスの開始時、またはを使用して、カウンターがリセットされたときに、カウンターが 0 に設定された後にサーバーに加えられた NFS V2、NFS V3 およびマウント V3 の呼び出しの数を表示 **nfsstat z**します。