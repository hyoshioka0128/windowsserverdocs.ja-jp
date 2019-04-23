---
title: セキュリティ サポート プロバイダー インターフェイスのアーキテクチャ
description: Windows Server のセキュリティ
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-windows-auth
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: de09e099-5711-48f8-adbd-e7b8093a0336
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 8b0a74089c5d8a88a380f8a56e3b9e03b84081c1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827023"
---
# <a name="security-support-provider-interface-architecture"></a>セキュリティ サポート プロバイダー インターフェイスのアーキテクチャ

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

IT プロフェッショナル向けのこのリファレンス トピックでは、セキュリティ サポート プロバイダー インターフェイス (SSPI) アーキテクチャ内で使用される Windows 認証プロトコルについて説明します。

Microsoft セキュリティ サポート プロバイダー インターフェイス (SSPI) は、Windows 認証の基盤です。 アプリケーションと認証が必要なインフラストラクチャ サービスを提供するのに SSPI を使用します。

SSPI は、実装の Generic Security Service API (GSSAPI) Windows Server オペレーティング システムでです。 GSSAPI の詳細については、RFC 2743 と、IETF RFC データベースでの RFC 2744 を参照してください。

Windows での特定の認証プロトコルを呼び出す既定のセキュリティ サポート プロバイダー (Ssp) は、Dll として、SSPI に組み込まれます。 これらの既定の Ssp は、次のセクションで説明します。 SSPI で操作できるようにする場合、Ssp の追加を組み込むことができます。

次の図に示すように Windows で SSPI は、クライアント コンピューターとサーバー間の既存の通信チャネル経由で認証トークンを実行するメカニズムを提供します。 2 つのコンピューターまたはデバイス認証を安全に通信できるようにする必要がある、ときに、認証の要求は、SSPI では、現在使用されているネットワーク プロトコルに関係なく、認証プロセスを完了にルーティングされます。 SSPI では、透過的なバイナリ ラージ オブジェクトを返します。 この時点で SSPI 層に渡すことが、アプリケーション間で渡されます。 したがって、SSPI では、セキュリティ システムへのインターフェイスを変更することがなく、コンピューターまたはネットワークで利用可能な各種のセキュリティ モデルを使用するアプリケーションができます。

![セキュリティ サポート プロバイダー インターフェイスのアーキテクチャを示す図](../media/security-support-provider-interface-architecture/AuthN_SecuritySupportProviderInterfaceArchitecture.jpg)

次のセクションには、SSPI と対話する既定 Ssp がについて説明します。 Ssp は、セキュリティで保護された通信をセキュリティ保護されていないネットワーク環境での昇格に Windows オペレーティング システムのさまざまな方法で使用されます。

