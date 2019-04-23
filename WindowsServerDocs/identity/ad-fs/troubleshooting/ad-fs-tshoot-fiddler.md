---
title: AD FS のトラブルシューティング - Fiddler
description: このドキュメントは、Fiddler は、インストールして、AD FS の要求に関する問題をトラブルシューティングするように Fiddler を構成する方法について説明します。
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 03/02/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 822300d0e4b6ae462a3c942e22530bbed5f93e86
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865633"
---
# <a name="ad-fs-troubleshooting---fiddler"></a>AD FS のトラブルシューティング - Fiddler
Fiddler は、HTTP または HTTPS web トラフィックのキャプチャに使用できるツールです。  このツールは、要求の発行プロセスのトラブルシューティングで支援するために使用できます。  トラフィックを調べることで、相互作用を分割しての理解を深める取得できます。  このドキュメントは、インストール、AD FS のトラフィックをキャプチャするように Fiddler を設定する方法について説明します。  WS フェデレーションを使用してサンプル fiddler のトレースを参照してください[AD FS のトラブルシューティング - Fiddler - WS フェデレーション。](ad-fs-tshoot-fiddler-ws-fed.md)

## <a name="download-and-install-fiddler"></a>ダウンロードして Fiddler をインストールします。
Fiddler をダウンロードする[ここ](https://www.telerik.com/download/fiddler)します。  ダウンロードした後、進んであり、インストールします。

## <a name="configure-fiddler-to-capture-ad-fs-traffic"></a>AD FS のトラフィックをキャプチャするように Fiddler を構成します。
AD FS のトラフィックをキャプチャするためには、SSL トラフィックを復号化するように Fiddler を構成する必要があります。 

### <a name="configure-the-fiddler-ssl-certificate"></a>Fiddler の SSL 証明書を構成します。
 SSL トラフィックを復号化するのにように Fiddler をセットアップするのにには、次の手順を使用します。

1.  Fiddler を開く
2.  上部にある **ツール**を選択します**Fiddler オプション**します。
3.  [HTTPS] タブをクリックします。
4.  チェック ボックスをオン**復号化の HTTPS トラフィック**選択**ブラウザーのみから**ドロップダウン リストから。
5.  チェック ボックスをオンに**サーバー証明書のエラーを無視する**します。
6.  **[OK]** をクリックします。

![Fiddler](media/ad-fs-tshoot-fiddler/fiddler1.png)

## <a name="next-steps"></a>次の手順

- [AD FS のトラブルシューティング](ad-fs-tshoot-overview.md)