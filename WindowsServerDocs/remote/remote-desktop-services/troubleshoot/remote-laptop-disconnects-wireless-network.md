---
title: リモート ラップトップがワイヤレス ネットワークから切断される
description: リモート ラップトップがワイヤレス ネットワークから切断される問題のトラブルシューティング。
audience: itpro
ms.custom: na
ms.reviewer: rklemen
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: troubleshooting
ms.assetid: ''
author: kaushika-msft
manager: dcscontentpm
ms.author: delhan
ms.date: 07/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: df43a69fa4777a9286cbe27cfa2d241111f7edf6
ms.sourcegitcommit: c5709021aa98abd075d7a8f912d4fd2263db8803
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/18/2020
ms.locfileid: "76265874"
---
# <a name="remote-laptop-disconnects-from-wireless-network"></a>リモート ラップトップがワイヤレス ネットワークから切断される

この問題は、リモート デスクトップ クライアントが 802.1x ワイヤレス ネットワークを使ってラップトップ コンピューターに接続しているときに、発生する可能性があります。 ラップトップがワイヤレス ネットワークから断続的に切断され、自動的には再接続しません。

これは、ワイヤレス ネットワーク接続に対するネットワーク認証の設定が**ユーザー認証**のときに発生する既知の問題です。

この問題を回避するには、ネットワーク認証の設定を **[ユーザーまたはコンピューターの認証]** または **[コンピューター認証]** に設定します。

 > [!NOTE]  
> 1 台のコンピューターでネットワーク認証の設定を変更するには、[ネットワークと共有センター] コントロール パネルを使って、新しい設定で新しいワイヤレス接続を作成することが必要な場合があります。

GPO を使ってワイヤレス ネットワーク設定を構成する方法について詳しくは、「[ワイヤレス ネットワークを構成する (IEEE 802.11) ポリシー](../../../networking/core-network-guide/cncg/wireless/e-wireless-access-deployment.md#bkmk_policies)」をご覧ください。
