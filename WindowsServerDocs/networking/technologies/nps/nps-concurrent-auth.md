---
title: NPS で処理する同時認証を増やす
description: このトピックでは、Windows Server 2016 でのネットワーク ポリシー サーバーの同時認証の構成手順について説明します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 2d9cdada-0625-41c8-8248-a32259b03e47
ms.author: pashort
author: shortpatti
ms.openlocfilehash: aa70c1a26e2c22d26545e1b46a6151d71a2b4095
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="increase-concurrent-authentications-processed-by-nps"></a>NPS で処理する同時認証を増やす

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

同時認証のネットワーク ポリシー サーバーを構成する手順については、このトピックを使用できます。

ドメイン コントローラー以外のコンピューターでネットワーク ポリシー サーバー \(NPS\) がインストールされているし、NPS サーバーは 1 秒あたりの認証要求の数が多いを受信して、NPS サーバーとドメイン コントローラー間で許可する同時認証の数を増やすことで NPS のパフォーマンスを改善できます。

これを行うには、次のレジストリ キーを編集する必要があります。 

`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Netlogon\Parameters`

という名前の新しい値を追加**MaxConcurrentApi** 2. ~ 5. から値を割り当てるとします。 

>[!CAUTION]
>値を割り当てる場合**MaxConcurrentApi**が高すぎる、NPS サーバーは、ドメイン コントローラーに過剰な負荷を配置する可能性があります。

NPS の管理に関する詳細については、次を参照してください。[ネットワーク ポリシー サーバーの管理](nps-manage-top.md)します。

NPS の詳細については、次を参照してください。[ネットワーク ポリシー サーバー (NPS)](nps-top.md)します。