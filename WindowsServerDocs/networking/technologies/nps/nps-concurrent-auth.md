---
title: NPS で処理する同時認証の数を増やす
description: このトピックでは、Windows Server 2016 でのネットワーク ポリシー サーバーの同時実行の認証の構成について説明します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 2d9cdada-0625-41c8-8248-a32259b03e47
ms.author: pashort
author: shortpatti
ms.openlocfilehash: fd930e34a4adf6c55812385b691df3e3575a4280
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818263"
---
# <a name="increase-concurrent-authentications-processed-by-nps"></a>NPS で処理する同時認証の数を増やす

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

ネットワーク ポリシー サーバーの同時実行の認証を構成する方法については、このトピックを使用できます。

ネットワーク ポリシー サーバーをインストールした場合\(NPS\)ドメイン以外のコンピューターでコント ローラーと NPS が受信して 1 秒あたりの認証要求の数が多いの数を増やすことで NPS のパフォーマンスを向上させることができます同時に行う認証、NPS およびドメイン コント ローラーの間で許可します。

これを行うには、次のレジストリ キーを編集する必要があります。 

`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Netlogon\Parameters`

という名前の新しい値を追加**MaxConcurrentApi** 2 ~ 5 の値を割り当てるとします。 

>[!CAUTION]
>値を割り当てる場合**MaxConcurrentApi**が多すぎますドメイン コント ローラーで、NPS が過剰な負荷をかける場合があります。

NPS の管理に関する詳細については、次を参照してください。[ネットワーク ポリシー サーバーの管理](nps-manage-top.md)します。

NPS の詳細については、次を参照してください。[ネットワーク ポリシー サーバー (NPS)](nps-top.md)します。