---
title: セキュリティ サポート プロバイダー インターフェイスのアーキテクチャ
description: Windows Server のセキュリティ
ms.prod: windows-server
ms.technology: security-windows-auth
ms.topic: article
ms.assetid: de09e099-5711-48f8-adbd-e7b8093a0336
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 89e6696c286cae7c3e89346d2044869082cdd8bc
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861735"
---
# <a name="security-support-provider-interface-architecture"></a>セキュリティ サポート プロバイダー インターフェイスのアーキテクチャ

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

IT プロフェッショナル向けのこのリファレンストピックでは、セキュリティサポートプロバイダインターフェイス (SSPI) アーキテクチャで使用される Windows 認証プロトコルについて説明します。

Microsoft セキュリティサポートプロバイダインターフェイス (SSPI) は、Windows 認証の基礎となります。 認証を必要とするアプリケーションとインフラストラクチャサービスは、SSPI を使用して提供します。

SSPI は、Windows Server オペレーティングシステムでの汎用セキュリティサービス API (GSSAPI) の実装です。 GSSAPI の詳細については、IETF RFC データベースの RFC 2743 および RFC 2744 を参照してください。

Windows で特定の認証プロトコルを呼び出す既定のセキュリティサポートプロバイダー (Ssp) は、SSPI に Dll として組み込まれています。 これらの既定の Ssp については、次のセクションで説明します。 SSPI を使用して操作できる場合は、追加の Ssp を組み込むことができます。

次の図に示すように、Windows の SSPI は、クライアントコンピューターとサーバー間の既存の通信チャネルで認証トークンを伝達するメカニズムを提供します。 2台のコンピューターまたはデバイスが安全に通信できるように認証する必要がある場合、認証要求は SSPI にルーティングされます。これにより、現在使用されているネットワークプロトコルに関係なく、認証プロセスが完了します。 SSPI は、透過的なバイナリラージオブジェクトを返します。 これらはアプリケーション間で渡され、その時点で SSPI レイヤーに渡すことができます。 そのため、SSPI を使用すると、アプリケーションは、インターフェイスをセキュリティシステムに変更することなく、コンピューターまたはネットワーク上で使用可能なさまざまなセキュリティモデルを使用できます。

![セキュリティサポートプロバイダーインターフェイスのアーキテクチャを示す図](../media/security-support-provider-interface-architecture/AuthN_SecuritySupportProviderInterfaceArchitecture.jpg)

次のセクションでは、SSPI と対話する既定の Ssp について説明します。 Windows オペレーティングシステムでは、セキュリティ保護されていないネットワーク環境で安全な通信を促進するために、さまざまな方法で Ssp が使用されます。

