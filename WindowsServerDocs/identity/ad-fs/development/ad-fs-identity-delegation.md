---
title: AD FS と id 委任のシナリオ
description: このシナリオでは、バックエンド リソースの id 委任チェーンをアクセス制御チェックを実行する要求にアクセスする必要があるアプリケーションについて説明します。
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: b82d5fd749ac874d09bc54123727aaf902c4d778
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819853"
---
# <a name="identity-delegation-scenario-with-ad-fs"></a>AD FS と id 委任のシナリオ


[.NET Framework 4.5 以降、Windows Identity Foundation (WIF) がされたに完全に統合、.NET Framework です。 WIF では、このトピックでは、WIF 3.5 では、アドレス指定のバージョンは非推奨し、.NET Framework 3.5 SP1 または .NET Framework 4 に対して開発する場合にのみ使用する必要があります。 .NET Framework 4.5、WIF 4.5 では別名で WIF の詳細についてはドキュメントを参照して、Windows Identity Foundation では、.NET Framework 4.5 開発ガイドします。] 

このシナリオでは、バックエンド リソースの id 委任チェーンをアクセス制御チェックを実行する要求にアクセスする必要があるアプリケーションについて説明します。 Id 委任チェーンは、通常は、最初の呼び出し元と直前の呼び出し元の id 情報で構成されます。

Windows プラットフォームを今すぐで Kerberos 委任モデルでは、バックエンド リソースの最初の呼び出し元が直前の呼び出し元の id にのみアクセス権を持ちます。 このモデルは、信頼されたサブシステム モデルとも呼ばれます。 WIF では、最初の呼び出し元だけでなく、アクターのプロパティを使用して委任チェーンの直前の呼び出し元の id を保持します。

次の図は、fabrikam 社の従業員が Contoso.com のアプリケーションで公開されるリソースにアクセスする一般的な id 委任シナリオを示します。

![同一。](media/ad-fs-identity-delegation/id1.png)

このシナリオに参加している架空ユーザーは次のとおりです。

- Frank:Fabrikam 社の従業員が Contoso のリソースにアクセスします。
- Daniel:アプリケーションで必要な変更を実装する Contoso アプリケーション開発者。
- Adam:Contoso の IT 管理者です。

このシナリオに関連するコンポーネントは次のとおりです。

- web1:最初の呼び出し元の委任された id を必要とするバックエンド リソースへのリンクの Web アプリケーション。 このアプリケーションは、ASP.NET で構築されます。
- さらに、即時呼び出し元の最初の呼び出し元の委任された id を必要とする SQL Server にアクセスする Web サービス。 このサービスは、WCF で構築されます。
- sts1:要求のプロバイダーの役割では、(web1) アプリケーションで予想される要求を出力する STS。 Fabrikam.com とも、アプリケーションの信頼を確立しました。
- sts2:STS は Fabrikam.com の id プロバイダーの役割であり fabrikam 社の従業員は認証を使用して終了ポイントを提供します。 Contoso.com と信頼関係を確立した fabrikam 社の従業員が Contoso.com のリソースにアクセスできるようにします。

>[!NOTE] 
>「ActAs トークン」、このシナリオでよく使用するとは、STS によって発行され、ユーザーの id を格納するトークンを指します。 アクターのプロパティには、STS の id が含まれています。

前の図に示すように、このシナリオでは、フローには。


1. Fabrikam の従業員の id とアクター プロパティで、即時呼び出し元の id の両方を含む ActAs トークンを取得する contoso 社のアプリケーションが構成されます。 Daniel は、アプリケーションにこれらの変更を実装しました。
2. ActAs トークンをバックエンド サービスに渡す、contoso 社のアプリケーションが構成されます。 Daniel は、アプリケーションにこれらの変更を実装しました。
3. Contoso Web サービスを構成するには sts1 を呼び出すことで、ActAs トークンを検証します。 Adam は sts1 委任要求の処理を有効になります。
4. Fabrikam ユーザー Frank は、contoso 社のアプリケーションにアクセスし、バックエンド リソースへのアクセスが与えられます。

