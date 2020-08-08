---
title: NPS で処理する同時認証の数を増やす
description: このトピックでは、Windows Server 2016 でネットワークポリシーサーバーの同時認証を構成する手順について説明します。
manager: brianlic
ms.topic: article
ms.assetid: 2d9cdada-0625-41c8-8248-a32259b03e47
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 2b21f357204ab61434bd12ba9121fb45dc84570f
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87969429"
---
# <a name="increase-concurrent-authentications-processed-by-nps"></a>NPS で処理する同時認証の数を増やす

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、ネットワークポリシーサーバーの同時認証を構成する手順について説明します。

ネットワークポリシーサーバー \( nps を \) ドメインコントローラー以外のコンピューターにインストールし、nps が1秒あたりに多数の認証要求を受信している場合は、nps とドメインコントローラー間で許可される同時認証の数を増やすことで、nps のパフォーマンスを向上させることができます。

これを行うには、次のレジストリキーを編集する必要があります。

`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Netlogon\Parameters`

**MaxConcurrentApi**という名前の新しい値を追加し、それに 2 ~ 5 の値を割り当てます。

>[!CAUTION]
>**MaxConcurrentApi**に値を割り当てた場合は、NPS によってドメインコントローラーに過剰な負荷がかかる可能性があります。

NPS の管理の詳細については、「 [Manage Network Policy Server](nps-manage-top.md)」を参照してください。

NPS の詳細については、「[ネットワークポリシーサーバー (nps)](nps-top.md)」を参照してください。