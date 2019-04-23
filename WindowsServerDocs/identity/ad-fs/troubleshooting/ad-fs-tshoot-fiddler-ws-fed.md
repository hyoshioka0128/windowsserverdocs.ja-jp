---
title: AD FS のトラブルシューティング - Fiddler - WS フェデレーション
description: このドキュメントでは、AD FS を使用した WS フェデレーション exchange の詳細なトレースを示しています。
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/18/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: be1c9f466ec13272d10f0fb9ca31cf326a1ec29a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59846903"
---
# <a name="ad-fs-troubleshooting---fiddler---ws-federation"></a>AD FS のトラブルシューティング - Fiddler - WS フェデレーション
![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler9.png)

## <a name="step-1-and-2"></a>手順 1. および 2.
これは、トレースの開始です。  このフレームで、次のわかります。 ![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler1.png)

要求:

- HTTP GET を証明書利用者のパーティ (http://sql1.contoso.com/SampApp)

応答:

- 応答は、HTTP 302 (リダイレクトです)。  トランスポートの応答ヘッダーでのデータが (にリダイレクトする場所を示しています https://sts.contoso.com/adfs/ls)
- リダイレクト URL には、wa が含まれています。 = wsignin 1.0、RP アプリケーションが私たちの Ws-federation サインイン要求を構築し、これを、AD FS の/adfs/ls/エンドポイントに送信されることが示されます。  これはバインディングのリダイレクトと呼ばれます。
![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler2.png)

## <a name="step-3-and-4"></a>手順 3 と 4

![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler3.png)

要求:

- HTTP GET を AD FS server(sts.contoso.com)

応答:

- 応答では、資格情報のプロンプトです。  これは、フォーム ケルベロスが使用されていることを示します。
- 応答の web ビューをクリックして、資格情報プロンプトを表示できます。
![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler6.png)

## <a name="step-5-and-6"></a>手順 5 と 6

![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler4.png)

要求:

- ユーザー名とパスワードは、HTTP POST します。  
- この資格情報をご紹介します。  要求に生データを調べることで、資格情報を確認できます。

応答:

- 応答が見つかりましたが、MSIAuth 暗号化された cookie が作成され、返されます。  これは、クライアントによって生成された SAML アサーションの検証に使用されます。  これは、"認証の cookie"でとも呼ばれますでありにのみ、Idp が AD FS に表示されます。


## <a name="step-7-and-8"></a>手順 7 ~ 8
![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler5.png)

要求:

- AD FS サーバーに、別の HTTP GET を実行し、認証トークンを提示できたので認証済み

応答:

- 応答は、AD FS が指定された資格情報に基づいてユーザーを認証されていることを意味する HTTP OK
- また、クライアントに 3 つの cookie を設定します。
    - MSISAuthenticated には、クライアントが認証されたときのタイムスタンプの base64 でエンコードされた値が含まれています。
    - MSISLoopDetectionCookie は、フェデレーション サーバーに無限のリダイレクト ループ終了したする停止のクライアントが AD FS の無限ループ検出メカニズムによって使用されます。 Cookie のデータは、base64 でエンコードされているタイムスタンプです。
    - MSISSignout は IdP を追跡するのに使用され、SSO セッションのすべての Rp にアクセスします。 この cookie は、Ws-federation のサインアウトが呼び出されたときに利用します。 Base64 デコーダーを使用して、この cookie の内容を確認できます。
    
## <a name="step-9-and-10"></a>手順 9 および 10
![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler7.png) 要求:

- HTTP POST

応答:

- 応答が見つかりました

## <a name="step-11-and-12"></a>手順 11. と 12.
![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler8.png) 要求:

- HTTP GET

応答:

- 応答は、[ok]

## <a name="next-steps"></a>次の手順

- [AD FS のトラブルシューティング](ad-fs-tshoot-overview.md)