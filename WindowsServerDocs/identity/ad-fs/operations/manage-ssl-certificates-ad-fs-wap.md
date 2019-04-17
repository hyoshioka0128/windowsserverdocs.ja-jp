---
ms.assetid: a3f50046-5d48-43d3-b0f8-ac2346b15285
title: "AD FS と WAP Windows Server 2016 での SSL 証明書の管理"
description: "AD FS と WAP Windows Server 2016 での SSL 証明書の管理"
author: jenfieldmsft
ms.author: billmath
manager: samueld
ms.date: 10/02/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 5156b3ad357ab8edb5e08a89a459beaf9b8c9b1a
ms.sourcegitcommit: ca7dc3d56a33924ae5fe0e9ffb1274da6dc4e54d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/03/2017
---
# <a name="managing-ssl-certificates-in-ad-fs-and-wap-in-windows-server-2016"></a>AD FS と WAP Windows Server 2016 での SSL 証明書の管理

>Windows Server 2016 の適用対象:

この記事では、AD FS と WAP サーバーに、新しい SSL 証明書を展開する方法について説明します。

>[!NOTE]
>今後は、AD FS ファーム用の SSL 証明書を置換する方法が推奨では、Azure AD Connect を使用します。  詳細については、次を参照してください[、Active Directory フェデレーション サービス (AD FS) ファーム用の SSL 証明書の更新。](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectfed-ssl-update)

## <a name="obtaining-your-ssl-certificates"></a>SSL 証明書を取得します。
運用環境の AD FS ファームの公的に信頼された SSL 証明書の使用をお勧めします。 これは通常、サード パーティへの証明書署名要求 (CSR)、パブリック証明書プロバイダーを送信することで取得されます。 さまざまな Windows 7 または上位のコンピューターを含む、CSR を生成する方法があります。 このドキュメントに、ベンダーが必要です。

- 証明書が満たしていることを確認、[AD FS と Web アプリケーション プロキシの SSL 証明書の要件](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1)

### <a name="how-many-certificates-are-needed"></a>どのくらいの証明書が必要
すべての AD FS と Web アプリケーション プロキシ サーバー間で共通の SSL 証明書を使用することをお勧めします。 要件の詳細については、ドキュメントを参照してください[AD FS と Web アプリケーション プロキシの SSL 証明書の要件。](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1)

### <a name="ssl-certificate-requirements"></a>SSL 証明書の要件
ルートの信頼関係と拡張機能などの名前付け要件については、ドキュメントを参照してください[AD FS と Web アプリケーション プロキシの SSL 証明書の要件](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1)

## <a name="replacing-the-ssl-certificate-for-ad-fs"></a>AD FS の SSL 証明書を置き換える
> [!NOTE]
> AD FS の SSL 証明書は、AD FS 管理スナップインで見つかった AD FS サービス通信証明書と同じではないです。 AD FS の SSL 証明書を変更するには、PowerShell を使用する必要があります。

まず、AD FS サーバーで実行している証明書をバインド モードを確認します。既定の証明書認証のバインド、またはクライアントが代替 TLS バインド モード。

### <a name="replacing-the-ssl-certificate-for-ad-fs-running-in-default-certificate-authentication-binding-mode"></a>既定の証明書認証バインド モードを実行している AD FS の SSL 証明書を置き換える
既定で AD FS では、ポート 443 でデバイス証明書の認証とポート 49443 でユーザー証明書の認証 (または、構成可能なポート 443 ではない) を実行します。
このモードで SSL 証明書を管理するのに Set-AdfsSslCertificate powershell コマンドレットを使用します。

次の手順に従います。

1. 最初に、新しい証明書を取得する必要があります。 これは通常、サード パーティへの証明書署名要求 (CSR)、パブリック証明書プロバイダーを送信することで行われます。 さまざまな Windows 7 または上位のコンピューターを含む、CSR を生成する方法があります。 このドキュメントに、ベンダーが必要です。

    * 証明書が満たしていることを確認、[AD FS と Web アプリケーション プロキシの SSL 証明書の要件](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1)

1. 証明書プロバイダーからの応答を取得した後は、各 AD FS と Web アプリケーション プロキシ サーバーのローカル コンピューター ストアにインポートします。

1. **プライマリ**AD FS サーバーで、次のコマンドレットを使用して、新しい SSL 証明書をインストールするには

```powershell
Set-AdfsSslCertificate -Thumbprint '<thumbprint of new cert>'
```

このコマンドを実行して、証明書の拇印を確認できます。

```powershell
dir Cert:\LocalMachine\My\
```

#### <a name="additional-notes"></a>追加の注意事項

