---
title: AD FS を使用した HTTP セキュリティ応答ヘッダーのカスタマイズ
description: このドキュメントでは、セキュリティの脆弱性から保護するためにセキュリティヘッダーをカスタマイズする方法を descirbes します。
author: billmath
ms.author: billmath
manager: daveba
ms.reviewer: akgoel23
ms.date: 02/19/2019
ms.topic: article
ms.openlocfilehash: 0984625564bfc6dabf8951fdcdf09fe76b0fcbdf
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87949706"
---
# <a name="customize-http-security-response-headers-with-ad-fs-2019"></a>AD FS 2019 で HTTP セキュリティ応答ヘッダーをカスタマイズする

一般的なセキュリティの脆弱性から保護するために、管理者はブラウザーベースの保護メカニズムの最新の機能強化を利用できるようにするために、AD FS によって送信された HTTP セキュリティ応答ヘッダーをカスタマイズする機能が追加されました 2019 AD FS。 これは、との2つの新しいコマンドレットの導入によって実現され `Get-AdfsResponseHeaders` `Set-AdfsResponseHeaders` ます。

>[!NOTE]
>コマンドレットを使用して HTTP セキュリティ応答ヘッダー (CORS ヘッダーを除く) をカスタマイズする機能: `Get-AdfsResponseHeaders` と `Set-AdfsResponseHeaders` は、AD FS 2016 に移植ました。 [KB4493473](https://support.microsoft.com/help/4493473/windows-10-update-kb4493473)と[KB4507459](https://support.microsoft.com/help/4507459/windows-10-update-kb4507459)をインストールすることによって、AD FS 2016 に機能を追加できます。

このドキュメントでは、一般的に使用されるセキュリティ応答ヘッダーについて説明し、AD FS 2019 によって送信されるヘッダーをカスタマイズする方法を示します。

>[!NOTE]
>このドキュメントでは、AD FS 2019 がインストールされていることを前提としています。


ヘッダーについて説明する前に、管理者がセキュリティヘッダーをカスタマイズする必要があるいくつかのシナリオを見てみましょう。

## <a name="scenarios"></a>シナリオ
1. 管理者は、 [**Http Strict-Transport-Security (HSTS)**](#http-strict-transport-security-hsts)を有効にしています (HTTPS 暗号化経由のすべての接続を強制します)。これにより、ハッキングされる可能性のあるパブリック wifi アクセスポイントから http を使用して web アプリにアクセスする可能性があるユーザーを保護できます。 また、サブドメインの HSTS を有効にすることで、セキュリティをさらに強化したいと考えています。
2. 管理者が、web ページの clickjacked を防ぐために、 [**X フレームオプション**](#x-frame-options)の応答ヘッダーを構成しました (iFrame に web ページが表示されないようにします)。 ただし、新しいビジネス要件によって、異なるオリジン (ドメイン) を持つアプリケーションからデータ (iFrame) を表示する必要があるため、ヘッダー値をカスタマイズする必要があります。
3. 管理者は[**、クロス**](#x-xss-protection)スクリプティング攻撃を検出した場合に、クロススクリプティング攻撃を防止し、ページをブロックすることを許可しています。 ただし、このような場合は、ヘッダーをカスタマイズして、校正後にページを読み込むことができるようにする必要があります。
4. 管理者は、[**クロスオリジンリソース共有 (CORS)**](#cross-origin-resource-sharing-cors-headers)を有効にし、AD FS の配信元 (ドメイン) を設定して、単一ページアプリケーションが別のドメインで web API にアクセスできるようにする必要があります。
5. 管理者は、クロスサイトスクリプトとデータインジェクション攻撃を防止するために、[**コンテンツセキュリティポリシー (CSP)**](#content-security-policy-csp)ヘッダーを有効にしています。これにより、クロスドメイン要求が禁止されます。 ただし、新しいビジネス要件により、web ページが任意の配信元からイメージを読み込んで、メディアを信頼できるプロバイダーに制限するように、ヘッダーをカスタマイズする必要があります。


## <a name="http-security-response-headers"></a>HTTP セキュリティ応答ヘッダー
応答ヘッダーは、AD FS によって web ブラウザーに送信される発信 HTTP 応答に含まれます。 次に示すように、コマンドレットを使用してヘッダーを表示でき `Get-AdfsResponseHeaders` ます。

![ヘッダー応答](media/customize-http-security-headers-ad-fs/header1.png)

`ResponseHeaders`上のスクリーンショットの属性は、すべての HTTP 応答で AD FS によって含まれるセキュリティヘッダーを識別します。 応答ヘッダーは、 `ResponseHeadersEnabled` が (既定値) に設定されている場合にのみ送信され `True` ます。 この値をに設定すると、 `False` HTTP 応答にセキュリティヘッダーのいずれかを含め AD FS を防ぐことができます。 ただし、これは推奨されません。  これを行うには、次のようにします。

```PowerShell
Set-AdfsResponseHeaders -EnableResponseHeaders $false
```

### <a name="http-strict-transport-security-hsts"></a>HTTP Strict-Transport-Security (HSTS)
HSTS は、HTTP と HTTPS の両方のエンドポイントを持つサービスのプロトコルダウングレード攻撃や cookie ハイジャックを軽減するための web セキュリティポリシーメカニズムです。 それを使用すると、Web サーバーで、Web ブラウザー (または他の準拠ユーザー エージェント) は HTTPS のみを使用して対話し、HTTP プロトコルを使用してはならないことを宣言できます。

Web 認証トラフィック用のすべての AD FS エンドポイントは、HTTPS 経由専用に開かれます。 その結果、AD FS http Strict Transport セキュリティポリシー機構が提供する脅威を効果的に軽減できます (http にリスナーが存在しないため、既定では HTTP へのダウングレードは行われません)。 ヘッダーをカスタマイズするには、次のパラメーターを設定します。

- **最長有効期間 = &lt; 有効期限- &gt; **有効期限 (秒) は、HTTPS を使用してのみサイトにアクセスする必要がある期間を指定します。 既定値と推奨値は31536000秒 (1 年) です。
- **includeSubDomains** –これは省略可能なパラメーターです。 指定した場合、HSTS ルールもすべてのサブドメインに適用されます。

#### <a name="hsts-customization"></a>HSTS のカスタマイズ
既定では、ヘッダーが有効になり、 `max-age` 1 年に設定されます。ただし、管理者は、 `max-age` (最長有効期間の値を減らすことは推奨されません) を変更することも、コマンドレットを使用してサブドメインの hsts を有効にすることもでき `Set-AdfsResponseHeaders` ます。

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "Strict-Transport-Security" -SetHeaderValue "max-age=<seconds>; includeSubDomains"
```

例:

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "Strict-Transport-Security" -SetHeaderValue "max-age=31536000; includeSubDomains"
 ```

既定では、ヘッダーは属性に含まれていますが、 `ResponseHeaders` 管理者はコマンドレットを使用してヘッダーを削除できます。 `Set-AdfsResponseHeaders`

```PowerShell
Set-AdfsResponseHeaders -RemoveHeaders "Strict-Transport-Security"
```

### <a name="x-frame-options"></a>X フレームオプション
AD FS 既定では、対話型ログインの実行時に外部アプリケーションが Iframe を使用することはできません。 これは、特定のスタイルのフィッシング攻撃を防ぐために行われます。 以前のセッションレベルのセキュリティが確立されているため、iFrame を使用して非対話型ログインを実行できることに注意してください。

ただし、まれに、iFrame 対応の対話型 AD FS ログインページを必要とする特定のアプリケーションを信頼する場合があります。 この目的では、' X-Frame オプション ' ヘッダーが使用されます。

この HTTP セキュリティ応答ヘッダーは、フレーム iframe でページを表示できるかどうかをブラウザーに通知するために使用され &lt; &gt; / &lt; &gt; ます。 ヘッダーは、次のいずれかの値に設定できます。

- **拒否**–フレーム内のページは表示されません。 これは既定の推奨設定です。
- **sameorigin** –原点が web ページの配信元と同じ場合にのみ、ページがフレームに表示されます。 このオプションは、すべての先祖が同じオリジンに含まれていない限り、あまり役に立ちません。
- **許可-開始 <specified origin> **-元の場合、ページはフレームにのみ表示されます (例 https://www :. ")。com) は、ヘッダー内の特定のオリジンと一致します。 これは、制限付きブラウザーでサポートされている場合があります。

#### <a name="x-frame-options-customization"></a>X フレームオプションのカスタマイズ
既定では、ヘッダーは [拒否] に設定されます。ただし、管理者はコマンドレットを使用して値を変更でき `Set-AdfsResponseHeaders` ます。
```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "X-Frame-Options" -SetHeaderValue "<deny/sameorigin/allow-from<specified origin>>"
 ```

例:

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "X-Frame-Options" -SetHeaderValue "allow-from https://www.example.com"
 ```

既定では、ヘッダーは属性に含まれていますが、 `ResponseHeaders` 管理者はコマンドレットを使用してヘッダーを削除できます。 `Set-AdfsResponseHeaders`

```PowerShell
Set-AdfsResponseHeaders -RemoveHeaders "X-Frame-Options"
```

### <a name="x-xss-protection"></a>X-XSS-保護
この HTTP セキュリティ応答ヘッダーは、クロスサイトスクリプティング (XSS) 攻撃がブラウザーによって検出されたときに、web ページの読み込みを停止するために使用されます。 これは XSS フィルターと呼ばれます。 ヘッダーは、次のいずれかの値に設定できます。

- **0** : XSS フィルター処理を無効にします。 推奨されません。
- **1** : XSS フィルター処理を有効にします。 XSS 攻撃が検出されると、ブラウザーによってページがサニタイズされます。
- **1; mode = block** – XSS フィルターを有効にします。 XSS 攻撃が検出されると、ブラウザーはページのレンダリングを防止します。 これは既定の推奨設定です。

#### <a name="x-xss-protection-customization"></a>X-XSS-保護のカスタマイズ
既定では、ヘッダーは1に設定されます。mode = block;ただし、管理者はコマンドレットを使用して値を変更でき `Set-AdfsResponseHeaders` ます。

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "X-XSS-Protection" -SetHeaderValue "<0/1/1; mode=block/1; report=<reporting-uri>>"
```

例:

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "X-XSS-Protection" -SetHeaderValue "1"
 ```

既定では、ヘッダーは属性に含まれていますが、 `ResponseHeaders` 管理者はコマンドレットを使用してヘッダーを削除できます。 `Set-AdfsResponseHeaders`

```PowerShell
Set-AdfsResponseHeaders -RemoveHeaders "X-XSS-Protection"
```

### <a name="cross-origin-resource-sharing-cors-headers"></a>クロスオリジンリソース共有 (CORS) ヘッダー
Web ブラウザーのセキュリティにより、web ページはスクリプト内からのクロスオリジン要求を実行できなくなります。 ただし、場合によっては、他のオリジン (ドメイン) 内のリソースにアクセスすることが必要になることがあります。 CORS は、サーバーが同じオリジンポリシーを緩めることを可能にする W3C 標準です。 CORS を使用することで、サーバーが一部のクロス オリジン要求を、その他の要求を拒否しながら、明示的に許可することができます。

CORS 要求について理解を深めるために、単一ページアプリケーション (SPA) が別のドメインで web API を呼び出す必要があるシナリオについて説明します。 さらに、SPA と API の両方が ADFS 2019 で構成されている AD FS、CORS が有効になっていることを考えてみましょう。 AD FS では、HTTP 要求で CORS ヘッダーを識別し、ヘッダー値を検証し、適切な CORS ヘッダーを応答に含めることができます (以下の CORS カスタマイズセクションで、AD FS 2019 で CORS を有効にし サンプルフロー:

1. ユーザーは、クライアントブラウザーから SPA にアクセスし、認証のために AD FS 認証エンドポイントにリダイレクトされます。 SPA は暗黙的な許可フロー用に構成されているため、認証が成功した後に、要求からブラウザーにアクセス + ID トークンが返されます。
2. ユーザー認証の後、SPA に含まれるフロントエンド JavaScript は、web API へのアクセスを要求します。 要求は、次のヘッダーを使用して AD FS にリダイレクトされます。
    - オプション–ターゲットリソースの通信オプションについて説明します。
    - Origin – web API の配信元が含まれます。
    - アクセス制御要求-メソッド–実際の要求が行われたときに使用される HTTP メソッド (例: DELETE) を識別します。
    - アクセス制御-要求ヘッダー-実際の要求が行われたときに使用される HTTP ヘッダーを識別します。

   >[!NOTE]
   >CORS 要求は標準の HTTP 要求に似ていますが、オリジンヘッダーが存在すると、受信要求が CORS 関連であることが通知されます。
3. AD FS は、ヘッダーに含まれる web API オリジンが AD FS で構成された信頼できる発行元に一覧表示されていることを確認します (以下の CORS カスタマイズセクションで、信頼されたオリジンを変更する方法の詳細)。 AD FS は、次のヘッダーで応答します。
    - アクセス制御-元に戻す-元のヘッダーと同じ値
    - アクセス制御-許可-メソッド–値は、アクセス制御要求メソッドのヘッダーと同じです
    - アクセス制御-許可ヘッダー-値は、アクセス制御ヘッダーヘッダーと同じです。
4. ブラウザーは、次のヘッダーを含む実際の要求を送信します。
    - HTTP メソッド (例、DELETE)
    - Origin – web API の配信元が含まれます。
    - アクセス制御-許可ヘッダー応答ヘッダーに含まれるすべてのヘッダー
5. 検証が完了すると、AD FS web API ドメイン (オリジン) をアクセス制御-許可元の応答ヘッダーに含めて、要求を承認します。
6. アクセス制御-許可元ヘッダーを含めることで、ブラウザーは要求された API を呼び出すことができます。

#### <a name="cors-customization"></a>CORS のカスタマイズ
既定では、CORS 機能は有効になりません。ただし、管理者は AdfsResponseHeaders コマンドレットを使用して機能を有効にすることができます。

```PowerShell
Set-AdfsResponseHeaders -EnableCORS $true
 ```

1つの有効な管理者は、同じコマンドレットを使用して、信頼されたオリジンの一覧を列挙できます。 たとえば、次のコマンドは、オリジン**https&#58;//example1.com**と**https&#58;//EXAMPLE1.COM**からの CORS 要求を許可します。

```PowerShell
Set-AdfsResponseHeaders -CORSTrustedOrigins https://example1.com,https://example2.com
 ```

> [!NOTE]
> 管理者は、信頼された元のリストに "*" を含めることで、任意の発信元からの CORS 要求を許可できます。ただし、セキュリティ上の脆弱性により、この方法は推奨されません。また、ユーザーが選択した場合は警告メッセージが表示されます。

### <a name="content-security-policy-csp"></a>コンテンツセキュリティポリシー (CSP)
この HTTP セキュリティ応答ヘッダーは、ブラウザーによって悪意のあるコンテンツが誤って実行されないようにすることで、クロスサイトスクリプト作成、jack、およびその他のデータインジェクション攻撃を防ぐために使用されます。 CSP をサポートしていないブラウザーは、単に CSP 応答ヘッダーを無視します。

#### <a name="csp-customization"></a>CSP のカスタマイズ
CSP ヘッダーをカスタマイズする場合は、ブラウザーで web ページの読み込みを許可するリソースを定義するセキュリティポリシーを変更します。 既定のセキュリティポリシーは、

`Content-Security-Policy: default-src ‘self' ‘unsafe-inline' ‘'unsafe-eval'; img-src ‘self' data:;`

**既定の-src**ディレクティブは、各ディレクティブを明示的に指定せずに[-src ディレクティブ](https://developer.mozilla.org/docs/Web/HTTP/Headers/Content-Security-Policy/default-src)を変更するために使用されます。 たとえば、次の例では、ポリシー1はポリシー2と同じです。

ポリシー 1
```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "Content-Security-Policy" -SetHeaderValue "default-src 'self'"
```

ポリシー 2
```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "Content-Security-Policy" -SetHeaderValue "script-src ‘self'; img-src ‘self'; font-src 'self';
frame-src 'self'; manifest-src 'self'; media-src 'self';"
```

ディレクティブが明示的に指定されている場合、指定された値は、既定の-src に指定された値よりも優先されます。 次の例では、img-src は値を ' * ' として受け取ります (任意のオリジンからイメージを読み込むことができます)。他の src ディレクティブは、値を ' self ' として受け取ります (web ページと同じオリジンに限定されます)。

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "Content-Security-Policy" -SetHeaderValue "default-src ‘self'; img-src *"
```
既定の src ポリシーには、次のソースを定義できます。

- ' self ' –これを指定すると、web ページの配信元に読み込むコンテンツの配信元が制限されます。
- ' unsafe ' インライン ' –ポリシーでこれを指定すると、インライン JavaScript と CSS を使用できます。
- ' unsafe-eval ' –ポリシーでこれを指定すると、eval のような JavaScript 機構でテキストを使用できます。
- none: これを指定すると、配信元からのコンテンツの読み込みが制限されます。
- data:-data: Uri を指定すると、コンテンツ作成者はドキュメントに小さなファイルをインラインで埋め込むことができます。 使用しないことをお勧めします。

>[!NOTE]
>AD FS は、認証プロセスで JavaScript を使用するため、既定のポリシーに ' unsafe ' インライン ' と ' unsafe-eval ' ソースを含めることで JavaScript を有効にします。

### <a name="custom-headers"></a>カスタム ヘッダー
上記のセキュリティ応答ヘッダー (HSTS、CSP、X フレームオプション、X-XSS-Protection、CORS) に加えて、AD FS 2019 は新しいヘッダーを設定する機能を提供します。

例: 新しいヘッダー "TestHeader" を値を "TestHeaderValue" に設定するには

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "TestHeader" -SetHeaderValue "TestHeaderValue"
 ```

設定すると、新しいヘッダーが AD FS 応答 (下の fiddler スニペット) で送信されます。

![Fiddler](media/customize-http-security-headers-ad-fs/header2.png)

## <a name="web-browser-compatibility"></a>Web ブラウザーの互換性
次の表とリンクを使用して、各セキュリティ応答ヘッダーと互換性のある web ブラウザーを特定します。

|HTTP セキュリティ応答ヘッダー|ブラウザーの互換性|
|-----|-----|
|HTTP Strict-Transport-Security (HSTS)|[HSTS ブラウザーの互換性](https://developer.mozilla.org/docs/Web/HTTP/Headers/Strict-Transport-Security#Browser_compatibility)|
|X フレームオプション|[X フレームオプションブラウザーの互換性](https://developer.mozilla.org/docs/Web/HTTP/Headers/X-Frame-Options#Browser_compatibility)|
|X-XSS-保護|[X-XSS-保護ブラウザーの互換性](https://developer.mozilla.org/docs/Web/HTTP/Headers/X-XSS-Protection#Browser_compatibility)|
|クロスオリジン リソース共有 (CORS)|[CORS ブラウザーの互換性](https://developer.mozilla.org/docs/Web/HTTP/CORS#Browser_compatibility)
|コンテンツセキュリティポリシー (CSP)|[CSP ブラウザーの互換性](https://developer.mozilla.org/docs/Web/HTTP/CSP#Browser_compatibility)

## <a name="next"></a>次へ

- [AD FS ヘルプトラブルシューティングガイドを使用する](https://aka.ms/adfshelp/troubleshooting )
- [AD FS のトラブルシューティング](../../ad-fs/troubleshooting/ad-fs-tshoot-overview.md)