-   [Kerberos セキュリティ サポート プロバイダー](#BKMK_KerbSSP)

-   [NTLM セキュリティ サポート プロバイダー](#BKMK_NTLMSSP)

-   [ダイジェスト セキュリティ サポート プロバイダー](#BKMK_DigestSSP)

-   [Schannel セキュリティ サポート プロバイダー](#BKMK_SchannelSSP)

-   [セキュリティ サポート プロバイダーにネゴシエートします。](#BKMK_NegoSSP)

-   [Credential Security Support Provider](#BKMK_CredSSP)

-   [セキュリティ サポート プロバイダーの拡張機能をネゴシエーションします。](#BKMK_NegoExtsSSP)

-   [PKU2U セキュリティ サポート プロバイダー](#BKMK_PKU2USSP)

このトピックの「も含まれていますいます。

[セキュリティ サポート プロバイダーの選択](security-support-provider-interface-architecture.md#BKMK_SecuritySupportProviderSelection)

### <a name="BKMK_KerbSSP"></a>Kerberos セキュリティ サポート プロバイダー
Microsoft によって実装される、この SSP は、Kerberos version 5 プロトコルのみを使用します。 このプロトコルは、ネットワーク ワーキング グループの RFC 4120 とドラフトのリビジョンに基づきます。 対話型のログオン パスワードまたはスマート カードで使用される業界標準プロトコルになります。 Windows でのサービスの推奨される認証方法もです。

すべてのドメイン サービスが Kerberos SSP をサポートする Kerberos プロトコルは、Windows 2000 以降、既定の認証プロトコルをされている、ため これらのサービスには、次のようなものがあります。

-   ライトウェイト ディレクトリ アクセス プロトコル (LDAP) を使用する active Directory クエリ

-   リモート プロシージャ コール サービスを使用してリモート サーバーまたはワークステーションの管理

-   印刷サービス

-   クライアント/サーバー認証

-   (Common Internet File System または CIFS とも呼ばれます) は、サーバー メッセージ ブロック (SMB) プロトコルを使用してリモート ファイル アクセス

-   分散ファイル システムの管理と参照

-   イントラネットにインターネット インフォメーション サービス (IIS) の認証

-   インターネット プロトコル セキュリティ (IPsec) セキュリティ機関の認証

-   証明書の要求のドメイン ユーザーとコンピューターの Active Directory 証明書サービス

場所: %windir%\Windows\System32\kerberos.dll

既定で指定されているバージョンでこのプロバイダーが含まれる、**に適用されます**このトピックでは、および Windows Server 2003 および Windows XP の先頭に一覧します。

**Kerberos プロトコルと Kerberos SSP の他のリソース**

-   [Microsoft Kerberos (Windows)](https://msdn.microsoft.com/library/aa378747(VS.85).aspx)

-   [\[MS KILE\]:Kerberos プロトコル拡張機能](https://msdn.microsoft.com/library/cc233855(PROT.10).aspx)

-   [\[MS-SFU\]:Kerberos プロトコル拡張:Service for User および制約付き委任プロトコルの仕様](https://msdn.microsoft.com/library/cc246071(PROT.13).aspx)

-   [Kerberos SSP/AP (Windows)](https://msdn.microsoft.com/library/aa377942(VS.85).aspx)

-   [Kerberos の強化](https://technet.microsoft.com/library/cc749438(v=ws.10).aspx)Windows vista の場合

-   [Kerberos 認証の変更点](https://technet.microsoft.com/library/dd560670(v=ws.10).aspx)Windows 7 の 

-   [Kerberos 認証のテクニカル リファレンス](https://technet.microsoft.com/library/cc739058(v=ws.10).aspx)

### <a name="BKMK_NTLMSSP"></a>NTLM セキュリティ サポート プロバイダー
NTLM のセキュリティ サポート プロバイダー (NTLM SSP) は、NTLM チャレンジ/レスポンス認証を許可して、整合性と機密性のオプションをネゴシエートするセキュリティ サポート プロバイダー インターフェイス (SSPI) でを使用するプロトコルをメッセージング バイナリです。 SSPI 認証を使用すると、サーバー メッセージ ブロックまたは CIFS 認証、HTTP ネゴシエート認証 (インターネット Web 認証など) およびリモート プロシージャ コール サービスを含む任意の場所、NTLM が使用されます。 NTLM SSP には、NTLM、NTLM version 2 (NTLMv2) が含まれます。 認証プロトコルです。

サポートされている Windows オペレーティング システムでは、次のような NTLM SSP を使用できます。

-   クライアント/サーバー認証

-   印刷サービス

-   CIFS (SMB) を使用してファイルへのアクセス

-   セキュリティで保護されたリモート プロシージャ コール サービスまたは DCOM サービス

Location: %windir%\Windows\System32\msv1_0.dll

既定で指定されているバージョンでこのプロバイダーが含まれる、**に適用されます**このトピックでは、および Windows Server 2003 および Windows XP の先頭に一覧します。

**NTLM プロトコルと NTLM SSP の他のリソース**

-   [MSV1_0 認証パッケージ (Windows)](https://msdn.microsoft.com/library/aa378753(VS.85).aspx)

-   [NTLM 認証の変更点](https://technet.microsoft.com/library/dd566199(v=ws.10).aspx)で Windows 7 

-   [Microsoft NTLM (Windows)](https://msdn.microsoft.com/library/aa378749(VS.85).aspx)

-   [監査と NTLM の使用に関するガイドを制限します。](https://technet.microsoft.com/library/jj865674(v=ws.10).aspx)

### <a name="BKMK_DigestSSP"></a>ダイジェスト セキュリティ サポート プロバイダー
ダイジェスト認証は、ライトウェイト ディレクトリ アクセス プロトコル (LDAP) と web の認証に使用される業界標準です。 ダイジェスト認証では、MD5 ハッシュまたはメッセージ ダイジェストとして、ネットワーク経由で資格情報を送信します。

次のようなダイジェスト SSP (Wdigest.dll) が使用されます。

-   Internet Explorer およびインターネット インフォメーション サービス (IIS) のアクセス

-   LDAP クエリ

Location: %windir%\Windows\System32\Digest.dll

既定で指定されているバージョンでこのプロバイダーが含まれる、**に適用されます**このトピックでは、および Windows Server 2003 および Windows XP の先頭に一覧します。

**ダイジェスト プロトコルとダイジェスト SSP の他のリソース**

-   [Microsoft ダイジェスト認証 (Windows)](https://msdn.microsoft.com/library/aa378745(VS.85).aspx)

-   [\[MS DPSP\]:ダイジェスト プロトコルの拡張機能](https://msdn.microsoft.com/library/cc227906(PROT.13).aspx)

### <a name="BKMK_SchannelSSP"></a>Schannel セキュリティ サポート プロバイダー
セキュリティで保護されたチャネル (Schannel) は、ユーザーがセキュリティで保護された web サーバーにアクセスしようとしたときなど、web ベースのサーバー認証に使用されます。

TLS プロトコル、SSL プロトコル、Private Communications テクノロジ (PCT) プロトコル、および、データグラム トランスポート層 (DTLS) プロトコルは、公開キーの暗号化に基づいています。 Schannel は、これらすべてのプロトコルを提供します。 どの Schannel プロトコルでも、クライアント/サーバー モデルが使用されています。 Schannel SSP では、公開キー証明書を使用して利用者を認証します。 パーティを認証するときに、Schannel SSP は、基本設定の次の順序でプロトコルを選択します。

-   トランスポート層セキュリティ (TLS) version 1.0

-   トランスポート層セキュリティ (TLS) version 1.1

-   トランスポート層セキュリティ (TLS) version 1.2

-   Secure Socket Layer (SSL) version 2.0

-   Secure Socket Layer (SSL) 3.0

-   プライベート通信テクノロジ (PCT)

    **注**PCT が既定で無効になっています。

選択されているプロトコルは、クライアントとサーバーがサポートできる推奨される認証プロトコルです。 たとえば、サーバーでは、すべての Schannel プロトコルであり、SSL 3.0 と SSL 2.0 のみクライアントがサポートする場合、認証プロセスは SSL 3.0 を使用します。

DTLS は、アプリケーションによって明示的に呼び出されたときに使用されます。 DTLS と、Schannel プロバイダーで使用されるその他のプロトコルの詳細については、次を参照してください。 [Schannel セキュリティ サポート プロバイダーのテクニカル リファレンス](../tls/schannel-security-support-provider-technical-reference.md)します。

場所: %windir%\Windows\System32\Schannel.dll

既定で指定されているバージョンでこのプロバイダーが含まれる、**に適用されます**このトピックでは、および Windows Server 2003 および Windows XP の先頭に一覧します。

> [!NOTE]
> TLS 1.2 は、このプロバイダーでは、Windows Server 2008 R2 および Windows 7 で導入されました。 DTLS は、このプロバイダーでは、Windows Server 2012 および Windows 8 で導入されました。

**TLS と SSL プロトコルと、Schannel SSP の他のリソース**

-   [セキュリティで保護されたチャネル (Windows)](https://msdn.microsoft.com/library/aa380123(VS.85).aspx)

-   [TLS/SSL のテクニカル リファレンス](https://technet.microsoft.com/library/cc784149(v=ws.10).aspx)

-   [\[MS TLSP\]:トランスポート層セキュリティ (TLS) のプロファイル](https://msdn.microsoft.com/library/dd207968(PROT.13).aspx)

### <a name="BKMK_NegoSSP"></a>セキュリティ サポート プロバイダーにネゴシエートします。
Simple and Protected GSS-API Negotiation Mechanism (SPNEGO)、ネゴシエート SSP の基礎を形成という特定の認証プロトコルをネゴシエートするために使用します。 アプリケーションがネットワークにログオンする sspi を呼び出すときに、要求を処理する SSP を指定できます。 アプリケーションでは、ネゴシエート SSP を指定する場合は要求を分析し、顧客が構成したセキュリティ ポリシーに基づいて、要求を処理するために、適切なプロバイダーを取得します。

SPNEGO は、rfc2478 で指定されます。

Windows オペレーティング システムのサポートされているバージョンでは、セキュリティのネゴシエートは、プロバイダーを選択し、Kerberos プロトコルと NTLM をサポートします。 選択をネゴシエート、Kerberos は、認証に関連するシステムのいずれかによって、そのプロトコルを使用できないか、呼び出し元のアプリケーションは、Kerberos プロトコルを使用するための十分な情報を提供できなかった場合を除き、既定ではプロトコルします。

Location: %windir%\Windows\System32\lsasrv.dll

既定で指定されているバージョンでこのプロバイダーが含まれる、**に適用されます**このトピックでは、および Windows Server 2003 および Windows XP の先頭に一覧します。

**ネゴシエート SSP の他のリソース**

-   [Microsoft ネゴシエート (Windows)](https://msdn.microsoft.com/library/aa378748(VS.85).aspx)

-   [\[MS SPNG\]:シンプルで保護された GSS-API ネゴシエーション機構 (SPNEGO) 拡張機能](https://msdn.microsoft.com/library/cc247021(PROT.13).aspx)

-   [\[MS N2HT\]:ネゴシエート、Nego2 HTTP 認証プロトコルの仕様](https://msdn.microsoft.com/library/dd303576(PROT.13).aspx)

### <a name="BKMK_CredSSP"></a>Credential Security Support Provider
新しいターミナル サービスとリモート デスクトップ サービス セッションを開始するときに、Credential Security Service Provider (CredSSP) は、シングル サインオン (SSO) ユーザー エクスペリエンスを提供します。 CredSSP は、クライアントのポリシーに基づく (を通じてサーバー側 SSP) で、ターゲット サーバーに (クライアント側の SSP を使用) して、クライアント コンピューターからユーザーの資格情報を委任するアプリケーションを使用できます。 CredSSP ポリシーのグループ ポリシーを使用して構成し、資格情報の委任が既定でオフにします。

Location: %windir%\Windows\System32\credssp.dll

既定で指定されているバージョンでこのプロバイダーが含まれる、**に適用されます**このトピックの冒頭にある一覧。

**資格情報の SSP の他のリソース**

-   [\[MS CSSP\]:資格情報のセキュリティ サポート プロバイダー (CredSSP) プロトコルの仕様](https://msdn.microsoft.com/library/cc226764(PROT.13).aspx)

-   [資格情報セキュリティ サービス プロバイダーと SSO のターミナル サービスのログオン](https://technet.microsoft.com/library/cc749211(v=ws.10).aspx)

### <a name="BKMK_NegoExtsSSP"></a>セキュリティ サポート プロバイダーの拡張機能をネゴシエーションします。
拡張機能のネゴシエーション (NegoExts) はネゴシエート Ssp は、NTLM または Kerberos プロトコル以外を使用する認証パッケージおよびシナリオをアプリケーションによって実装される Microsoft およびその他のソフトウェア企業。

この拡張機能をネゴシエート パッケージには、次のシナリオを許可します。

-   **フェデレーション システム内でのリッチ クライアントの可用性** SharePoint サイトでドキュメントにアクセスでき、それらはすべての機能を備えた Microsoft Office アプリケーションを使用して編集できます。

-   **Microsoft Office サービスのリッチ クライアントをサポートします。** ユーザーは、Microsoft Office のサービスにサインインし、すべての機能を備えた Microsoft Office アプリケーションを使用できます。

-   **ホストされた Microsoft Exchange サーバー、および Outlook です。** Exchange Server が、web でホストされているため、確立されているドメインの信頼関係はありません。 Outlook では、Windows Live サービスを使用して、ユーザーを認証します。

-   **クライアント コンピューターとサーバー間のリッチ クライアントの可用性** オペレーティング システムのネットワークと認証のコンポーネントが使用されます。

Windows ネゴシエート パッケージでは、Kerberos と NTLM の場合と同様に、同じ方法で NegoExts SSP を扱います。 NegoExts.dll が起動時にローカル システム機関 (LSA) に読み込まれます。 認証要求を受信すると、要求のソースに基づく NegoExts はサポートされている Ssp の間でネゴシエートします。 資格情報と、ポリシー、暗号化情報を送信するセキュリティ トークンが作成されている、適切な SSP を収集します。

NegoExts でサポートされている Ssp は、Kerberos、NTLM などのスタンドアロンの Ssp ではありません。 そのため、NegoExts SSP 内認証メソッドが何らかの理由で失敗したときに認証失敗メッセージを表示またはログに記録します。 認証方法を再交渉またはフォールバックすることはできません。

場所: %windir%\Windows\System32\negoexts.dll

既定で指定されているバージョンでこのプロバイダーが含まれる、**に適用されます**Windows Server 2008 および Windows Vista を除く、このトピックの冒頭にある一覧。

### <a name="BKMK_PKU2USSP"></a>PKU2U セキュリティ サポート プロバイダー
PKU2U プロトコルが導入され、Windows 7 および Windows Server 2008 R2 で、SSP として実装されています。 この SSP では、メディアおよび Windows 7 で導入された、ホーム グループと呼ばれる機能を共有するファイルを特にのピア ツー ピア認証を有効します。 この機能は、ドメインのメンバーではないコンピューター間で共有を許可します。

場所: %windir%\Windows\System32\pku2u.dll

既定で指定されているバージョンでこのプロバイダーが含まれる、**に適用されます**Windows Server 2008 および Windows Vista を除く、このトピックの冒頭にある一覧。

**PKU2U プロトコルと PKU2U SSP の他のリソース**

-   [オンライン Id の統合の概要](https://technet.microsoft.com/library/dd560662(v=ws.10).aspx)

## <a name="BKMK_SecuritySupportProviderSelection"></a>セキュリティ サポート プロバイダーの選択
Windows SSPI は、インストールされているセキュリティ サポート プロバイダーによってサポートされるプロトコルのいずれかを使用できます。 ただし、すべてのオペレーティング システムとして Windows Server を実行して、特定のコンピューターの同じ SSP パッケージをサポートするためクライアントとサーバーの両方がサポートするプロトコルを使用するネゴシエートする必要があります。 Windows Server は、クライアント コンピューターと可能ですが、オペレーティング システムがクライアント コンピューターとクライアントの Kerberos をサポートしていないアプリケーションを許可するのには、Kerberos プロトコル、厳密な標準ベース プロトコルを使用するアプリケーションが優先されます。認証プロトコルです。

認証は、2 つの場所との通信を行う前に、のコンピューターは、プロトコルに合意する必要があります、両方をサポートできること。 各コンピューターの任意のプロトコル、SSPI を使用するのには、適切な SSP をいる必要があります。 たとえば、クライアント コンピューターとサーバーが Kerberos 認証プロトコルを使用するには、サポートする必要両方 Kerberos v5 します。 Windows Server は、関数を使用して**EnumerateSecurityPackages**これら Ssp の機能は、コンピューターと何ではサポートされている Ssp を識別するためにします。

認証プロトコルの選択は、次の 2 つの方法のいずれかで処理できます。

1.  [1 つの認証プロトコル](#BKMK_SingleAuth)

2.  [Negotiate オプション](#BKMK_Negotiate)

### <a name="BKMK_SingleAuth"></a>1 つの認証プロトコル
1 つの許容可能なプロトコルを指定するには、サーバーで、指定したプロトコルまたは通信が失敗したクライアント コンピューターをサポートする必要があります。 1 つの許容可能なプロトコルを指定すると、認証の交換が行われて、次のように。

1.  クライアント コンピューターでは、サービスへのアクセスを要求します。

2.  サーバーは、要求に応答し、使用されるプロトコルを指定します。

3.  クライアント コンピューターでは、指定されたプロトコルがサポートするかどうかを確認するためのチェック、応答の内容を調べます。 かどうか、クライアント コンピューターは、指定されたプロトコルをサポートして、認証が続行されます。 クライアント コンピューターが、プロトコルをサポートしていない場合、認証が失敗した、リソースにアクセスするクライアント コンピューターが承認されているかどうかに関係なく。

### <a name="BKMK_Negotiate"></a>Negotiate オプション
しようと、許容可能なプロトコルを検索するには、クライアントとサーバーを許可するのには、negotiate オプションを使用できます。 これについては、Simple and Protected GSS-API Negotiation Mechanism (SPNEGO) に基づきます。 認証プロトコルをネゴシエートするオプションを使用して、認証が開始されると、SPNEGO 交換が行われて、次のように。

1.  クライアント コンピューターでは、サービスへのアクセスを要求します。

2.  サーバーは、サポートできる認証プロトコルと認証チャレンジまたはその最初の選択肢であるプロトコルに基づいて、応答の一覧で応答します。 たとえば、サーバーは、Kerberos プロトコルと NTLM、ボックスの一覧し、Kerberos 認証の応答を送信します。

3.  クライアント コンピューターは、指定したプロトコルのいずれかをサポートするかどうかを判断するためのチェック、応答の内容を調べます。

    -   クライアント コンピューターでは、優先プロトコルをサポートする場合は、認証が行われます。

    -   場合は、クライアント コンピューターは、優先プロトコルをサポートしていませんが、サーバーが表示されているその他のプロトコルのいずれかをサポートして、クライアント コンピューターには、サーバーのバージョンの確認がサポートする認証プロトコルと認証が続行されますことができます。

    -   クライアント コンピューターが一覧表示されているプロトコルのいずれかにもできません認証は失敗します。

## <a name="see-also"></a>関連項目
[Windows 認証のアーキテクチャ](https://technet.microsoft.com/library/dn169024(v=ws.10).aspx)


