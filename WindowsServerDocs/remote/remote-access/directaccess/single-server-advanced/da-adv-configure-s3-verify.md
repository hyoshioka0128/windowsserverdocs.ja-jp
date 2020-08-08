---
title: 手順 3-高度な DirectAccess 展開を確認する
description: このトピックは、「Windows Server 2016 の詳細設定を使用して単一の DirectAccess サーバーを展開する」の一部です。
manager: brianlic
ms.topic: article
ms.assetid: ae8bbff0-c981-4bc6-8df1-861621d0627f
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 3d5b189d70497ead26f24f43bba9dcfe2d443ce0
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87989762"
---
# <a name="step-3-verify-the-advanced-directaccess-deployment"></a>手順 3-高度な DirectAccess 展開を確認する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、DirectAccess 展開が正しく構成されていることを確認する方法について説明します。

### <a name="to-verify-access-to-internal-resources-through-directaccess"></a>DirectAccess を通じた内部リソースへのアクセスを確認するには

1.  DirectAccess クライアントコンピューターを企業ネットワークに接続し、グループポリシーオブジェクトを取得します。

2.  通知領域の [**ネットワーク接続**] アイコンをクリックして、DirectAccess メディアマネージャーにアクセスします。

3.  [ **DirectAccess 接続**] をクリックすると、状態が**ローカルに接続**されていることがわかります。

4.  クライアント コンピューターを外部ネットワークに接続して、内部リソースへのアクセスを試行します。

    すべての企業リソースにアクセスできます。

## <a name="previous-step"></a><a name="BKMK_Links"></a>前の手順

-   [手順 2: DirectAccess サーバーの構成](./da-adv-configure-s2-servers.md)