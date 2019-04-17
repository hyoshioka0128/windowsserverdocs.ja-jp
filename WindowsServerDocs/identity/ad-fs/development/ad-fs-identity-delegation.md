---
title: "AD FS による ID 委任のシナリオ"
description: "このシナリオでは、アクセス制御チェックを実行する識別情報の委任チェーンを必要とする、バックエンドのリソースにアクセスする必要があるアプリケーションについて説明します。"
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: b82d5fd749ac874d09bc54123727aaf902c4d778
ms.sourcegitcommit: c16a2bf1b8a48ff267e71ff29f18b5e5cda003e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/28/2018
---
# <a name="identity-delegation-scenario-with-ad-fs"></a>AD FS による ID 委任のシナリオ


[.NET Framework 4.5 以降では、Windows Identity Foundation (WIF) が完全に統合されました、.NET Framework します。 WIF 3.5 では、このトピックで取り上げて WIF のバージョンは推奨されなくなりましたおよび .NET Framework 3.5 SP1 または .NET Framework 4 に対してを開発するときにのみ使用する必要があります。 詳細については、.NET Framework 4.5、WIF 4.5 とも呼ばれるで WIF ドキュメントを参照して、Windows Identity Foundation で .NET Framework 4.5 開発ガイド。] 

このシナリオでは、アクセス制御チェックを実行する識別情報の委任チェーンを必要とする、バックエンドのリソースにアクセスする必要があるアプリケーションについて説明します。 単純な識別情報の委任チェーンは通常、最初の呼び出し側および直接の呼び出し元の ID の情報で構成されます。

本日、Windows プラットフォームで Kerberos の委任モデルでは、バック エンド リソースは、直接の呼び出し元の ID にのみを除く、最初の呼び出し元のアクセス権を持ちます。 このモデルは、信頼されたサブシステムのモデルとも呼ばれます。 WIF では、最初の呼び出し元だけでなく、アクターのプロパティを使用して委任チェーン内の直接の呼び出し元の ID を保持します。

次の図は、fabrikam 社の従業員 Contoso.com アプリケーションで公開されたリソースにアクセスする、一般的な ID 委任のシナリオを示しています。

![識別情報](media/ad-fs-identity-delegation/id1.png)

このシナリオに参加している架空のユーザーは次のとおりです。

- Frank: Contoso リソースにアクセスする必要のある fabrikam 社の従業員です。
- Daniel: Contoso アプリケーション開発者の方に、アプリケーションで必要な変更を実装します。
- Adam: Contoso の IT 管理者。

このシナリオに関連するコンポーネントは次のとおりです。

- web1: Web アプリケーションへのリンクを最初の呼び出し元の委任された ID を必要とするバックエンド リソースをします。 このアプリケーションは ASP.NET で構築されています。
- と共にを直接の呼び出し元の最初の呼び出し側の委任された ID を必要とする、SQL サーバーにアクセスする Web サービスです。 このサービスは、WCF に従って作成されます。
- sts1: An STS され、要求プロバイダーでは、役割を担うされる必要があるアプリケーション (web1) によって信頼性情報を出力します。 Fabrikam.com とも、アプリケーションの信頼を確立します。
- sts2: An STS Fabrikam.com の ID プロバイダーの役割が、fabrikam 社の従業員を認証に使用するエンドポイントを提供します。 Fabrikam 社の従業員が Contoso.com 上のリソースにアクセスできるように Contoso.com と信頼関係を確立します。

>[!NOTE] 
>「ActAs トークン」、このシナリオで通常使用するいるとは、STS によって発行され、ユーザーの ID を含むトークンを指します。 アクターのプロパティには、STS の ID が含まれています。

このシナリオではフローは次の図は、以前のようにです。


1. Contoso アプリケーションは Fabrikam の従業員の ID とアクター プロパティで、即時呼び出し元の ID の両方を含む ActAs トークンを取得するように構成します。 Daniel は、アプリケーションにこれらの変更を実装しました。
2. Contoso アプリケーションは、バックエンド サービスに ActAs トークンを渡すように構成します。 Daniel は、アプリケーションにこれらの変更を実装しました。
3. Contoso Web サービスは、sts1 を呼び出すことによって、ActAs トークンを検証するように構成します。 Adam は委任要求を処理する sts1 を有効になります。
4. Fabrikam ユーザー Frank は Contoso アプリケーションにアクセスして、バック エンド リソースへのアクセスが与えられます。

