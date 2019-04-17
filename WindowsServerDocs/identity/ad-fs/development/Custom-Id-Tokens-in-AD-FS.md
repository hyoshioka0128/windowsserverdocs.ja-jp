---
title: "AD FS 2016 で OpenID 接続または OAuth を使用するときに、id_token に出力される要求をカスタマイズします。"
description: "AD FS 2016 でのカスタム ID トークン conecpts の技術概要"
author: anandyadavmsft
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.reviewer: anandy
ms.technology: identity-adfs
ms.openlocfilehash: c17d50bb6d90726eafc3e585f16a7a8189a68392
ms.sourcegitcommit: c16a2bf1b8a48ff267e71ff29f18b5e5cda003e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/28/2018
---
# <a name="customize-claims-to-be-emitted-in-idtoken-when-using-openid-connect-or-oauth-with-ad-fs-2016"></a>AD FS 2016 で OpenID 接続または OAuth を使用するときに、id_token に出力される要求をカスタマイズします。

## <a name="overview"></a>概要
The article [here](enabling-openId-connect-with-ad-fs.md) shows how to build an app that uses AD FS for OpenID Connect sign on. ただし、既定では、id_token で利用可能なクレームの固定セットのみです。 AD FS 2016 で OpenID 接続シナリオ id_token をカスタマイズする機能があります。

## <a name="when-are-custom-id-token-used"></a>カスタム ID がしたときに使用されるトークンですか?
特定のシナリオでことは、クライアント アプリケーションにアクセスしようとするリソースがないことです。 そのため、本当に必要はありません、アクセス トークン。 このような場合、クライアント アプリケーションには、のみ、ID トークンですが、機能のためにいくつか追加の信頼性情報と基本的に必要があります。

## <a name="what-are-the-restrictions-on-getting-custom-claims-in-id-token"></a>ID でカスタムの要求のトークンの取得に関する制限事項とは何ですか。

### <a name="scenario-1"></a>シナリオ 1

![制限します。](media/Custom-Id-Tokens-in-AD-FS/res1.png)

1.  response_mode が form_post として設定します。
2.  パブリック クライアントのみを取得できますカスタム要求 ID でトークン
3.  証明書利用者の識別子は、クライアント識別子と同じである必要があります。

### <a name="scenario-2"></a>シナリオ 2

![制限します。](media/Custom-Id-Tokens-in-AD-FS/restrict2.png)

[KB4019472](https://support.microsoft.com/help/4019472/windows-10-update-kb4019472)、AD FS サーバーにインストールされています。
1.  response_mode が form_post として設定します。
2.  クライアント – RP ペアにスコープ allatclaims を割り当てます。
次の例に示されている Grant-ADFSApplicationPermission コマンドレットを使用して、スコープを割り当てることができます。

``` powershell
Grant-AdfsApplicationPermission -ClientRoleIdentifier "https://my/privateclient" -ServerRoleIdentifier "https://rp/fedpassive" -ScopeNames "allatclaims","openid"
```

## <a name="creating-an-oauth-application-to-handle-custom-claims-in-id-token"></a>OAuth ID トークン内のカスタムの要求を処理するアプリケーションを作成します。
記事を使用して[次のとおり](Enabling-OpenId-Connect-with-AD-FS-2016.md)OpenID 接続の AD FS がサインオンを使用するアプリケーション アプリを作成します。 カスタムの信頼性情報と、ID トークンを受信するための AD FS で、アプリケーションを構成するには、次の手順に従います。

### <a name="create-the-application-group-in-ad-fs-2016"></a>AD FS 2016 でアプリケーション グループを作成します。

1.  CustomTokenClient と呼ばれる、以下に示す、新しいテンプレートに基づくアプリケーション グループを作成します。

![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap1.png)

2. このテンプレートでは、機密性の高いクライアントを作成します。 Id をメモし、VS プロジェクトの SSL URL として返される URI を指定します。

![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap2.png)

3.  次の手順で選択**共有シークレットを生成**クライアント資格情報を作成し、生成されたクライアントの資格情報をコピーします。

![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap3.png)

4. をクリックして**次**進んでウィザードを完了します。

![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap4.png)

### <a name="create-the-relying-party"></a>証明書利用者を作成します。
ID でカスタムの信頼性情報を追加するためにトークンを作成する必要が信頼性情報は、ID トークンに追加される RP します。 次に示すように、新しい証明書利用者を作成するのにには、証明書利用者信頼の追加ウィザードを使用します。
 
![証明書利用者](media/Custom-Id-Tokens-in-AD-FS/rpsnap1.png)

証明書利用者が作成されたら、証明書利用者のパーティ エントリを右クリックし、選択**要求発行ポリシーの編集**要求発行規則を追加します。 以下に示すように、ID トークンの必要なカスタムの信頼性情報を追加します。

![証明書利用者](media/Custom-Id-Tokens-in-AD-FS/rpsnap2.png)

### <a name="assign-allatclaims-scope-to-the-pair-of-client-and-relying-party"></a>クライアントと証明書利用者のペアに"allatclaims"スコープを割り当てる
PowerShell を使用して AD FS サーバーで、次の例で指定されている新しい allatclaims スコープを割り当てる (clientID とサーバーを変更します。

``` powershell
Grant-AdfsApplicationPermission -ClientRoleIdentifier "5db77ce4-cedf-4319-85f7-cc230b7022e0" -ServerRoleIdentifier "https://customidrp1/" -ScopeNames "allatclaims","openid"
```

>[!NOTE]
>アプリケーションの設定に従って ClientRoleIdentifier と ServerRoleIdentifier を変更します。

## <a name="test-the-custom-claims-in-id-token"></a>ID トークン内のカスタムの信頼性情報をテストします。

次に、常に信頼性情報にアクセスを使用したコードの同じビットを使用して、確認できます、id_token の一部となるその他の信頼性情報。
たとえば、.NET MVC サンプル アプリケーションでは、コントローラーのファイルの 1 つ開きを入力しますのようなコードの下。


``` code
    [Authorize]
    public ActionResult About()
    {

        ClaimsPrincipal cp = ClaimsPrincipal.Current;

        string userName = cp.FindFirst(ClaimTypes.GivenName).Value;
        ViewBag.Message = String.Format("Hello {0}!", userName);
        return View();

    }

```

>[!NOTE]
>Please be aware that the resource parameter is required in the Oauth2 request.
>
>Bad example:
>
>**https&#58;//sts.contoso.com/adfs/oauth2/authorize?response_type=id_token&scope=openid&redirect_uri=https&#58;//myportal/auth&nonce=b3ceb943fc756d927777&client_id=6db3ec2a-075a-4c72-9b22-ca7ab60cb4e7&state=42c2c156aef47e8d0870&resource=6db3ec2a-075a-4c72-9b22-ca7ab60cb4e7**
>
>Good example:
>
>**https&#58;//sts.contoso.com/adfs/oauth2/authorize?response_type=id_token&scope=openid&redirect_uri=https&#58;//myportal/auth&nonce=b3ceb943fc756d927777&client_id=6db3ec2a-075a-4c72-9b22-ca7ab60cb4e7&state=42c2c156aef47e8d0870&resource=https&#58;//customidrp1/**
>
>If the resource parameter is not in the request you may recieve an error or a token without any custom claims.

## <a name="next-steps"></a>次の手順
[AD FS の開発](../../ad-fs/AD-FS-Development.md)  