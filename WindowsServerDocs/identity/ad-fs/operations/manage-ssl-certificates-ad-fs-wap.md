---
ms.assetid: a3f50046-5d48-43d3-b0f8-ac2346b15285
title: Windows Server 2016 の AD FS と WAP で SSL 証明書を管理する
description: Windows Server 2016 の AD FS と WAP で SSL 証明書を管理する
author: jenfieldmsft
ms.author: billmath
manager: samueld
ms.date: 10/02/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: abcff8632bc8a3a75af4eee30c3aed046ca0ccc9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877343"
---
# <a name="managing-ssl-certificates-in-ad-fs-and-wap-in-windows-server-2016"></a>Windows Server 2016 の AD FS と WAP で SSL 証明書を管理する

>適用先:Windows Server 2016

この記事では、AD FS と WAP のサーバーに新しい SSL 証明書をデプロイする方法について説明します。

>[!NOTE]
>今後、AD FS ファームの SSL 証明書を置換することをお勧めの方法は、Azure AD Connect を使用します。  詳細については、次を参照してください[、Active Directory フェデレーション サービス (AD FS) ファームの SSL 証明書の更新。](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectfed-ssl-update)

## <a name="obtaining-your-ssl-certificates"></a>SSL 証明書を取得します。
運用環境の AD FS ファームでは、公的に信頼された SSL 証明書の使用をお勧めします。 これは通常、サード パーティに証明書署名要求 (CSR)、プロバイダーの公開証明書を送信することで取得されます。 さまざまな Windows 7 または上位のコンピューターを含む、CSR を生成する方法があります。 このドキュメントに、ベンダーが必要です。

- 証明書が満たしていることを確認、 [AD FS と Web アプリケーション プロキシの SSL 証明書の要件](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1)

### <a name="how-many-certificates-are-needed"></a>証明書の数が必要です。
すべての AD FS と Web アプリケーション プロキシ サーバーの間で共通の SSL 証明書を使用することをお勧めします。 要件の詳細については、ドキュメントを参照してください[AD FS と Web アプリケーション プロキシの SSL 証明書の要件。](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1)

### <a name="ssl-certificate-requirements"></a>SSL 証明書の要件
要件の名前付けなど、信頼および拡張機能のルートはドキュメントをご覧ください[AD FS と Web アプリケーション プロキシの SSL 証明書の要件。](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1)

## <a name="replacing-the-ssl-certificate-for-ad-fs"></a>AD FS の SSL 証明書を置換
> [!NOTE]
> AD FS SSL 証明書は、AD FS 管理スナップインで見つかった AD FS サービス通信証明書と同じではありません。 AD FS SSL 証明書を変更するには PowerShell を使用する必要があります。

まず、AD FS サーバーで実行して証明書をバインド モードを決定します。 既定の証明書認証のバインド、またはクライアントが代替 TLS バインド モード。

### <a name="replacing-the-ssl-certificate-for-ad-fs-running-in-default-certificate-authentication-binding-mode"></a>既定の証明書認証のバインド モードを実行して AD FS の SSL 証明書を置換
既定で AD FS では、デバイス証明書認証をポート 443 とポート 49443 でユーザー証明書認証 (または、構成可能なポート 443 ではない) を実行します。
このモードでは、SSL 証明書を管理するのに Set-adfssslcertificate powershell コマンドレットを使用します。

次の手順を実行します。

1. 最初に、新しい証明書を取得する必要があります。 これは通常、サード パーティに証明書署名要求 (CSR)、プロバイダーの公開証明書を送信することで行われます。 さまざまな Windows 7 または上位のコンピューターを含む、CSR を生成する方法があります。 このドキュメントに、ベンダーが必要です。

    * 証明書が満たしていることを確認、 [AD FS と Web アプリケーション プロキシの SSL 証明書の要件](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1)

1. 証明書プロバイダーからの応答を取得した後は、各 AD FS および Web アプリケーション プロキシ サーバーのローカル コンピューター ストアにインポートします。

1. **プライマリ**AD FS サーバーで、次のコマンドレットを使用して、新しい SSL 証明書をインストールするには

```powershell
Set-AdfsSslCertificate -Thumbprint '<thumbprint of new cert>'
```

このコマンドを実行して証明書の拇印が見つかります。

```powershell
dir Cert:\LocalMachine\My\
```

#### <a name="additional-notes"></a>その他のメモ