## <a name="set-up-the-identity-provider-ip"></a>Id プロバイダー (IP) の設定します。

3 つのオプションは、Fabrikam.com 管理者、Frank できます。


1. 購入し、Active Directory® フェデレーション サービス (AD FS) などの STS 製品をインストールします。
2. LiveID STS などのクラウド STS 製品にサブスクライブします。
3. WIF を使用してカスタムの STS を構築します。

このサンプル シナリオについて Frank がオプション 1 を選択し、IP STS として AD FS をインストールするものとします。 また、という名前のユーザーを認証する、\windowsauth 終了点を構成します。 AD FS の製品マニュアルを参照して、Adam は、Contoso の IT 管理者に会話して Frank Contoso.com ドメインと信頼関係を確立します。

## <a name="set-up-the-claims-provider"></a>要求プロバイダーを設定します。

オプション Contoso.com 管理者の利用可能な Adam と同じ ID プロバイダーの前に説明しました。 このサンプルのシナリオでは、Adam はオプション 1 を選択し、RP STS として AD FS 2.0 をインストールすると仮定します。

## <a name="set-up-trust-with-the-ip-and-application"></a>IP およびアプリケーションとの信頼関係をセットアップします。

AD FS のドキュメントを参照して、Adam は Fabrikam.com とアプリケーション間の信頼を確立します。

## <a name="set-up-delegation"></a>委任を設定します。

AD FS では、委任の処理を提供します。 AD FS のドキュメントを参照しているで Adam ActAs トークンの処理が有効にします。

## <a name="application-specific-changes"></a>アプリケーションに固有の変更

Id 委任のサポートを既存のアプリケーションに追加するのには、以下の変更を加え必要があります。 Daniel では、WIF を使用して、これらの変更を加えます。


- その web1 sts1 から受信したブートス トラップ トークンをキャッシュします。
- 発行されたトークンを使って CreateChannelActingAs を使用すると、バック エンドの Web サービスへのチャンネルを作成できます。
- バックエンド サービスのメソッドを呼び出します。

## <a name="cache-the-bootstrap-token"></a>ブートス トラップ トークンをキャッシュします。

ブートス トラップ トークンは、STS によって発行された最初のトークンし、アプリケーションは、そこから信頼性情報を抽出します。 このサンプル シナリオで Frank、ユーザーの sts1 によってこのトークンが発行されたし、アプリケーションでは、それをキャッシュします。 次のコード サンプルは、ASP.NET アプリケーションでトークンのブートス トラップを取得する方法を示しています。

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
WIF 提供メソッド、[CreateChannelActingAs](https://msdn.microsoft.com/library/ee733863.aspx)、ActAs 要素として指定されたセキュリティ トークンを使用してトークン発行要求を補足する、指定した種類のチャネルを作成します。 ブートス トラップ トークンをこのメソッドに渡すし、返されたチャネルで必要なサービス メソッドを呼び出すことができます。 このサンプル シナリオで Frank の識別情報は、[アクター](https://msdn.microsoft.com/library/microsoft.identitymodel.claims.iclaimsidentity.actor.aspx)プロパティが web1 の ID に設定します。

次のコード スニペットを使用して Web サービスを呼び出す方法を示しています。[CreateChannelActingAs](https://msdn.microsoft.com/library/ee733863.aspx)し、返されたチャネルでサービスの方法、ComputeResponse、のいずれかを呼び出します。

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
## <a name="web-service-specific-changes"></a>Web サービスに固有の変更

Web サービスを WCF を使って構築されたバインディングは、適切な発行元のアドレスを持つ IssuedSecurityTokenParameters で構成した後、WIF を有効になっているので、ActAs の検証が WIF によって自動的に処理されます。 

Web サービスは、アプリケーションで必要な特定のメソッドを公開します。 サービスに必要な特定のコード変更はありません。 次のコード サンプルは、IssuedSecurityTokenParameters と Web サービスの構成を示しています。

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