## <a name="set-up-the-identity-provider-ip"></a>Id プロバイダー (IP) を設定します。

3 つのオプションは、Fabrikam.com の管理者、Frank 使用できます。


1. 購入し、Active Directory® フェデレーション サービス (AD FS) など、STS の製品をインストールします。
2. LiveID STS などのクラウド STS 製品をサブスクライブします。
3. WIF を使用してカスタム STS を構築します。

このサンプルでは、Frank はオプション 1 を選択し、IP STS として AD FS をインストールすると仮定します。 また、終了点は、ユーザーを認証する、\windowsauth という名前を構成します。 AD FS 製品のマニュアルを参照して、Adam の場合、Contoso の IT 管理者との対話では、Frank は、Contoso.com ドメインと信頼関係を確立します。

## <a name="set-up-the-claims-provider"></a>クレーム プロバイダーを設定します。

オプションは、Contoso.com の管理者の使用可能な Adam の場合は、同じ id プロバイダーの前に説明したようにします。 このサンプルでは、Adam はオプション 1 を選択し、RP STS として AD FS 2.0 をインストールすると仮定します。

## <a name="set-up-trust-with-the-ip-and-application"></a>IP およびアプリケーションとの信頼関係を設定します。

AD FS のマニュアルを見ながら、Adam は、Fabrikam.com とアプリケーション間の信頼を確立します。

## <a name="set-up-delegation"></a>委任を設定します。

AD FS は、委任処理を提供します。 AD FS のマニュアルを参照して、ActAs トークンの処理が可能 Adam です。

## <a name="application-specific-changes"></a>アプリケーション固有の変更

既存のアプリケーションに id 委任のサポートを追加するのには、次の変更を加えてする必要があります。 Daniel では、WIF を使用して、これらの変更を加えます。


- Sts1 から受信したその web1 ブートス トラップ トークンをキャッシュします。
- 発行済みトークンを使用して CreateChannelActingAs を使用すると、バック エンドの Web サービスへのチャネルを作成できます。
- バックエンド サービスのメソッドを呼び出します。

## <a name="cache-the-bootstrap-token"></a>ブートス トラップ トークンをキャッシュします。

ブートス トラップ トークンが最初に、STS によって発行されたトークンと、アプリケーションがそこからクレームを抽出します。 このサンプル シナリオで、Frank のユーザーの sts1 によってこのトークンが発行され、アプリケーションではキャッシュします。 次のコード サンプルでは、ASP.NET アプリケーションでトークンをブートス トラップを取得する方法を示します。

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
WIF には、メソッド、 [CreateChannelActingAs](https://msdn.microsoft.com/library/ee733863.aspx)、ActAs 要素として指定したセキュリティ トークンを使用して、トークン発行要求を補足する指定した種類のチャネルを作成します。 ブートス トラップ トークンをこのメソッドに渡すし、返されたチャネルで必要なサービス メソッドを呼び出すことができます。 Frank の id を持ってこのサンプル シナリオで、[アクター](https://msdn.microsoft.com/library/microsoft.identitymodel.claims.iclaimsidentity.actor.aspx)プロパティ web1 の id に設定します。

次のコード スニペットを使用して Web サービスを呼び出す方法を示しています。 [CreateChannelActingAs](https://msdn.microsoft.com/library/ee733863.aspx)を返されたチャネルで呼び出して、サービスのメソッド、ComputeResponse、のいずれか。

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

Web サービスを WCF で構築されたバインディングが適切な発行者アドレスを持つ IssuedSecurityTokenParameters で構成されると、wif を有効になっているので、ActAs の検証は WIF によって自動的に処理されます。 

Web サービスは、アプリケーションで必要な特定のメソッドを公開します。 サービスに必要な特定のコード変更はありません。 次のコード サンプルでは、IssuedSecurityTokenParameters 使用して Web サービスの構成を示します。

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