* Set-adfssslcertificate コマンドレットは、マルチノード コマンドレットです。つまり、プライマリから実行するのには、ファーム内のすべてのノードが更新されます。 Server 2016 の新機能です。 Server 2012 R2 では、Set-adfssslcertificate を各サーバーで実行する必要があります。
* Set-adfssslcertificate コマンドレットは、プライマリ サーバーでのみ実行する必要があります。 Server 2016 が実行されているプライマリ サーバーにあるし、ファーム動作レベル 2016年に発生する必要があります。
* Set-adfssslcertificate コマンドレットは、その他の AD FS サーバーを構成するには、ポート 5985 (TCP) を他のノード上で開いて PowerShell リモート処理を使用します。
* Set-adfssslcertificate コマンドレットは adfssrv プリンシパル読み取りアクセス許可を付与の秘密キーへの SSL 証明書。 このプリンシパルは、AD FS サービスを表します。 SSL 証明書の秘密キーへの AD FS サービス アカウントの読み取りアクセスを付与する必要はありません。

### <a name="replacing-the-ssl-certificate-for-ad-fs-running-in-alternate-tls-binding-mode"></a>代替の TLS バインド モードで実行されている AD FS の SSL 証明書を置換
TLS バインド モード別のクライアントで構成されている、AD FS は別のホスト名にポート 443 でデバイス証明書の認証とポート 443 を同様に、ユーザーの証明書認証を実行します。 ユーザー証明書のホスト名は、AD FS ホスト名付けた"certauth"、"certauth.fs.contoso.com"などとです。
このモードでは、SSL 証明書を管理するのに powershell コマンドレット セット AdfsAlternateTlsClientBinding を使用します。 だけでなく、代替のクライアントの TLS バインド、AD FS の SSL 証明書の設定をその他のすべてのバインドを管理します。

次の手順を実行します。

1. 最初に、新しい証明書を取得する必要があります。 これは通常、サード パーティに証明書署名要求 (CSR)、プロバイダーの公開証明書を送信することで行われます。 さまざまな Windows 7 または上位のコンピューターを含む、CSR を生成する方法があります。 このドキュメントに、ベンダーが必要です。

    * 証明書が満たしていることを確認、 [AD FS と Web アプリケーション プロキシの SSL 証明書の要件](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1)

1. 証明書プロバイダーからの応答を取得した後は、各 AD FS および Web アプリケーション プロキシ サーバーのローカル コンピューター ストアにインポートします。

1. **プライマリ**AD FS サーバーで、次のコマンドレットを使用して、新しい SSL 証明書をインストールするには

```powershell
Set-AdfsAlternateTlsClientBinding -Thumbprint '<thumbprint of new cert>'
```

このコマンドを実行して証明書の拇印が見つかります。

```powershell
dir Cert:\LocalMachine\My\
```

#### <a name="additional-notes"></a>その他のメモ

* セット AdfsAlternateTlsClientBinding コマンドレットは、マルチノード コマンドレットです。つまり、プライマリから実行するのには、ファーム内のすべてのノードが更新されます。
* セット AdfsAlternateTlsClientBinding コマンドレットは、プライマリ サーバーでのみ実行する必要があります。 Server 2016 が実行されているプライマリ サーバーにあるし、ファーム動作レベル 2016年に発生する必要があります。
* セット AdfsAlternateTlsClientBinding コマンドレットは、その他の AD FS サーバーを構成するには、ポート 5985 (TCP) を他のノード上で開いて PowerShell リモート処理を使用します。
* セット AdfsAlternateTlsClientBinding コマンドレットは adfssrv プリンシパル読み取りアクセス許可を付与の秘密キーへの SSL 証明書。 このプリンシパルは、AD FS サービスを表します。 SSL 証明書の秘密キーへの AD FS サービス アカウントの読み取りアクセスを付与する必要はありません。

## <a name="replacing-the-ssl-certificate-for-the-web-application-proxy"></a>Web アプリケーション プロキシの SSL 証明書を置換
WAP の証明書認証のバインドの既定または代替クライアント TLS バインド モードの両方を構成するため、セット WebApplicationProxySslCertificate コマンドレットを使用できます。
Web アプリケーション プロキシの SSL 証明書を置換する**各**Web アプリケーション プロキシ サーバーでは、次のコマンドレットを使用して、新しい SSL 証明書をインストールします。

```powershell
Set-WebApplicationProxySslCertificate '<thumbprint of new cert>'
```

上記のコマンドレットでは、古い証明書が既に切れているため失敗した場合、次のコマンドレットを使用してプロキシを再構成します。

```powershell
$cred = Get-Credential
```

AD FS サーバーのローカル管理者であるドメイン ユーザーの資格情報を入力します。

```powershell
Install-WebApplicationProxy -FederationServiceTrustCredential $cred -CertificateThumbprint '<thumbprint of new cert>' -FederationServiceName 'fs.contoso.com'
```

## <a name="additional-references"></a>その他の参照情報  
* [AD FS で証明書の認証の代替ホスト名バインドのサポートします。](../operations/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication.md)
* [AD FS と証明書 KeySpec プロパティ情報](../technical-reference/AD-FS-and-KeySpec-Property.md)
