---
title: 手順 3 の展開を確認します
description: このトピックは、「Windows Server 2016 用はじめにウィザードを使用して単一の DirectAccess サーバーを展開する」の一部です。
manager: brianlic
ms.topic: article
ms.assetid: 45e9edd6-acca-4d59-851a-a0cc8bd8b4c6
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 905daa32b8293fd1140b0bf6915b18ab16445bba
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87970329"
---
# <a name="step-3-verify-deployments"></a>手順 3 の展開を確認します

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、基本的な DirectAccess 展開が正しく構成されていることを確認する方法について説明します。

### <a name="to-verify-access-to-internal-resources-through-directaccess"></a>DirectAccess を通じた内部リソースへのアクセスを確認するには

1.  DirectAccess クライアント コンピューターを企業ネットワークに接続し、グループ ポリシーを取得します。

2.  通知領域の **[ネットワーク接続]** アイコンをクリックして、DA メディア マネージャーにアクセスします。

3.  **[DirectAccess 接続]** をクリックすると、状態が **[ローカル接続]** として表示されます。

4.  クライアント コンピューターを外部ネットワークに接続して、内部リソースへのアクセスを試行します。

    すべての企業リソースにアクセスできます。

## <a name="previous-step"></a><a name="BKMK_Links"></a>前の手順

-   [手順 2: DirectAccess サーバーを構成する](da-basic-configure-s2-server.md)



