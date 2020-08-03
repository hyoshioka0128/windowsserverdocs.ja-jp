---
title: 手順 3. リモートアクセス (VPN) の展開を確認する
description: このトピックは、「Windows Server 2016 の既存のリモートアクセス (VPN) 展開に DirectAccess を追加する」の一部です。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: 43ac612e-2e77-418c-8171-ebb2086b7cb6
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 9eb64024eb7ad9b80a1ba8c949939b33426ad6da
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2020
ms.locfileid: "87518158"
---
# <a name="step-3-verify-the-remote-access-vpn-deployment"></a>手順 3. リモートアクセス (VPN) の展開を確認する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、DirectAccess 展開が正しく構成されていることを確認する方法について説明します。

### <a name="to-verify-access-to-internal-resources-through-directaccess"></a>DirectAccess を通じた内部リソースへのアクセスを確認するには

1.  DirectAccess クライアント コンピューターを企業ネットワークに接続し、グループ ポリシーを取得します。

2.  通知領域の **[ネットワーク接続]** アイコンをクリックして、DA メディア マネージャーにアクセスします。

3.  **[DirectAccess 接続]** をクリックすると、状態が **[ローカル接続]** として表示されます。

4.  クライアント コンピューターを外部ネットワークに接続して、内部リソースへのアクセスを試行します。

    すべての企業リソースにアクセスできます。



