---
title: AD FS のトラブルシューティング-Fiddler
description: このドキュメントでは、Fiddler の概要と、要求 AD FS の問題をトラブルシューティングするために Fiddler をインストールして構成する方法について説明します。
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 03/02/2018
ms.topic: article
ms.openlocfilehash: e631d9b1dd93b9f3eb3d224fa5e2007e3661e21c
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87972029"
---
# <a name="ad-fs-troubleshooting---fiddler"></a>AD FS のトラブルシューティング-Fiddler
Fiddler は、HTTP/HTTPS web トラフィックをキャプチャするために使用できるツールです。  このツールを使用すると、要求の発行プロセスのトラブルシューティングに役立てることができます。  トラフィックを確認することにより、相互作用がどこで妨げられているかについて理解を深めることができます。  このドキュメントでは、AD FS トラフィックをキャプチャするために Fiddler をインストールしてセットアップする方法について説明します。  WS-FEDERATION を使用した fiddler トレースの例については、「 [AD FS のトラブルシューティング-fiddler](ad-fs-tshoot-fiddler-ws-fed.md) 」を参照してください。

## <a name="download-and-install-fiddler"></a>Fiddler をダウンロードしてインストールする
Fiddler は[こちら](https://www.telerik.com/download/fiddler)からダウンロードできます。  ダウンロードが完了したら、それをインストールします。

## <a name="configure-fiddler-to-capture-ad-fs-traffic"></a>AD FS トラフィックをキャプチャするように Fiddler を構成する
AD FS トラフィックをキャプチャするには、SSL トラフィックの暗号化を解除するために Fiddler を構成する必要があります。

### <a name="configure-the-fiddler-ssl-certificate"></a>Fiddler SSL 証明書の構成
 SSL トラフィックの暗号化を解除するために Fiddler をセットアップするには、次の手順に従います。

1.  Fiddler を開きます
2.  上部の [**ツール**] で、[ **Fiddler Options**] を選択します。
3.  [HTTPS] タブをクリックします。
4.  **HTTPS トラフィックの暗号化を解除**するチェックボックスをオンにし、ドロップダウンから [**ブラウザーのみ**] を選択します。
5.  [**サーバー証明書エラーを無視**する] チェックボックスをオンにします。
6.  **[OK]** をクリックします。

![Fiddler](media/ad-fs-tshoot-fiddler/fiddler1.png)

## <a name="next-steps"></a>次の手順

- [AD FS のトラブルシューティング](ad-fs-tshoot-overview.md)