* Set-AdfsSslCertificate コマンドレットは、マルチノード コマンドレットです。つまり、プライマリから実行するのには、ファーム内のすべてのノードが更新されます。 これは、Server 2016 の新機能です。 Server 2012 R2 では、各サーバーで Set-AdfsSslCertificate を実行する必要があります。
* Set-AdfsSslCertificate コマンドレットは、プライマリ サーバーでのみ実行するのには。 プライマリ サーバーが Server 2016 を実行してファームの動作のレベルは、2016年に発生します。
* Set-AdfsSslCertificate コマンドレットは、ポート 5985 (TCP) は、その他のノード上で開いているかどうかを確認、他の AD FS サーバーを構成する PowerShell リモート処理が使用されます。
* Set-AdfsSslCertificate コマンドレットは、adfssrv プリンシパルの読み取りアクセス許可の秘密キーへの SSL 証明書を与えられます。 このプリンシパルは、AD FS サービスを表します。 SSL 証明書の秘密キーに AD FS サービスのアカウント読み取りアクセス権を付与する必要はありません。

### <a name="replacing-the-ssl-certificate-for-ad-fs-running-in-alternate-tls-binding-mode"></a>代替の TLS バインド モードで実行されている AD FS の SSL 証明書を置き換える
TLS バインド モードの代替のクライアントで構成されている、AD FS は異なるホスト名でにポート 443 でデバイス証明書の認証とポート 443 で同様に、ユーザー証明書認証を実行します。 ユーザー証明書のホスト名は、AD FS ホスト名前に付加されます"certauth"、"certauth.fs.contoso.com"などとは
このモードで SSL 証明書を管理するのに Set-AdfsAlternateTlsClientBinding powershell コマンドレットを使用します。 代替のクライアントの TLS バインドだけでなくを AD FS 設定の SSL 証明書もその他のすべてのバインドを管理します。

次の手順に従います。

1. 最初に、新しい証明書を取得する必要があります。 これは通常、サード パーティへの証明書署名要求 (CSR)、パブリック証明書プロバイダーを送信することで行われます。 さまざまな Windows 7 または上位のコンピューターを含む、CSR を生成する方法があります。 このドキュメントに、ベンダーが必要です。

    * 証明書が満たしていることを確認、[AD FS と Web アプリケーション プロキシの SSL 証明書の要件](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-fs/overview/AD-FS-2016-Requirements#BKMK_1)

1. 証明書プロバイダーからの応答を取得した後は、各 AD FS と Web アプリケーション プロキシ サーバーのローカル コンピューター ストアにインポートします。

1. **プライマリ**AD FS サーバーで、次のコマンドレットを使用して、新しい SSL 証明書をインストールするには

```powershell
Set-AdfsAlternateTlsClientBinding -Thumbprint '<thumbprint of new cert>'
```

このコマンドを実行して、証明書の拇印を確認できます。

```powershell
dir Cert:\LocalMachine\My\
```

#### <a name="additional-notes"></a>追加の注意事項

* Set-AdfsAlternateTlsClientBinding コマンドレットは、マルチノード コマンドレットです。つまり、プライマリから実行するのには、ファーム内のすべてのノードが更新されます。
* Set-AdfsAlternateTlsClientBinding コマンドレットは、プライマリ サーバーでのみ実行するのには。 プライマリ サーバーが Server 2016 を実行してファームの動作のレベルは、2016年に発生します。
* Set-AdfsAlternateTlsClientBinding コマンドレットは、ポート 5985 (TCP) は、その他のノード上で開いているかどうかを確認、他の AD FS サーバーを構成する PowerShell リモート処理が使用されます。
* Set-AdfsAlternateTlsClientBinding コマンドレットは、adfssrv プリンシパルの読み取りアクセス許可の秘密キーへの SSL 証明書を与えられます。 このプリンシパルは、AD FS サービスを表します。 SSL 証明書の秘密キーに AD FS サービスのアカウント読み取りアクセス権を付与する必要はありません。

## <a name="replacing-the-ssl-certificate-for-the-web-application-proxy"></a>Web アプリケーション プロキシの SSL 証明書を置き換える
WAP で既定の証明書認証のバインディングまたは代替クライアント TLS バインド モードの両方を構成するため、Set-WebApplicationProxySslCertificate コマンドレットを使用できます。
Web アプリケーション プロキシの SSL 証明書を置換する**各**Web アプリケーション プロキシ サーバーでは、次のコマンドレットを使用して、新しい SSL 証明書をインストールします。

```powershell
Set-WebApplicationProxySslCertificate '<thumbprint of new cert>'
```

古い証明書の有効期限が切れているため、上記のコマンドレットが失敗した場合は、次のコマンドレットを使用して、プロキシを再構成します。

```powershell
$cred = Get-Credential
```

AD FS サーバーのローカル管理者であるドメイン ユーザーの資格情報を入力してください。

```powershell
Install-WebApplicationProxy -FederationServiceTrustCredential $cred -CertificateThumbprint '<thumbprint of new cert>' -FederationServiceName 'fs.contoso.com'
```

## <a name="additional-references"></a>その他の参照  
* [AD FS の証明書認証用の代替ホスト名バインドのサポートします。](../operations/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication.md)
* [AD FS と証明書の KeySpec プロパティについて](../technical-reference/AD-FS-and-KeySpec-Property.md)