-   [Kerberos セキュリティサポートプロバイダ](#BKMK_KerbSSP)

-   [NTLM セキュリティサポートプロバイダ](#BKMK_NTLMSSP)

-   [ダイジェストセキュリティサポートプロバイダ](#BKMK_DigestSSP)

-   [Schannel セキュリティサポートプロバイダ](#BKMK_SchannelSSP)

-   [セキュリティサポートプロバイダーのネゴシエート](#BKMK_NegoSSP)

-   [資格情報セキュリティサポートプロバイダ](#BKMK_CredSSP)

-   [Negotiate Extension セキュリティサポートプロバイダ](#BKMK_NegoExtsSSP)

-   [PKU2U セキュリティサポートプロバイダ](#BKMK_PKU2USSP)

このトピックには次のものも含まれます。

[セキュリティサポートプロバイダーの選択](security-support-provider-interface-architecture.md#BKMK_SecuritySupportProviderSelection)

### <a name="kerberos-security-support-provider"></a><a name="BKMK_KerbSSP"></a>Kerberos セキュリティサポートプロバイダ
この SSP は、Microsoft によって実装されている Kerberos version 5 プロトコルのみを使用します。 このプロトコルは、ネットワーク作業グループの RFC 4120 と下書きのリビジョンに基づいています。 これは、対話型ログオンのパスワードまたはスマートカードと共に使用される業界標準のプロトコルです。 また、Windows でのサービスの推奨される認証方法でもあります。

Kerberos プロトコルは Windows 2000 以降の既定の認証プロトコルであるため、すべてのドメインサービスで Kerberos SSP がサポートされています。 これらのサービスには、次のようなものがあります。

-   ライトウェイトディレクトリアクセスプロトコル (LDAP) を使用する Active Directory クエリ

-   リモートプロシージャコールサービスを使用するリモートサーバーまたはワークステーションの管理

-   印刷サービス

-   クライアント/サーバー認証

-   サーバーメッセージブロック (SMB) プロトコル (共通インターネットファイルシステムまたは CIFS とも呼ばれます) を使用するリモートファイルアクセス

-   分散ファイルシステムの管理と紹介

-   インターネットインフォメーションサービスするためのイントラネット認証 (IIS)

-   インターネットプロトコルセキュリティのセキュリティ機関認証 (IPsec)

-   ドメインユーザーとコンピューターの証明書サービスを Active Directory するための証明書要求

場所:%windir%\Windows\System32\kerberos.dll

このプロバイダーは、このトピックの冒頭にある「**適用対象**」の一覧に記載されているバージョンと、windows Server 2003 および windows XP に既定で含まれています。

**Kerberos プロトコルと Kerberos SSP に関するその他のリソース**

-   [Microsoft Kerberos (Windows)](https://msdn.microsoft.com/library/aa378747(VS.85).aspx)

-   [\[MS-16\]: Kerberos プロトコル拡張機能](https://msdn.microsoft.com/library/cc233855(PROT.10).aspx)

-   [\[MS SFU\]: Kerberos プロトコル拡張機能: ユーザーと制約付き委任プロトコルの仕様のサービス](https://msdn.microsoft.com/library/cc246071(PROT.13).aspx)

-   [Kerberos SSP/AP (Windows)](https://msdn.microsoft.com/library/aa377942(VS.85).aspx)

-   Windows Vista の[Kerberos の機能強化](https://technet.microsoft.com/library/cc749438(v=ws.10).aspx)

-   Windows 7 の[Kerberos 認証の変更点](https://technet.microsoft.com/library/dd560670(v=ws.10).aspx) 

-   [Kerberos 認証のテクニカルリファレンス](https://technet.microsoft.com/library/cc739058(v=ws.10).aspx)

### <a name="ntlm-security-support-provider"></a><a name="BKMK_NTLMSSP"></a>NTLM セキュリティサポートプロバイダ
Ntlm セキュリティサポートプロバイダー (NTLM SSP) は、NTLM チャレンジ応答認証を許可し、整合性と機密性のオプションをネゴシエートするために、セキュリティサポートプロバイダーインターフェイス (SSPI) によって使用されるバイナリメッセージングプロトコルです。 NTLM は、サーバーメッセージブロックや CIFS 認証、HTTP ネゴシエート認証 (インターネット Web 認証など)、リモートプロシージャコールサービスなど、SSPI 認証が使用される場所で使用されます。 NTLM SSP には、NTLM と NTLM バージョン 2 (NTLMv2) の認証プロトコルが含まれています。

サポートされている Windows オペレーティングシステムでは、次の場合に NTLM SSP を使用できます。

-   クライアント/サーバー認証

-   印刷サービス

-   CIFS (SMB) を使用したファイルアクセス

-   リモートプロシージャコールサービスまたは DCOM サービスをセキュリティで保護する

場所:%windir%\Windows\System32\ msv1_0

このプロバイダーは、このトピックの冒頭にある「**適用対象**」の一覧に記載されているバージョンと、windows Server 2003 および windows XP に既定で含まれています。

**NTLM プロトコルと NTLM SSP に関するその他のリソース**

-   [MSV1_0 認証パッケージ (Windows)](https://msdn.microsoft.com/library/aa378753(VS.85).aspx)

-   Windows 7 での[NTLM 認証の変更点](https://technet.microsoft.com/library/dd566199(v=ws.10).aspx) 

-   [Microsoft NTLM (Windows)](https://msdn.microsoft.com/library/aa378749(VS.85).aspx)

-   [NTLM 使用法ガイドの監査と制限](https://technet.microsoft.com/library/jj865674(v=ws.10).aspx)

### <a name="digest-security-support-provider"></a><a name="BKMK_DigestSSP"></a>ダイジェストセキュリティサポートプロバイダ
ダイジェスト認証は、ライトウェイトディレクトリアクセスプロトコル (LDAP) と web 認証に使用される業界標準です。 ダイジェスト認証は、MD5 ハッシュまたはメッセージダイジェストとして、ネットワーク経由で資格情報を転送します。

次の場合にダイジェスト SSP (Wdigest .dll) が使用されます。

-   Internet Explorer とインターネットインフォメーションサービス (IIS) へのアクセス

-   LDAP クエリ

場所:%windir%\Windows\System32\Digest.dll

このプロバイダーは、このトピックの冒頭にある「**適用対象**」の一覧に記載されているバージョンと、windows Server 2003 および windows XP に既定で含まれています。

**ダイジェストプロトコルとダイジェスト SSP に関するその他のリソース**

-   [Microsoft ダイジェスト認証 (Windows)](https://msdn.microsoft.com/library/aa378745(VS.85).aspx)

-   [\[MS-DPSP\]: ダイジェストプロトコルの拡張機能](https://msdn.microsoft.com/library/cc227906(PROT.13).aspx)

### <a name="schannel-security-support-provider"></a><a name="BKMK_SchannelSSP"></a>Schannel セキュリティサポートプロバイダ
セキュリティで保護されたチャネル (Schannel) は、ユーザーがセキュリティで保護された web サーバーにアクセスしようとした場合など、web ベースのサーバー認証に使用されます。

TLS プロトコル、SSL プロトコル、プライベート通信テクノロジ (PCT) プロトコル、およびデータグラムトランスポート層 (DTLS) プロトコルは、公開キー暗号化に基づいています。 Schannel には、これらすべてのプロトコルが用意されています。 どの Schannel プロトコルでも、クライアント/サーバー モデルが使用されています。 Schannel SSP では、公開キー証明書を使用して利用者を認証します。 パーティを認証するときに、Schannel SSP は次の優先順位でプロトコルを選択します。

-   TLS (Transport Layer Security) バージョン1.0

-   TLS (Transport Layer Security) バージョン1.1

-   TLS (Transport Layer Security) バージョン1.2

-   Secure Socket Layer (SSL) バージョン2.0

-   Secure Socket Layer (SSL) バージョン3.0

-   プライベート通信テクノロジ (PCT)

    **メモ**既定では、PCT は無効になっています。

選択されたプロトコルは、クライアントとサーバーがサポートできる優先認証プロトコルです。 たとえば、サーバーがすべての Schannel プロトコルをサポートし、クライアントが SSL 3.0 と SSL 2.0 のみをサポートしている場合、認証プロセスでは SSL 3.0 が使用されます。

DTLS は、アプリケーションによって明示的に呼び出されたときに使用されます。 DTLS と Schannel プロバイダーで使用されるその他のプロトコルの詳細については、「 [Schannel Security Support Provider テクニカルリファレンス](../tls/schannel-security-support-provider-technical-reference.md)」を参照してください。

場所:%windir%\Windows\System32\Schannel.dll

このプロバイダーは、このトピックの冒頭にある「**適用対象**」の一覧に記載されているバージョンと、windows Server 2003 および windows XP に既定で含まれています。

> [!NOTE]
> TLS 1.2 は、Windows Server 2008 R2 および Windows 7 のこのプロバイダーで導入されました。 DTLS は、Windows Server 2012 および Windows 8 のこのプロバイダーで導入されました。

**TLS および SSL プロトコルと Schannel SSP に関するその他のリソース**

-   [セキュリティで保護されたチャネル (Windows)](https://msdn.microsoft.com/library/aa380123(VS.85).aspx)

-   [TLS/SSL テクニカルリファレンス](https://technet.microsoft.com/library/cc784149(v=ws.10).aspx)

-   [\[MS TLSP\]: Transport Layer Security (TLS) プロファイル](https://msdn.microsoft.com/library/dd207968(PROT.13).aspx)

### <a name="negotiate-security-support-provider"></a><a name="BKMK_NegoSSP"></a>セキュリティサポートプロバイダーのネゴシエート
Simple and Protected GSS API ネゴシエーションメカニズム (SPNEGO) は、特定の認証プロトコルのネゴシエーションに使用できる Negotiate SSP の基礎を形成します。 アプリケーションが SSPI を呼び出してネットワークにログオンするときに、要求を処理する SSP を指定できます。 アプリケーションで Negotiate SSP が指定されている場合は、要求を分析し、顧客が構成したセキュリティポリシーに基づいて、要求を処理するための適切なプロバイダーを選択します。

SPNEGO は、RFC 2478 で指定されています。

サポートされている Windows オペレーティングシステムのバージョンでは、ネゴシエートセキュリティサポートプロバイダーが Kerberos プロトコルと NTLM のどちらかを選択します。 ネゴシエートでは、認証に関係するシステムのいずれかでプロトコルを使用できない場合、または呼び出し元のアプリケーションが Kerberos プロトコルを使用するための十分な情報を提供しなかった場合を除き、Kerberos プロトコルが既定で選択されます。

場所:%windir%\Windows\System32\lsasrv.dll

このプロバイダーは、このトピックの冒頭にある「**適用対象**」の一覧に記載されているバージョンと、windows Server 2003 および windows XP に既定で含まれています。

**Negotiate SSP に関するその他のリソース**

-   [Microsoft Negotiate (Windows)](https://msdn.microsoft.com/library/aa378748(VS.85).aspx)

-   [\[MS-SPNG\]: Simple および Protected GSS-API ネゴシエーションメカニズム (SPNEGO) の拡張機能](https://msdn.microsoft.com/library/cc247021(PROT.13).aspx)

-   [\[N2HT\]: Negotiate と Nego2 HTTP 認証プロトコルの仕様](https://msdn.microsoft.com/library/dd303576(PROT.13).aspx)

### <a name="credential-security-support-provider"></a><a name="BKMK_CredSSP"></a>資格情報セキュリティサポートプロバイダ
Credential Security Service Provider (CredSSP) は、新しいターミナルサービスとリモートデスクトップサービスセッションを開始するときにシングルサインオン (SSO) ユーザーエクスペリエンスを提供します。 CredSSP を使用すると、アプリケーションは、クライアントのポリシーに基づいて、(クライアント側の SSP を使用して) クライアントコンピューターからターゲットサーバーにユーザーの資格情報を委任することができます。 CredSSP ポリシーはグループポリシーを使用して構成され、資格情報の委任は既定で無効になっています。

場所:%windir%\Windows\System32\credssp.dll

このプロバイダーは、このトピックの冒頭にある「**適用対象**」の一覧に指定されているバージョンに既定で含まれています。

**資格情報 SSP に関するその他のリソース**

-   [\[MS-CSSP\]: Credential Security Support Provider (CredSSP) プロトコル仕様](https://msdn.microsoft.com/library/cc226764(PROT.13).aspx)

-   [資格情報セキュリティサービスプロバイダーとターミナルサービスログオン用 SSO](https://technet.microsoft.com/library/cc749211(v=ws.10).aspx)

### <a name="negotiate-extensions-security-support-provider"></a><a name="BKMK_NegoExtsSSP"></a>Negotiate Extension セキュリティサポートプロバイダ
Negotiate Extensions (NegoExts) は、Microsoft およびその他のソフトウェア会社によって実装されているアプリケーションとシナリオについて、NTLM または Kerberos プロトコル以外の Ssp の使用をネゴシエートする認証パッケージです。

この Negotiate パッケージに対するこの拡張機能では、次のシナリオが許可されます。

-   **フェデレーションシステム内でのリッチクライアントの可用性。** ドキュメントは、SharePoint サイトでアクセスできます。また、フル機能の Microsoft Office アプリケーションを使用して編集することもできます。

-   **Microsoft Office services のリッチクライアントのサポート。** ユーザーは Microsoft Office services にサインインし、フル機能の Microsoft Office アプリケーションを使用できます。

-   **ホストされている Microsoft Exchange Server および Outlook。** Exchange Server が web でホストされているため、ドメインの信頼が確立されていません。 Outlook では、Windows Live サービスを使用してユーザーを認証します。

-   **クライアントコンピューターとサーバーの間のリッチクライアントの可用性。** オペレーティングシステムのネットワークと認証のコンポーネントが使用されます。

Windows Negotiate パッケージでは、Kerberos と NTLM の場合と同じ方法で NegoExts SSP を扱います。 スタートアップ時に、ローカルシステム権限 (LSA) に NegoExts dll が読み込まれます。 要求のソースに基づいて認証要求を受信すると、サポートされている Ssp 間で NegoExts がネゴシエートします。 資格情報とポリシーを収集して暗号化し、セキュリティトークンが作成された適切な SSP にその情報を送信します。

NegoExts でサポートされている Ssp は、Kerberos や NTLM などのスタンドアロンの Ssp ではありません。 そのため、NegoExts SSP では、何らかの理由で認証方法が失敗すると、認証エラーメッセージが表示されるか、ログに記録されます。 再ネゴシエーションまたは代替の認証方法は使用できません。

場所:%windir%\Windows\System32\negoexts.dll

このプロバイダーは、このトピックの冒頭にある「**適用対象**」の一覧に記載されているバージョンに既定で含まれています (windows Server 2008 と windows Vista は除く)。

### <a name="pku2u-security-support-provider"></a><a name="BKMK_PKU2USSP"></a>PKU2U セキュリティサポートプロバイダ
PKU2U プロトコルは、Windows 7 および Windows Server 2008 R2 の SSP として導入され、実装されています。 この SSP は、特に Windows 7 で導入されたホームグループと呼ばれるメディアおよびファイル共有機能を通じて、ピアツーピア認証を有効にします。 この機能は、ドメインのメンバーではないコンピューター間での共有を許可します。

場所:%windir%\Windows\System32\pku2u.dll

このプロバイダーは、このトピックの冒頭にある「**適用対象**」の一覧に記載されているバージョンに既定で含まれています (windows Server 2008 と windows Vista は除く)。

**PKU2U プロトコルと PKU2U SSP に関するその他のリソース**

-   [オンライン Id 統合の概要](https://technet.microsoft.com/library/dd560662(v=ws.10).aspx)

## <a name="security-support-provider-selection"></a><a name="BKMK_SecuritySupportProviderSelection"></a>セキュリティサポートプロバイダーの選択
Windows SSPI では、インストールされているセキュリティサポートプロバイダーでサポートされているプロトコルのいずれかを使用できます。 ただし、すべてのオペレーティングシステムが Windows Server を実行している特定のコンピューターと同じ SSP パッケージをサポートしているわけではないため、クライアントとサーバーは両方がサポートしているプロトコルを使用するためにネゴシエーションを行う必要があります。 Windows Server では、可能な場合、クライアントコンピューターとアプリケーションは、強力な標準ベースのプロトコルである Kerberos プロトコルを使用することを推奨しますが、オペレーティングシステムは、Kerberos プロトコルをサポートしていないクライアントコンピューターとクライアントアプリケーションの認証を引き続き許可します。

認証を行う前に、2つの通信コンピューターが両方のプロトコルでサポートできるプロトコルに同意する必要があります。 SSPI を介して任意のプロトコルを使用できるようにするには、各コンピューターに適切な SSP が必要です。 たとえば、クライアントコンピューターとサーバーが Kerberos 認証プロトコルを使用するには、Kerberos v5 がサポートされている必要があります。 Windows Server では、関数**EnumerateSecurityPackages**を使用して、コンピューターでサポートされている ssp と、それらの ssp の機能を識別します。

認証プロトコルの選択は、次の2つの方法のいずれかで処理できます。

1.  [単一の認証プロトコル](#BKMK_SingleAuth)

2.  [Negotiate オプション](#BKMK_Negotiate)

### <a name="single-authentication-protocol"></a><a name="BKMK_SingleAuth"></a>単一の認証プロトコル
サーバーで1つの許容されるプロトコルが指定されている場合、クライアントコンピューターは指定されたプロトコルをサポートする必要があります。指定しない場合、通信は失敗します。 1つの許容されるプロトコルを指定すると、認証の交換は次のように行われます。

1.  クライアントコンピューターは、サービスへのアクセスを要求します。

2.  サーバーは要求に応答し、使用されるプロトコルを指定します。

3.  クライアントコンピューターは、応答の内容を調べ、指定されたプロトコルをサポートしているかどうかを確認します。 クライアントコンピューターが指定されたプロトコルをサポートしている場合は、認証が続行されます。 クライアントコンピューターでプロトコルがサポートされていない場合、クライアントコンピューターにリソースへのアクセスが許可されているかどうかに関係なく、認証は失敗します。

### <a name="negotiate-option"></a><a name="BKMK_Negotiate"></a>Negotiate オプション
Negotiate オプションを使用すると、クライアントとサーバーが許容されるプロトコルを検索することができます。 これは、単純および保護された GSS API ネゴシエーションメカニズム (SPNEGO) に基づいています。 認証プロトコルに対してネゴシエートするオプションで認証が開始されると、SPNEGO の交換は次のように行われます。

1.  クライアントコンピューターは、サービスへのアクセスを要求します。

2.  サーバーは、最初に選択されたプロトコルに基づいて、サポート可能な認証プロトコルの一覧と認証チャレンジまたは応答を返します。 たとえば、サーバーが Kerberos プロトコルと NTLM を一覧表示し、Kerberos 認証応答を送信する場合があります。

3.  クライアントコンピューターは、応答の内容を調べ、指定されたプロトコルのいずれかをサポートしているかどうかを確認します。

    -   クライアントコンピューターが優先プロトコルをサポートしている場合は、認証が続行されます。

    -   クライアントコンピューターが優先プロトコルをサポートしていないが、サーバーによって一覧表示されている他のプロトコルのいずれかをサポートしている場合、クライアントコンピューターは、サーバーがサポートしている認証プロトコルを認識し、認証を続行します。

    -   クライアントコンピューターが、一覧に示されているプロトコルのいずれかをサポートしていない場合、認証の交換は失敗します。

## <a name="see-also"></a>参照
[Windows 認証のアーキテクチャ](https://technet.microsoft.com/library/dn169024(v=ws.10).aspx)


