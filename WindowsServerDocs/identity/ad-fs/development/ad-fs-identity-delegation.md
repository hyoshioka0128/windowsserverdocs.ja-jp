---
title: AD FS を使用した id 委任のシナリオ
description: このシナリオでは、アクセス制御チェックを実行するために id 委任チェーンが必要なバックエンドリソースにアクセスする必要があるアプリケーションについて説明します。
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 292bec5f73e2746103ffc41cde729ddc59728e0b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407870"
---
# <a name="identity-delegation-scenario-with-ad-fs"></a>AD FS を使用した id 委任のシナリオ


[.NET Framework 4.5 以降では、Windows Identity Foundation (WIF) は .NET Framework に完全に統合されています。 このトピックでアドレス指定された WIF のバージョンである WIF 3.5 は非推奨とされており、.NET Framework 3.5 SP1 または .NET Framework 4 に対して開発する場合にのみ使用してください。 .NET Framework 4.5 の WIF (WIF 4.5 とも呼ばれます) の詳細については、『 .NET Framework 4.5 Development Guide 』の Windows Identity Foundation のドキュメントを参照してください。 

このシナリオでは、アクセス制御チェックを実行するために id 委任チェーンが必要なバックエンドリソースにアクセスする必要があるアプリケーションについて説明します。 単純な id 委任チェーンは、通常、最初の呼び出し元の情報と、直前の呼び出し元の id で構成されます。

現在、Windows プラットフォーム上の Kerberos 委任モデルでは、バックエンドリソースは、最初の呼び出し元の id に対してのみアクセスできます。 このモデルは、一般に信頼されたサブシステムモデルと呼ばれます。 WIF は、アクタープロパティを使用して、最初の呼び出し元とデリゲートチェーンの直前の呼び出し元の id を保持します。

次の図は、Fabrikam の従業員が Contoso.com アプリケーションで公開されているリソースにアクセスする一般的な id 委任シナリオを示しています。

![同一。](media/ad-fs-identity-delegation/id1.png)

このシナリオに参加する架空のユーザーは次のとおりです。

- 佐藤Contoso のリソースにアクセスする Fabrikam の従業員。
- Danielアプリケーションで必要な変更を実装する Contoso アプリケーション開発者。
- AdamContoso IT 管理者。

このシナリオに関連するコンポーネントは次のとおりです。

- web1最初の呼び出し元の委任された id を必要とするバックエンドリソースへのリンクを持つ Web アプリケーション。 このアプリケーションは ASP.NET を使用して構築されています。
- SQL Server にアクセスする Web サービス。最初の呼び出し元の委任された id と、直前の呼び出し元の id が必要です。 このサービスは、WCF を使用して構築されています。
- sts1:要求プロバイダーの役割を持つ STS。アプリケーション (web1) によって予期される要求を出力します。 また、Fabrikam.com とアプリケーションの信頼関係が確立されています。
- sts2:Fabrikam.com の id プロバイダーの役割を果たす STS。 Fabrikam の従業員が認証に使用するエンドポイントを提供します。 Fabrikam の従業員が Contoso.com のリソースにアクセスできるように、Contoso.com との信頼関係が確立されました。

>[!NOTE] 
>このシナリオでよく使用される "ActAs token" という用語は、STS によって発行され、ユーザーの id が含まれているトークンを指します。 アクタープロパティには、STS の id が含まれています。

上の図に示すように、このシナリオのフローは次のようになります。


1. Contoso アプリケーションは、Fabrikam の従業員の id と、アクタープロパティの直前の呼び出し元の id の両方を含む ActAs トークンを取得するように構成されています。 Daniel は、これらの変更をアプリケーションに実装しました。
2. Contoso アプリケーションは、ActAs トークンをバックエンドサービスに渡すように構成されています。 Daniel は、これらの変更をアプリケーションに実装しました。
3. Contoso Web サービスは、sts1 を呼び出して ActAs トークンを検証するように構成されています。 Adam は、委任要求を処理するために sts1 を有効にしました。
4. Fabrikam user Frank は Contoso アプリケーションにアクセスし、バックエンドリソースへのアクセス権を付与します。

## <a name="set-up-the-identity-provider-ip"></a>Id プロバイダー (IP) の設定

Fabrikam.com 管理者は、次の3つのオプションを使用できます。 Frank:


1. Active Directory®フェデレーションサービス (AD FS) などの STS 製品を購入してインストールします。
2. LiveID STS などのクラウド STS 製品をサブスクライブします。
3. WIF を使用してカスタム STS を構築します。

このサンプルシナリオでは、Frank がオプション1を選択し、IP-HTTPS として AD FS をインストールするとします。 また、ユーザーを認証するために、「\ windowsauth」という名前のエンドポイントを構成します。 AD FS の製品ドキュメントを参照し、Adam と通信することにより、Contoso.com ドメインとの信頼関係を確立します。

## <a name="set-up-the-claims-provider"></a>要求プロバイダーを設定する

Contoso.com 管理者である Adam のオプションは、前に id プロバイダーについて説明したものと同じです。 このサンプルシナリオでは、Adam がオプション1を選択し、RP STS として AD FS 2.0 をインストールするとします。

## <a name="set-up-trust-with-the-ip-and-application"></a>IP およびアプリケーションとの信頼関係を設定する

AD FS のドキュメントを参照することにより、Adam は Fabrikam.com とアプリケーションの間に信頼を確立します。

## <a name="set-up-delegation"></a>委任の設定

AD FS は、委任処理を提供します。 AD FS のドキュメントを参照することにより、Adam は ActAs トークンを処理できるようになります。

## <a name="application-specific-changes"></a>アプリケーション固有の変更

既存のアプリケーションに id 委任のサポートを追加するには、次の変更を行う必要があります。 Daniel は、WIF を使用してこれらの変更を行います。


- Web1 が sts1 から受け取ったブートストラップトークンをキャッシュします。
- CreateChannelActingAs を発行済みトークンと共に使用して、バックエンド Web サービスへのチャネルを作成します。
- バックエンドサービスのメソッドを呼び出します。

## <a name="cache-the-bootstrap-token"></a>ブートストラップトークンをキャッシュする

ブートストラップトークンは STS によって発行された最初のトークンであり、アプリケーションはそこから要求を抽出します。 このサンプルシナリオでは、このトークンはユーザー Frank の sts1 によって発行され、アプリケーションによってキャッシュされます。 次のコードサンプルは、ASP.NET アプリケーションでブートストラップトークンを取得する方法を示しています。

```
// Get the Bootstrap Token
SecurityToken bootstrapToken = null;

IClaimsPrincipal claimsPrincipal = Thread.CurrentPrincipal as IClaimsPrincipal;
if ( claimsPrincipal != null )
{
    IClaimsIdentity claimsIdentity = (IClaimsIdentity)claimsPrincipal.Identity;
    bootstrapToken = claimsIdentity.BootstrapToken;
}
```
WIF には、 [CreateChannelActingAs](https://msdn.microsoft.com/library/ee733863.aspx)というメソッドが用意されています。このメソッドは、指定されたセキュリティトークンを持つトークン発行要求を ActAs 要素として補強する、指定された種類のチャネルを作成します。 ブートストラップトークンをこのメソッドに渡し、返されたチャネルで必要なサービスメソッドを呼び出すことができます。 このサンプルシナリオでは、Frank の id で[Actor](https://msdn.microsoft.com/library/microsoft.identitymodel.claims.iclaimsidentity.actor.aspx)プロパティが web1's identity に設定されています。

次のコードスニペットは、 [CreateChannelActingAs](https://msdn.microsoft.com/library/ee733863.aspx)を使用して Web サービスを呼び出し、返されたチャネルでサービスのメソッド ComputeResponse の1つを呼び出す方法を示しています。

```
// Get the channel factory to the backend service from the application state
ChannelFactory<IService2Channel> factory = (ChannelFactory<IService2Channel>)Application[Global.CachedChannelFactory];

// Create and setup channel to talk to the backend service
IService2Channel channel;
lock (factory)
{
// Setup the ActAs to point to the caller's token so that we perform a 
// delegated call to the backend service
// on behalf of the original caller.
    channel = factory.CreateChannelActingAs<IService2Channel>(callerToken);
}

string retval = null;

// Call the backend service and handle the possible exceptions
try
{
    retval = channel.ComputeResponse(value);
    channel.Close();
} catch (Exception exception)
{
    StringBuilder sb = new StringBuilder();
    sb.AppendLine("An unexpected exception occurred.");
    sb.AppendLine(exception.StackTrace);
    channel.Abort();
    retval = sb.ToString();
}

```
## <a name="web-service-specific-changes"></a>Web サービス固有の変更

Web サービスは WCF を使用して構築され、WIF が有効になっているため、適切な発行者アドレスを持つ IssuedSecurityTokenParameters でバインドが構成されると、ActAs の検証が WIF によって自動的に処理されます。 

Web サービスは、アプリケーションが必要とする特定のメソッドを公開します。 サービスには特定のコード変更は必要ありません。 次のコードサンプルは、IssuedSecurityTokenParameters を使用した Web サービスの構成を示しています。

```
// Configure the issued token parameters with the correct settings
IssuedSecurityTokenParameters itp = new IssuedSecurityTokenParameters( "http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1" );
itp.IssuerMetadataAddress = new EndpointAddress( "http://localhost:6000/STS/mex" );
itp.IssuerAddress = new EndpointAddress( "http://localhost:6000/STS" );

// Create the security binding element
SecurityBindingElement sbe = SecurityBindingElement.CreateIssuedTokenForCertificateBindingElement( itp );
sbe.MessageSecurityVersion = MessageSecurityVersion.WSSecurity11WSTrust13WSSecureConversation13WSSecurityPolicy12BasicSecurityProfile10;

// Create the HTTP transport binding element
HttpTransportBindingElement httpBE = new HttpTransportBindingElement();

// Create the custom binding using the prepared binding elements
CustomBinding binding = new CustomBinding( sbe, httpBE );

using ( ServiceHost host = new ServiceHost( typeof( Service2 ), new Uri( "http://localhost:6002/Service2" ) ) )
{
    host.AddServiceEndpoint( typeof( IService2 ), binding, "" );
    host.Credentials.ServiceCertificate.SetCertificate( "CN=localhost", StoreLocation.LocalMachine, StoreName.My );

// Enable metadata generation via HTTP GET
    ServiceMetadataBehavior smb = new ServiceMetadataBehavior();
    smb.HttpGetEnabled = true;
    host.Description.Behaviors.Add( smb );
    host.AddServiceEndpoint( typeof( IMetadataExchange ), MetadataExchangeBindings.CreateMexHttpBinding(), "mex" );

// Configure the service host to use WIF
    ServiceConfiguration configuration = new ServiceConfiguration();
    configuration.IssuerNameRegistry = new TrustedIssuerNameRegistry();

    FederatedServiceCredentials.ConfigureServiceHost( host, configuration );

    host.Open();

    Console.WriteLine( "Service2 started, press ENTER to stop ..." );
    Console.ReadLine();

    host.Close();
}
```

## <a name="next-steps"></a>次の手順
[AD FS の開発](../../ad-fs/AD-FS-Development.md)  
