---
title: NPS で処理する同時認証の数を増やす
description: このトピックでは、Windows Server 2016 でネットワークポリシーサーバーの同時認証を構成する手順について説明します。
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 2d9cdada-0625-41c8-8248-a32259b03e47
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 5397a1de41717dfc65ee0b0582c1289c6a53b33a
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80316296"
---
# <a name="increase-concurrent-authentications-processed-by-nps"></a>NPS で処理する同時認証の数を増やす

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、ネットワークポリシーサーバーの同時認証を構成する手順について説明します。

ドメインコントローラー以外のコンピューターにネットワークポリシーサーバー \(NPS\) インストールし、NPS が1秒あたりに多数の認証要求を受信している場合は、nps とドメインコントローラー間で許可される同時認証の数を増やすことで、NPS のパフォーマンスを向上させることができます。

これを行うには、次のレジストリキーを編集する必要があります。 

`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Netlogon\Parameters`

**MaxConcurrentApi**という名前の新しい値を追加し、それに 2 ~ 5 の値を割り当てます。 

>[!CAUTION]
>**MaxConcurrentApi**に値を割り当てた場合は、NPS によってドメインコントローラーに過剰な負荷がかかる可能性があります。

NPS の管理の詳細については、「 [Manage Network Policy Server](nps-manage-top.md)」を参照してください。

NPS の詳細については、「[ネットワークポリシーサーバー (nps)](nps-top.md)」を参照してください。