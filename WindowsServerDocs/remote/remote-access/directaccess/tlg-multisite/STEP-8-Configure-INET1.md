---
title: 手順 8. INET1 を構成する
description: このトピックは、「Windows Server 2016 用の DirectAccess マルチサイト展開のテストラボガイド」の一部です。
manager: brianlic
ms.topic: article
ms.assetid: 693acb5c-dffc-4484-8286-163bb67724c9
ms.author: coreyp
author: coreyp-at-msft
ms.openlocfilehash: 2e53eb8af7327932123fde8eb138611e5ae65242
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87953678"
---
# <a name="step-8-configure-inet1"></a>手順 8: INET1 を構成する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

クライアントコンピューターがインターネット経由でリモートアクセスサーバーに接続できるようにするには、INET1 で EDGE1 の DNS エントリを構成する必要があります。

### <a name="to-create-the-2-edge1-dns-entry"></a>2 EDGE1 DNS エントリを作成するには

1.  **スタート**画面で「**dnsmgmt.msc**」と入力し、enter キーを押します。

2.  コンソールツリーで、[**前方参照ゾーン**] を開き、[ **contoso.com**] をクリックします。次に、[ **contoso.com**] を右クリックし、[**新しいホスト (A または AAAA)**] をクリックします。

3.  [**名前**] に「 **2-EDGE1**」と入力します。 [ **IP アドレス**] に、「 **131.107.0.20**」と入力します。 [**ホストの追加**] をクリックし、[**OK**] をクリックして、[**完了**] をクリックします。



