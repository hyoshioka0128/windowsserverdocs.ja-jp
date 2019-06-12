---
title: AD FS を使用した HTTP セキュリティ応答ヘッダーをカスタマイズします。
description: これは、結果、セキュリティの脆弱性から保護するためのセキュリティ ヘッダーをカスタマイズする方法が descirbes に文書化します。
author: billmath
ms.author: billmath
manager: daveba
ms.reviewer: akgoel23
ms.date: 02/19/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 231c8783032f51f607565922d90ea7f7eb877cfd
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444689"
---
# <a name="customize-http-security-response-headers-with-ad-fs-2019"></a>AD FS 2019 HTTP セキュリティ応答ヘッダーをカスタマイズします。 
 
一般的なセキュリティの脆弱性に対して保護を利用するために、最新のブラウザー ベースの保護メカニズムで機能を利用するには、管理者は、AD FS 2019 がセキュリティの HTTP 応答ヘッダーをカスタマイズするための機能を追加AD FS によって送信されます。 2 つの新しいコマンドレットの概要を介して行われます。`Get-AdfsResponseHeaders`と`Set-AdfsResponseHeaders`します。  
 
よくについて説明しますが、このドキュメントで AD FS 2019 によって送信されるヘッダーをカスタマイズするのに方法を示す応答ヘッダーのセキュリティを使用します。   
 
>[!NOTE]
>ドキュメントでは、AD FS 2019 がインストールされていることを前提としています。  

 
ヘッダーについて説明します、前に管理者がセキュリティ ヘッダーをカスタマイズするための必要性を作成するいくつかのシナリオを見てみましょう 
 
