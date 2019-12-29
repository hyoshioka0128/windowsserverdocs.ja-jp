---
title: AD FS のトラブルシューティング-Fiddler
description: このドキュメントでは、WS-FEDERATION exchange と AD FS の詳細なトレースについて説明します。
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/18/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: d263f48aadff7c77cba44a2328d472ebbe5dfbbf
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407216"
---
# <a name="ad-fs-troubleshooting---fiddler---ws-federation"></a>AD FS のトラブルシューティング-Fiddler
![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler9.png)

## <a name="step-1-and-2"></a>手順 1. と 2.
これは、トレースの開始です。  このフレームには、次のように表示されます。 ![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler1.png)

要求:

- 証明書利用者への HTTP GET (http://sql1.contoso.com/SampApp)

応答

- 応答は HTTP 302 (リダイレクト) です。  応答ヘッダーのトランスポートデータは、リダイレクト先を示しています (https://sts.contoso.com/adfs/ls)
- リダイレクト URL には、wa = wsignin 1.0 が含まれています。これは、RP アプリケーションが WS-FEDERATION サインイン要求を構築し、これを AD FS の/adfs/ls/エンドポイントに送信したことを示します。  これはリダイレクトバインドと呼ばれます。
![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler2.png)

## <a name="step-3-and-4"></a>手順 3. と 4.

![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler3.png)

要求:

- HTTP GET AD FS サーバー (sts. contoso .com)

応答

- 応答は、資格情報の入力を求められます。  これは、フォーム authnetication を使用していることを示します。
- 応答の WebView をクリックすると、資格情報プロンプトが表示されます。
![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler6.png)

## <a name="step-5-and-6"></a>手順 5. および 6.

![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler4.png)

要求:

- ユーザー名とパスワードを使用した HTTP POST。  
- 資格情報を提示します。  要求の生データを見ると、資格情報が表示されます。

応答

- 応答が見つかり、MSIAuth で暗号化された cookie が作成されて返されます。  これは、クライアントによって作成された SAML アサーションを検証するために使用されます。  これは "authentication cookie" とも呼ばれ、AD FS が Idp の場合にのみ存在します。


## <a name="step-7-and-8"></a>手順 7. および 8.
![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler5.png)

要求:

- 認証が完了したので、AD FS サーバーに対して別の HTTP GET を実行し、認証トークンを提示します。

応答

- 応答は、指定された資格情報に基づいてユーザーを認証した AD FS であることを示す HTTP OK です。
- また、3つの cookie をクライアントに戻します。
    - MSISAuthenticated は、クライアントが認証されたときに、base64 でエンコードされたタイムスタンプ値を格納します。
    - MSISLoopDetectionCookie は、無限ループ検出メカニズムによって、フェデレーションサーバーへの無限のリダイレクトループで終了したクライアントを停止するために AD FS 使用されます。 Cookie データは、base64 でエンコードされたタイムスタンプです。
    - MSISSignout は、SSO セッションに対してアクセスされた IdP とすべての RPs を追跡するために使用されます。 このクッキーは、WS-FEDERATION サインアウトが呼び出されたときに使用されます。 Base64 デコーダーを使用して、この cookie の内容を表示できます。
    
## <a name="step-9-and-10"></a>手順 9. および 10.
![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler7.png) 要求:

- HTTP POST

応答

- 応答が見つかりました

## <a name="step-11-and-12"></a>手順 11. と 12.
![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler8.png) 要求:

- HTTP GET

応答

- 応答は OK です。

## <a name="next-steps"></a>次の手順

- [AD FS のトラブルシューティング](ad-fs-tshoot-overview.md)