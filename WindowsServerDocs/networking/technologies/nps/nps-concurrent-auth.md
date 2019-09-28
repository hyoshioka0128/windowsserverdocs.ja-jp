---
title: NPS で処理する同時認証の数を増やす
description: このトピックでは、Windows Server 2016 でネットワークポリシーサーバーの同時認証を構成する手順について説明します。
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 2d9cdada-0625-41c8-8248-a32259b03e47
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 31dec30ba3c843b78974daa7a1e4ed6893b1ebbd
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71396432"
---
# <a name="increase-concurrent-authentications-processed-by-nps"></a>NPS で処理する同時認証の数を増やす

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、ネットワークポリシーサーバーの同時認証を構成する手順について説明します。

ドメインコントローラー以外のコンピューターにネットワークポリシーサーバー \(NPS @ no__t-1 をインストールし、NPS が1秒あたりに多数の認証要求を受信している場合は、同時実行の数を増やすことで NPS のパフォーマンスを向上させることができます。NPS とドメインコントローラー間の認証が許可されます。

これを行うには、次のレジストリキーを編集する必要があります。 

`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Netlogon\Parameters`

**MaxConcurrentApi**という名前の新しい値を追加し、それに 2 ~ 5 の値を割り当てます。 

>[!CAUTION]
>**MaxConcurrentApi**に値を割り当てた場合は、NPS によってドメインコントローラーに過剰な負荷がかかる可能性があります。

NPS の管理の詳細については、「 [Manage Network Policy Server](nps-manage-top.md)」を参照してください。

NPS の詳細については、「[ネットワークポリシーサーバー (nps)](nps-top.md)」を参照してください。