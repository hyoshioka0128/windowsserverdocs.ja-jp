---
title: AD FS 2016 で OpenID Connect または OAuth を使用する場合は、id_token に出力される要求をカスタマイズします。
description: AD FS 2016 でのカスタム id トークン conecpts の技術概要
author: anandyadavmsft
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.reviewer: anandy
ms.technology: identity-adfs
ms.openlocfilehash: 8c8e14f22a4bca5b6d32e841814a58a4b4ddca01
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820643"
---
# <a name="customize-claims-to-be-emitted-in-idtoken-when-using-openid-connect-or-oauth-with-ad-fs-2016"></a>AD FS 2016 で OpenID Connect または OAuth を使用する場合は、id_token に出力される要求をカスタマイズします。

## <a name="overview"></a>概要
記事[ここ](enabling-openId-connect-with-ad-fs.md)OpenID Connect のサインオン用に AD FS を使用するアプリをビルドする方法を示します。 ただし、既定では、id_token で使用できる要求の固定セットだけです。 AD FS 2016 では、OpenID Connect のシナリオで id_token をカスタマイズする機能があります。

## <a name="when-are-custom-id-token-used"></a>カスタム ID が場合に使用されるトークンですか?
特定のシナリオでは、クライアント アプリケーションにアクセスしようとするリソースがないことができます。 そのため、アクセス トークンは本当に必要ありません。 このような場合、クライアント アプリケーションには、のみ、ID トークンですがいくつか追加の要求のヘルプで、機能を本質的には必要があります。

## <a name="what-are-the-restrictions-on-getting-custom-claims-in-id-token"></a>ID でカスタム要求のトークンの取得に関する制限事項とは

### <a name="scenario-1"></a>例 1

![制限](media/Custom-Id-Tokens-in-AD-FS/res1.png)

1.  response_mode は form_post として設定します。
2.  パブリック クライアントのみで入手できますカスタム クレーム ID トークン
3.  証明書利用者のパーティの識別子をクライアント識別子と同じにする必要があります。

### <a name="scenario-2"></a>シナリオ 2

![制限](media/Custom-Id-Tokens-in-AD-FS/restrict2.png)

[KB4019472](https://support.microsoft.com/help/4019472/windows-10-update-kb4019472) AD FS サーバーにインストールされています。
1.  response_mode は form_post として設定します。
2.  クライアント-RP ペアには、スコープ allatclaims を割り当てます。
次の例に示すように Grant ADFSApplicationPermission コマンドレットを使用して、スコープを割り当てることができます。

``` powershell
Grant-AdfsApplicationPermission -ClientRoleIdentifier "https://my/privateclient" -ServerRoleIdentifier "https://rp/fedpassive" -ScopeNames "allatclaims","openid"
```

## <a name="creating-an-oauth-application-to-handle-custom-claims-in-id-token"></a>ID トークンのカスタム要求を処理するために OAuth アプリケーションを作成します。
アーティクルを使用して、[ここで](Enabling-OpenId-Connect-with-AD-FS-2016.md)OpenID Connect の AD FS のサインオンに使用するアプリケーションのアプリを作成します。 カスタム クレームと ID トークンを受信するための AD FS でアプリケーションを構成するのには、次の手順に従います。

### <a name="create-the-application-group-in-ad-fs-2016"></a>AD FS 2016 でのアプリケーション グループを作成します。

1.  CustomTokenClient と呼ばれる、次に示す、新しいテンプレートに基づくアプリケーション グループを作成します。

![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap1.png)

2. このテンプレートは、秘密のクライアントを作成します。 Id をメモし、VS プロジェクトの SSL URL として戻り値の URI を指定します。

![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap2.png)

3.  次の手順で選択**共有シークレットを生成**クライアント資格情報を作成し、生成されたクライアント資格情報をコピーします。

![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap3.png)

4. をクリックして**次**ウィザードを完了に進んでください。

![クライアント](media/Custom-Id-Tokens-in-AD-FS/clientsnap4.png)

### <a name="create-the-relying-party"></a>証明書利用者のパーティを作成します
ID でカスタム クレームを追加するためにトークンを作成する必要を RP のクレームは、ID トークンに追加される予定です。 次に示すように、新しい証明書利用者のパーティを作成するのにには、証明書利用者信頼の追加ウィザードを使用します。
 
![証明書利用者](media/Custom-Id-Tokens-in-AD-FS/rpsnap1.png)

証明書利用者が作成されると、証明書利用者のパーティのエントリを右クリックし、選択**要求発行ポリシーの編集**要求発行規則を追加します。 次に示すように、ID トークンに必要なカスタム クレームを追加します。

![証明書利用者](media/Custom-Id-Tokens-in-AD-FS/rpsnap2.png)

### <a name="assign-allatclaims-scope-to-the-pair-of-client-and-relying-party"></a>クライアントと証明書利用者のペアに"allatclaims"スコープを割り当てる
AD FS サーバーで PowerShell を使用して次の例で指定されている新しい allatclaims スコープを割り当てる (サーバーとクライアント Id を変更します。

``` powershell
Grant-AdfsApplicationPermission -ClientRoleIdentifier "5db77ce4-cedf-4319-85f7-cc230b7022e0" -ServerRoleIdentifier "https://customidrp1/" -ScopeNames "allatclaims","openid"
```

>[!NOTE]
>アプリケーションの設定に従い ClientRoleIdentifier および ServerRoleIdentifier を変更します。

## <a name="test-the-custom-claims-in-id-token"></a>ID トークン内のカスタム要求をテストします。

次に、常に要求へのアクセスに使用したコードの同じビットを使用して確認できます、id_token の一部となる追加の要求。
.NET MVC サンプル アプリケーションでは、コント ローラーのファイルのいずれかを開くのようなコードを入力するなどの下。


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
>Oauth2 要求にリソース パラメーターが必要なことに注意してください。
>
>不適切な使用例:
>
>**https&#58;//sts.contoso.com/adfs/oauth2/authorize?response_type=id_token & スコープ = openid & redirect_uri = https&#58;//myportal/auth & nonce = b3ceb943fc756d927777 & client_id = 6db3ec2a 075a-4 c 72 9b22 ca7ab60cb4e7(& a) の状態 = 42c2c156aef47e8d0870 & リソース 6db3ec2a 075a-4 c 72 9b22 ca7ab60cb4e7 を =**
>
>適切な例:
>
>**https&#58;//sts.contoso.com/adfs/oauth2/authorize?response_type=id_token & スコープ = openid & redirect_uri = https&#58;//myportal/auth & nonce = b3ceb943fc756d927777 & client_id = 6db3ec2a 075a-4 c 72 9b22 ca7ab60cb4e7(& a) の状態 = 42c2c156aef47e8d0870 & リソース = https&#58;//customidrp1/ & response_mode form_post を =**
>
>要求にリソース パラメーターがない場合、エラーまたはカスタムのクレームなしのトークンを受け取る可能性があります。

## <a name="next-steps"></a>次の手順
[AD FS の開発](../../ad-fs/AD-FS-Development.md)  