## <a name="scenarios"></a>シナリオ 
1. 管理者が有効になっている[ **HTTP Strict-トランスポート-Security (HSTS)** ](#http-strict-transport-security-hsts) (HTTPS の暗号化を介したすべての接続を強制) パブリック wifi アクセスから HTTP を使用して web アプリにアクセスするユーザーを保護するにはポイント ハックされる可能性があります。 サブドメインの HSTS を有効にするとさらにセキュリティを強化するためにたいです。  
2. 管理者が構成されている、 [ **X フレーム-オプション**](#x-frame-options) (iFrame の任意の web ページのレンダリングを防止する) 応答ヘッダー clickjacked の中から web ページを保護します。 ただし、彼女必要があります (iFrame) のデータを表示する新しいビジネス要件のためのヘッダーの値をカスタマイズするさまざまな配信元 (ドメイン) を持つアプリケーションから。
3. 管理者が有効になっている[ **X の XSS 保護**](#x-xss-protection) (クロス スクリプティング攻撃を防止) 不要部分を削除し、ブラウザーがクロス スクリプティング攻撃が検出された場合、ページをブロックします。 ただし、彼女必要があります、ページ読み込みを許可するヘッダーをカスタマイズする 1 回のサニタイズします。  
4. 管理者が有効にする必要があります[**クロス オリジン リソース共有 (CORS)** ](#cross-origin-resource-sharing-cors-headers)し、別のドメインと web API にアクセスするシングル ページ アプリケーションを許可する AD FS で配信元の (ドメイン) を設定します。  
5. 管理者が有効になっている[**コンテンツ セキュリティ ポリシー (CSP)** ](#content-security-policy-csp)ヘッダー クロス サイト スクリプティングおよび data インジェクションを防ぐには、クロス ドメイン要求を禁止することで攻撃です。 ただし、新しいビジネス要件のためには、web ページは、任意のオリジンからイメージを読み込むし、メディアを信頼できるプロバイダーに制限を許可するヘッダーをカスタマイズする彼女必要があります。  

 
## <a name="http-security-response-headers"></a>セキュリティの HTTP 応答ヘッダー 
AD FS によって、web ブラウザーに送信される出力方向の HTTP 応答には、応答ヘッダーが含まれます。 使用して、ヘッダーを表示することができます、`Get-AdfsResponseHeaders`コマンドレットを次に示すよう。  

![応答のヘッダー](media/customize-http-security-headers-ad-fs/header1.png)

`ResponseHeaders`上のスクリーン ショットで属性がセキュリティ ヘッダーに含まれるすべての HTTP 応答での AD FS によってを識別します。 場合にのみ応答ヘッダーが送信されます`ResponseHeadersEnabled`に設定されている`True`(既定値)。 値を設定できます`False`を AD FS のセキュリティ ヘッダーのいずれかの HTTP 応答などを防ぐためにします。 ただしこれは推奨されません。  実行するには、次を使用します。

```PowerShell
Set-AdfsResponseHeaders -EnableResponseHeaders $false
```
 
### <a name="http-strict-transport-security-hsts"></a>HTTP Strict-トランスポート-Security (HSTS) 
HSTS は、web セキュリティのポリシー メカニズムのプロトコルのダウン グレード攻撃や cookie のハイジャックを HTTP と HTTPS の両方のエンドポイントを持つサービスを軽減するのに役立ちます。 Web サーバーは、web ブラウザー (またはその他の complying ユーザー エージェント) のみの対話で HTTPS を使用して、HTTP プロトコルを使用することはありませんを宣言できます。  
 
Web 認証トラフィックのすべての AD FS のエンドポイントは https のみを使って開かれます。 その結果、AD FS で効果的に HTTP Strict Transport Security ポリシー メカニズムを提供する脅威が軽減 (既定ではありません HTTP へのダウン グレードで HTTP リスナーが存在しないため)。 次のパラメーターを設定して、ヘッダーをカスタマイズすることができます。 
 
- **最大継続期間 =&lt;有効期限が切れる時刻&gt;** – 秒単位で有効期限は、どのくらいの期間、サイトのみアクセスすることは HTTPS を使用してを指定します。 既定の推奨値は 31536000 秒 (1 年) です。  
- **includeSubDomains** – これは省略可能なパラメーター。 指定した場合も、すべてのサブドメインに HSTS ルールが適用されます。  
 
#### <a name="hsts-customization"></a>HSTS のカスタマイズ 
既定では、ヘッダーが有効になっていると`max-age`1 年間に設定。 ただし、管理者を変更できる、 `max-age` (最長有効期間の値を小さくは推奨されません) 経由のサブドメインの HSTS を有効にするか、`Set-AdfsResponseHeaders`コマンドレット。  
 
```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "Strict-Transport-Security" -SetHeaderValue "max-age=<seconds>; includeSubDomains" 
``` 

以下に例を示します。 

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "Strict-Transport-Security" -SetHeaderValue "max-age=31536000; includeSubDomains" 
 ```

既定では、ヘッダーが含まれている、`ResponseHeaders`属性。 ただし、管理者は、ヘッダーからを削除できます、`Set-AdfsResponseHeaders`コマンドレット。  
 
```PowerShell
Set-AdfsResponseHeaders -RemoveHeaders "Strict-Transport-Security" 
```

### <a name="x-frame-options"></a>X フレーム-オプション 
既定で AD FS では、対話型ログインを実行するときに、Iframe を使用する外部のアプリケーションは許可されません。 これは、特定のスタイルのフィッシング攻撃を防ぐために実行されます。 設定されている以前のセッション レベルのセキュリティのために iFrame を使用して非対話型ログインを実行できることに注意してください。  
 
ただし、特定のまれなケースでは、iFrame できる対話型の AD FS ログイン ページを必要とする特定のアプリケーションを信頼することがあります。 'X フレーム オプション' ヘッダーは、この目的のために使用されます。  
 
この HTTP セキュリティ応答ヘッダーが内のページを表示できるかどうかをブラウザーに通信するために使用される、&lt;フレーム&gt;/&lt;iframe&gt;します。 ヘッダーは、次の値のいずれかに設定できます。 
 
- **拒否**– フレーム内のページは表示されません。 これは、既定で、設定をお勧めします。  
- **sameorigin** –、配信元の web ページの配信元と同じ場合、ページをフレームに表示のみができます。 すべての先祖が同じ生成元でもない場合、オプションは非常に便利なできません。  
- **許可から<specified origin>** の場合、ページをフレームに表示のみが、配信元 (例えば、 https://www。"。com) では、ヘッダーに特定の基準と一致します。 

#### <a name="x-frame-options-customization"></a>X フレーム-オプションのカスタマイズ  
既定では、ヘッダーを拒否; に設定されます。ただし、管理者を使用して値を変更できます、`Set-AdfsResponseHeaders`コマンドレット。  
```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "X-Frame-Options" -SetHeaderValue "<deny/sameorigin/allow-from<specified origin>>" 
 ```

以下に例を示します。 

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "X-Frame-Options" -SetHeaderValue "allow-from https://www.example.com" 
 ```

既定では、ヘッダーが含まれている、`ResponseHeaders`属性。 ただし、管理者は、ヘッダーからを削除できます、`Set-AdfsResponseHeaders`コマンドレット。  

```PowerShell
Set-AdfsResponseHeaders -RemoveHeaders "X-Frame-Options" 
```

### <a name="x-xss-protection"></a>X の XSS 保護 
この HTTP セキュリティ応答ヘッダーを使用して、web ページをブラウザーでクロスサイト スクリプティング (XSS) 攻撃が検出されたときの読み込みを停止します。 これは、XSS フィルター処理と呼ばれます。 ヘッダーは、次の値のいずれかに設定できます。 
 
- **0** – 無効にします XSS フィルター処理します。 推奨されません。  
- **1** – により、XSS フィルター処理します。 XSS 攻撃が検出された場合、ブラウザーはページをサニタイズします。   
- **1 になります。モード ブロックを =** – により、XSS フィルター処理します。 XSS 攻撃が検出された場合、ブラウザーは、ページのレンダリングを防ぐ。 これは、既定で、設定をお勧めします。  

#### <a name="x-xss-protection-customization"></a>X の XSS 保護のカスタマイズ 
既定では、ヘッダーは 1 に設定します。モードはブロックを =ただし、管理者を使用して値を変更できます、`Set-AdfsResponseHeaders`コマンドレット。  

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "X-XSS-Protection" -SetHeaderValue "<0/1/1; mode=block/1; report=<reporting-uri>>" 
``` 

以下に例を示します。 

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "X-XSS-Protection" -SetHeaderValue "1" 
 ```

既定では、ヘッダーが含まれている、`ResponseHeaders`属性。 ただし、管理者は、ヘッダーからを削除できます、`Set-AdfsResponseHeaders`コマンドレット。 

```PowerShell
Set-AdfsResponseHeaders -RemoveHeaders "X-XSS-Protection" 
```

### <a name="cross-origin-resource-sharing-cors-headers"></a>クロス オリジン リソース共有 (CORS) ヘッダー 
Web ブラウザーのセキュリティは、web ページがスクリプトから開始されるクロスオリジン要求を行うことを防ぎます。 ただし、場合がありますたいその他のオリジン (ドメイン) のリソースにアクセスします。 CORS は、サーバーによる同一オリジン ポリシーの緩和にできる W3C 標準です。 CORS を使用することによって、不明なリクエストは拒否しながら、一部のクロス オリジン要求のみを明示的に許可できるようになります。  
 
CORS 要求をより深く理解するには、みましょうチュートリアル シナリオは、単一ページ アプリケーション (SPA) の場所をする必要が別のドメインを使用して web API を呼び出します。 さらに、について考えてみましょう SPA と API の両方が ADFS 2019 で構成されていることと、AD FS が有効になっている CORS つまり AD FS は、HTTP 要求の CORS ヘッダーを識別、ヘッダーの値を検証、および、応答に適切な CORS ヘッダーを含める (有効にする方法の詳細とad FS 2019 以下の CORS のカスタマイズ」セクションで CORS を構成します)。 サンプルのフロー: 

1. ユーザーは、クライアント ブラウザーから SPA にアクセスし、認証用の AD FS の認証エンドポイントにリダイレクトされます。 SPA は、暗黙的な許可フロー用に構成は、以降は、認証成功後にブラウザーに、アクセスと ID を返します。 トークンを要求します。  
2. ユーザーの認証後は、フロント エンド JavaScript SPA に含まれるは、web API にアクセスする要求を行います。 要求は次のヘッダーと共に AD FS にリダイレクトされます。
    - オプション – 対象リソースの通信オプションについて説明します 
    - -配信元には、web API の原点が含まれています。
    - アクセス制御の要求メソッド: HTTP メソッドを識別します (例:、削除) 実際の要求が行われたときに使用するには 
    - アクセス制御の要求ヘッダーの実際の要求が行われたときに使用される HTTP ヘッダーを識別します。 
    
   >[!NOTE]
   >CORS 要求が標準の HTTP 要求に似ています、ただし、配信元のヘッダーの存在を通知受信した要求が CORS に関連します。 
3. AD FS では、web API の配信元がヘッダーに含まれるが AD FS (以下の CORS のカスタマイズ」セクションで、信頼されたオリジンを変更する方法の詳細) で構成されている信頼されたオリジンで表示されていることを確認します。 AD FS は、次のヘッダーと共に応答します。  
    - アクセス制御の許可-オリジン – Origin ヘッダーと同じ値 
    - アクセス コントロール-許可する-メソッド-アクセス制御の要求メソッド ヘッダーと同じ値 
    - アクセス制御の要求ヘッダーのヘッダーのように同じアクセス コントロール-許可する-ヘッダー - の値します。 
4. ブラウザーは、次のヘッダーを含む実際の要求を送信します。 
    - HTTP メソッド (例:、削除) 
    - -配信元には、web API の原点が含まれています。 
    - アクセスの制御-許可する-ヘッダー応答ヘッダーに含まれるすべてのヘッダー 
5. 確認されたら、AD FS は、アクセス制御の許可-オリジンの応答ヘッダーで web API のドメイン (オリジン) を含めることによって要求を承認します。  
6. アクセス制御の許可-オリジン ヘッダーを含めることにより、要求された API の呼び出しで進めてブラウザー。

#### <a name="cors-customization"></a>CORS のカスタマイズ 
既定では、CORS 機能は使用できません。ただし、管理者は、セット AdfsResponseHeaders コマンドレットを使って機能を有効にできます。  

```PowerShell 
Set-AdfsResponseHeaders -EnableCORS $true 
 ```

1 つ有効にすると、管理者は、同じコマンドレットを使用して信頼されたオリジンの一覧を列挙できます。 次のコマンドは、オリジンからの CORS 要求を許可する、 **https&#58;//example1.com**と**https&#58;//example1.com**します。 
 
```PowerShell
Set-AdfsResponseHeaders -CORSTrustedOrigins https://example1.com,https://example2.com 
 ```

> [!NOTE]
> 管理者は、任意のオリジンからの CORS 要求を許可するなど、"*"の信頼されたオリジンは、一覧でこのアプローチはセキュリティの脆弱性と、警告メッセージのため推奨されませんが提供されているを選択したかどうか。 

### <a name="content-security-policy-csp"></a>コンテンツ セキュリティ ポリシー (CSP) 
この HTTP セキュリティ応答ヘッダーは、ブラウザーが誤って悪意のあるコンテンツを実行するを防ぐことで、クロスサイト スクリプティング、クリックジャッ キング、およびその他のデータのインジェクション攻撃を防ぐために使用されます。 CSP をサポートしないブラウザーでは、単に CSP の応答ヘッダーを無視します。  
 
#### <a name="csp-customization"></a>CSP のカスタマイズ 
CSP のヘッダーのカスタマイズでは、リソース ブラウザーを定義するセキュリティ ポリシーを web ページを読み込むことができる変更する必要があります。 既定のセキュリティ ポリシーは、します。  
 
`Content-Security-Policy: default-src ‘self’ ‘unsafe-inline’ ‘’unsafe-eval’; img-src ‘self’ data:;` 
 
**既定 src**ディレクティブを使用して変更する[- src ディレクティブ](https://developer.mozilla.org/docs/Web/HTTP/Headers/Content-Security-Policy/default-src)各ディレクティブを明示的にリストすることがなく。 ポリシーの次の例で 1 は、ポリシー 2 と同じです。  

ポリシー 1 
```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "Content-Security-Policy" -SetHeaderValue "default-src 'self'" 
```
 
ポリシー 2
```PowerShell 
Set-AdfsResponseHeaders -SetHeaderName "Content-Security-Policy" -SetHeaderValue "script-src ‘self’; img-src ‘self’; font-src 'self';  
frame-src 'self'; manifest-src 'self'; media-src 'self';" 
```

ディレクティブが明示的に表示されている場合、指定された値は、既定 src に指定された値をオーバーライドします。として値の取得が次の例で img src ' *' (任意のオリジンから読み込まれるイメージを許可する) 他の src ディレクティブが値を取得中に 'self' (web ページと同じ生成元への制限)。  

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "Content-Security-Policy" -SetHeaderValue "default-src ‘self’; img-src *" 
```
既定 src ポリシーに対して次のソースを定義できます。 
 
- web ページの配信元に読み込むには、コンテンツの配信元を制限 'self' – これを指定します。 
- ' unsafe インライン ': ポリシーでこれを指定することにより、インライン JavaScript の使用と CSS 
- ' unsafe-eval' – ポリシーでこれを指定するを使用できるようにテキストなどのメカニズムを JavaScript の eval 
- 読み込む任意のオリジンからのコンテンツを制限 'none' – これを指定します。 
- データ:-データを指定します。Uri には、インラインの小さなファイルをドキュメントに埋め込むには、コンテンツの作成者が使用できます。 使用量がお勧めしません。  
 
>[!NOTE]
>AD FS 認証プロセスでは JavaScript を使用し、したがって 'で unsafe インライン' を含めることで JavaScript を有効にし、' 安全でない eval' ソースの既定のポリシー。  

### <a name="custom-headers"></a>カスタム ヘッダー 
上記のほか、セキュリティ応答ヘッダーを表示 (HSTS、CSP、X フレームのオプション、X の XSS 保護、および CORS)、AD FS 2019 新しいヘッダーを設定する機能を提供します。  
 
以下に例を示します。値を新しいヘッダー"TestHeader"を"TestHeaderValue"として設定するには 

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "TestHeader" -SetHeaderValue "TestHeaderValue" 
 ```

設定すると、この新しいヘッダーは、AD FS 応答 (次のスニペット fiddler) で送信されます。  
 
![Fiddler](media/customize-http-security-headers-ad-fs/header2.png)

## <a name="web-browswer-compatibility"></a>Web ブラウザの互換性
どの web ブラウザーが各セキュリティ応答ヘッダーとの互換性を判断するのにには、次の表とリンクを使用します。

|セキュリティの HTTP 応答ヘッダー|ブラウザーの互換性|
|-----|-----|
|HTTP Strict-トランスポート-Security (HSTS)|[HSTS ブラウザーの互換性](https://developer.mozilla.org/docs/Web/HTTP/Headers/Strict-Transport-Security#Browser_compatibility)|
|X フレーム-オプション|[X フレーム-オプションのブラウザーの互換性](https://developer.mozilla.org/docs/Web/HTTP/Headers/X-Frame-Options#Browser_compatibility)| 
|X の XSS 保護|[X の XSS 保護ブラウザーの互換性](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-XSS-Protection#Browser_compatibility)| 
|クロス オリジン リソース共有 (CORS)|[CORS のブラウザーの互換性](https://developer.mozilla.org/docs/Web/HTTP/CORS#Browser_compatibility) 
|コンテンツ セキュリティ ポリシー (CSP)|[CSP のブラウザーの互換性](https://developer.mozilla.org/docs/Web/HTTP/CSP#Browser_compatibility) 

## <a name="next"></a>Next

- [AD FS ヘルプ troublehshooting ガイドを使用してください。](https://aka.ms/adfshelp/troubleshooting )
- [AD FS のトラブルシューティング](../../ad-fs/troubleshooting/ad-fs-tshoot-overview.md)
