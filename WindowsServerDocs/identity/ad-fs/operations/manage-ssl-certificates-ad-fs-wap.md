---
ms.assetid: a3f50046-5d48-43d3-b0f8-ac2346b15285
title: Windows Server 2016 の AD FS と WAP で SSL 証明書を管理する
description: Windows Server 2016 の AD FS と WAP で SSL 証明書を管理する
author: jenfieldmsft
ms.author: billmath
manager: samueld
ms.date: 10/02/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: a982df8ce7d1f335a1c2242f277b1983573c9ee1
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86954205"
---
# <a name="managing-ssl-certificates-in-ad-fs-and-wap-in-windows-server-2016"></a>Windows Server 2016 の AD FS と WAP で SSL 証明書を管理する



この記事では、AD FS と WAP サーバーに新しい SSL 証明書を展開する方法について説明します。

>[!NOTE]
>AD FS ファームで今後使用する SSL 証明書を置き換えるには、Azure AD Connect を使用することをお勧めします。  詳細については[、「Active Directory フェデレーションサービス (AD FS) (AD FS) ファームの SSL 証明書を更新](/azure/active-directory/connect/active-directory-aadconnectfed-ssl-update)する」を参照してください。

## <a name="obtaining-your-ssl-certificates"></a>SSL 証明書の取得
運用 AD FS ファームの場合は、公的に信頼された SSL 証明書を使用することをお勧めします。 これは通常、サードパーティの公開証明書プロバイダーに証明書署名要求 (CSR) を送信することによって取得されます。 Windows 7 以降の PC から、CSR を生成するにはさまざまな方法があります。 このことについては、ベンダーにドキュメントが必要です。

- 証明書が[AD FS と Web アプリケーションプロキシの SSL 証明書の要件](../overview/ad-fs-requirements.md#BKMK_1)を満たしていることを確認します。

### <a name="how-many-certificates-are-needed"></a>必要な証明書の数
すべての AD FS および Web アプリケーションプロキシサーバーで共通の SSL 証明書を使用することをお勧めします。 要件の詳細については、「ドキュメント[AD FS」と「Web アプリケーションプロキシの SSL 証明書の要件](../overview/ad-fs-requirements.md#BKMK_1)」を参照してください。

### <a name="ssl-certificate-requirements"></a>SSL 証明書の要件
名前付け、信頼のルート、および拡張機能を含む要件については、ドキュメント[AD FS と Web アプリケーションプロキシの SSL 証明書の要件](../overview/ad-fs-requirements.md#BKMK_1)を参照してください。

## <a name="replacing-the-ssl-certificate-for-ad-fs"></a>AD FS の SSL 証明書の置き換え
> [!NOTE]
> AD FS SSL 証明書は、AD FS 管理スナップインで見つかる AD FS サービス通信証明書と同じものではありません。 AD FS SSL 証明書を変更するには、PowerShell を使用する必要があります。

まず、AD FS サーバーで実行されている証明書バインドモード (既定の証明書認証バインドまたは代替クライアント TLS バインドモード) を決定します。

### <a name="replacing-the-ssl-certificate-for-ad-fs-running-in-default-certificate-authentication-binding-mode"></a>既定の証明書認証バインドモードで実行されている AD FS の SSL 証明書を置き換える
AD FS 既定では、ポート443でのデバイス証明書の認証と、ポート 49443 (または443ではない構成可能なポート) でのユーザー証明書の認証が実行されます。
このモードでは、powershell コマンドレット Set-adfssslcertificate を使用して SSL 証明書を管理します。

次の手順に従います。

1. まず、新しい証明書を取得する必要があります。 これは通常、サードパーティの公開証明書プロバイダーに証明書署名要求 (CSR) を送信することによって行われます。 Windows 7 以降の PC から、CSR を生成するにはさまざまな方法があります。 このことについては、ベンダーにドキュメントが必要です。

    * 証明書が[AD FS と Web アプリケーションプロキシの SSL 証明書の要件](../overview/ad-fs-requirements.md#BKMK_1)を満たしていることを確認します。

1. 証明書プロバイダーから応答を取得したら、各 AD FS および Web アプリケーションプロキシサーバーのローカルコンピューターストアにインポートします。

1. **プライマリ**AD FS サーバーで、次のコマンドレットを使用して、新しい SSL 証明書をインストールします。

```powershell
Set-AdfsSslCertificate -Thumbprint '<thumbprint of new cert>'
```

証明書の拇印は、次のコマンドを実行することで見つけることができます。

```powershell
dir Cert:\LocalMachine\My\
```

#### <a name="additional-notes"></a>追加情報

* Set-adfssslcertificate コマンドレットは、マルチノードコマンドレットです。これは、プライマリから実行するだけで、ファーム内のすべてのノードが更新されることを意味します。 これは、サーバー2016で新たに追加されたものです。 サーバー 2012 R2 では、各サーバーで Set-adfssslcertificate を実行する必要がありました。
* Set-adfssslcertificate コマンドレットは、プライマリサーバーでのみ実行する必要があります。 プライマリサーバーはサーバー2016を実行している必要があり、ファームの動作レベルは2016に上げる必要があります。
* Set-adfssslcertificate コマンドレットは、PowerShell リモート処理を使用して他の AD FS サーバーを構成し、他のノードでポート 5985 (TCP) が開いていることを確認します。
* Set-adfssslcertificate コマンドレットは、adfssrv プリンシパルに SSL 証明書の秘密キーへの読み取りアクセス許可を付与します。 このプリンシパルは、AD FS サービスを表します。 AD FS サービスアカウントに、SSL 証明書の秘密キーへの読み取りアクセス権を付与する必要はありません。

### <a name="replacing-the-ssl-certificate-for-ad-fs-running-in-alternate-tls-binding-mode"></a>代替 TLS バインドモードで実行されている AD FS の SSL 証明書を置き換える
代替クライアント TLS バインドモードで構成されている場合、AD FS はポート443でデバイス証明書認証を実行し、別のホスト名でポート443でもユーザー証明書認証を実行します。 ユーザー証明書のホスト名は、"certauth.fs.contoso.com" など、"certauth" で事前に付加された AD FS ホスト名です。
このモードでは、powershell コマンドレット AdfsAlternateTlsClientBinding を使用して SSL 証明書を管理します。 これにより、代替のクライアント TLS バインドだけでなく、AD FS が SSL 証明書を設定するその他のすべてのバインドも管理されます。

次の手順に従います。

1. まず、新しい証明書を取得する必要があります。 これは通常、サードパーティの公開証明書プロバイダーに証明書署名要求 (CSR) を送信することによって行われます。 Windows 7 以降の PC から、CSR を生成するにはさまざまな方法があります。 このことについては、ベンダーにドキュメントが必要です。

    * 証明書が[AD FS と Web アプリケーションプロキシの SSL 証明書の要件](../overview/ad-fs-requirements.md#BKMK_1)を満たしていることを確認します。

1. 証明書プロバイダーから応答を取得したら、各 AD FS および Web アプリケーションプロキシサーバーのローカルコンピューターストアにインポートします。

1. **プライマリ**AD FS サーバーで、次のコマンドレットを使用して、新しい SSL 証明書をインストールします。

```powershell
Set-AdfsAlternateTlsClientBinding -Thumbprint '<thumbprint of new cert>'
```

証明書の拇印は、次のコマンドを実行することで見つけることができます。

```powershell
dir Cert:\LocalMachine\My\
```

#### <a name="additional-notes"></a>追加情報

* AdfsAlternateTlsClientBinding コマンドレットは、マルチノードコマンドレットです。これは、プライマリから実行するだけで、ファーム内のすべてのノードが更新されることを意味します。
* AdfsAlternateTlsClientBinding コマンドレットは、プライマリサーバーでのみ実行する必要があります。 プライマリサーバーはサーバー2016を実行している必要があり、ファームの動作レベルは2016に上げる必要があります。
* AdfsAlternateTlsClientBinding コマンドレットは、PowerShell リモート処理を使用して他の AD FS サーバーを構成し、他のノードでポート 5985 (TCP) が開いていることを確認します。
* AdfsAlternateTlsClientBinding コマンドレットは、adfssrv プリンシパルに SSL 証明書の秘密キーへの読み取りアクセス許可を付与します。 このプリンシパルは、AD FS サービスを表します。 AD FS サービスアカウントに、SSL 証明書の秘密キーへの読み取りアクセス権を付与する必要はありません。

## <a name="replacing-the-ssl-certificate-for-the-web-application-proxy"></a>Web アプリケーションプロキシの SSL 証明書の置換
WAP で既定の証明書認証バインドと代替クライアント TLS バインドモードの両方を構成する場合は、WebApplicationProxySslCertificate コマンドレットを使用できます。
Web アプリケーションプロキシの SSL 証明書を置き換えるには、**各**Web アプリケーションプロキシサーバーで次のコマンドレットを使用して、新しい ssl 証明書をインストールします。

```powershell
Set-WebApplicationProxySslCertificate -Thumbprint '<thumbprint of new cert>'
```

古い証明書の有効期限が既に切れているために上記のコマンドレットが失敗した場合は、次のコマンドレットを使用してプロキシを再構成します。

```powershell
$cred = Get-Credential
```

AD FS サーバーのローカル管理者であるドメインユーザーの資格情報を入力します

```powershell
Install-WebApplicationProxy -FederationServiceTrustCredential $cred -CertificateThumbprint '<thumbprint of new cert>' -FederationServiceName 'fs.contoso.com'
```

## <a name="additional-references"></a>その他のリファレンス  
* [AD FS での証明書認証のための代替ホスト名バインドのサポート](../operations/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication.md)
* [AD FS と certificate KeySpec のプロパティ情報](../technical-reference/AD-FS-and-KeySpec-Property.md)
