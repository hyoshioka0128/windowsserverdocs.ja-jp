---
title: "セキュリティ サポート プロバイダー インターフェイスのアーキテクチャ"
description: "Windows Server のセキュリティ"
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
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="security-support-provider-interface-architecture"></a>セキュリティ サポート プロバイダー インターフェイスのアーキテクチャ

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

IT プロフェッショナル向けのこのリファレンス トピックでは、セキュリティ サポート プロバイダー インターフェイス (SSPI) アーキテクチャ内で使用される Windows 認証プロトコルについて説明します。

Microsoft セキュリティ サポート プロバイダー インターフェイス (SSPI) は、Windows 認証の基盤です。 アプリケーションおよびインフラストラクチャ サービスを認証を必要とするは、それを提供するのに SSPI を使用します。

SSPI は、実装の汎用的なセキュリティ Service API (GSSAPI) Windows Server オペレーティング システムです。 GSSAPI の詳細については、RFC 2743 と、IETF RFC データベースでの RFC 2744 を参照してください。

Windows での特定の認証プロトコルを起動する既定のセキュリティ サポート プロバイダー (Ssp) は、Dll として、SSPI に組み込まれます。 これらの既定の Ssp は、次のセクションで説明します。 場合は、SSPI で操作できるように、Ssp の追加を組み込むことができます。

次の図に示すように、Windows の SSPI 認証トークンをクライアント コンピューターとサーバー間の既存の通信チャネル経由で実行するメカニズムを提供します。 2 つのコンピューターまたはデバイスは、認証を安全に通信できるようにする必要があります、ときに、sspi は、現在使用されているネットワーク プロトコルに関係なく、認証プロセスが完了すると認証の要求がルーティングされます。 SSPI は、透明なバイナリ ラージ オブジェクトを返します。 その時点で、SSPI レイヤーに渡すことが、アプリケーション間で渡されます。 したがって、SSPI は、コンピューターまたはネットワーク上のセキュリティ システムにインターフェイスを変更することがなく利用できる各種のセキュリティ モデルを使用するアプリケーションを使用できます。

![セキュリティ サポート プロバイダー インターフェイスのアーキテクチャを示す図](../media/security-support-provider-interface-architecture/AuthN_SecuritySupportProviderInterfaceArchitecture.jpg)

次のセクションでは、SSPI でやり取りする既定 Ssp について説明します。 Ssp は、保護されていないネットワーク環境でセキュリティで保護された通信を昇格に Windows オペレーティング システムでのさまざまな方法で使用されます。

-   [Kerberos セキュリティ サポート プロバイダー](#BKMK_KerbSSP)

-   [NTLM セキュリティ サポート プロバイダー](#BKMK_NTLMSSP)

-   [ダイジェスト セキュリティ サポート プロバイダー](#BKMK_DigestSSP)

-   [Schannel セキュリティ サポート プロバイダー](#BKMK_SchannelSSP)

-   [セキュリティ サポート プロバイダーをネゴシエーションします。](#BKMK_NegoSSP)

-   [Credential Security Support Provider](#BKMK_CredSSP)

-   [セキュリティ サポート プロバイダーの拡張機能をネゴシエートします。](#BKMK_NegoExtsSSP)

-   [PKU2U セキュリティ サポート プロバイダー](#BKMK_PKU2USSP)

このトピックの「も含まれていますいます。

[セキュリティ サポート プロバイダーの選択](security-support-provider-interface-architecture.md#BKMK_SecuritySupportProviderSelection)

### <a name="BKMK_KerbSSP"></a>Kerberos セキュリティ サポート プロバイダー
この SSP は、Microsoft によって実装されるように、Kerberos version 5 プロトコルのみを使用します。 このプロトコルは、Network Working Group の RFC 4120 とドラフトのリビジョンに基づいています。 業界標準のプロトコル、パスワードまたはスマート カードと対話型ログオンに使用することをお勧めします。 Windows のサービスの推奨される認証方法もです。

すべてのドメイン サービスが Kerberos SSP をサポートする、Kerberos プロトコルは、Windows 2000 以降、既定の認証プロトコルをされている、ため これらのサービスは次のとおりです。

-   ライトウェイト ディレクトリ アクセス プロトコル (LDAP) を使用する active Directory クエリ

-   リモート プロシージャ コール サービスを使用してリモート サーバーまたはワークステーションの管理

-   プリント サービス

-   クライアント/サーバー認証

-   リモート ファイル アクセスとも呼ばれる Common Internet File System (CIFS) は、サーバー メッセージ ブロック (SMB) プロトコルを使用します。

-   分散ファイル システムの管理と参照

-   イントラネットの認証には、インターネット インフォメーション サービス (IIS)

-   インターネット プロトコル セキュリティ (IPsec) のセキュリティ権限の認証

-   ドメイン ユーザーとコンピューターに対して Active Directory 証明書サービスに証明書の要求

場所: %windir%\Windows\System32\kerberos.dll

このプロバイダーがで指定されているバージョンでは既定で含まれている、**に適用されます**このトピックでは、Windows Server 2003 と Windows XP の先頭にリストします。

**Kerberos プロトコルと Kerberos SSP の他のリソース**

-   [Microsoft Kerberos (Windows)](https://msdn.microsoft.com/library/aa378747(VS.85).aspx)

-   [\[MS-KILE\]: Kerberos プロトコルの拡張機能](https://msdn.microsoft.com/library/cc233855(PROT.10).aspx)

-   [\[MS-SFU\]: Kerberos プロトコル拡張: Service for User および制約付き委任プロトコルの仕様](https://msdn.microsoft.com/library/cc246071(PROT.13).aspx)

-   [Kerberos SSP/AP (Windows)](https://msdn.microsoft.com/library/aa377942(VS.85).aspx)

-   [Kerberos の強化](https://technet.microsoft.com/library/cc749438(v=ws.10).aspx)Windows vista の場合

-   [Kerberos 認証の変更点](https://technet.microsoft.com/library/dd560670(v=ws.10).aspx)Windows 7 用 

-   [Kerberos 認証のテクニカル リファレンス](https://technet.microsoft.com/library/cc739058(v=ws.10).aspx)

### <a name="BKMK_NTLMSSP"></a>NTLM セキュリティ サポート プロバイダー
NTLM セキュリティ サポート プロバイダー (NTLM SSP) は、メッセージング プロトコルを使用してセキュリティ サポート プロバイダー インターフェイス (SSPI) で NTLM チャレンジ応答認証を許可したり統合と機密のオプションをネゴシエートするバイナリです。 SSPI 認証を使用すると、サーバー メッセージ ブロックまたは CIFS 認証、HTTP のネゴシエート認証 (たとえば、インターネット Web 認証)、およびリモート プロシージャ コール サービスを含む場所には、NTLM が使用されます。 NTLM SSP には、NTLM と NTLM バージョン 2 (NTLMv2) が含まれます。認証プロトコルを実装します。

サポートされている Windows オペレーティング システムでは、次のような NTLM SSP を使用できます。

-   クライアント/サーバー認証

-   プリント サービス

-   CIFS (SMB) を使用してファイルへのアクセス

-   セキュリティで保護されたリモート プロシージャ コール サービスまたは DCOM サービス

場所: %windir%\Windows\System32\msv1_0.dll

このプロバイダーがで指定されているバージョンでは既定で含まれている、**に適用されます**このトピックでは、Windows Server 2003 と Windows XP の先頭にリストします。

**NTLM プロトコルと NTLM SSP の他のリソース**

-   [MSV1_0 認証パッケージ (Windows)](https://msdn.microsoft.com/library/aa378753(VS.85).aspx)

-   [NTLM 認証の変更点](https://technet.microsoft.com/library/dd566199(v=ws.10).aspx)Windows 7 で 

-   [Microsoft NTLM (Windows)](https://msdn.microsoft.com/library/aa378749(VS.85).aspx)

-   [監査と NTLM の使用に関するガイドを制限します。](https://technet.microsoft.com/library/jj865674(v=ws.10).aspx)

### <a name="BKMK_DigestSSP"></a>ダイジェスト セキュリティ サポート プロバイダー
ダイジェスト認証は、ライトウェイト ディレクトリ アクセス プロトコル (LDAP) と Web 認証に使用する業界標準です。 ダイジェスト認証は、MD5 ハッシュまたはメッセージ ダイジェストとして、ネットワーク経由での資格情報を送信します。

次のようなダイジェスト SSP (Wdigest.dll) が使用されます。

-   Internet Explorer およびインターネット インフォメーション サービス (IIS) のアクセス

-   LDAP クエリ

場所: %windir%\Windows\System32\Digest.dll

このプロバイダーがで指定されているバージョンでは既定で含まれている、**に適用されます**このトピックでは、Windows Server 2003 と Windows XP の先頭にリストします。

**ダイジェスト プロトコルとダイジェスト SSP の他のリソース**

-   [Microsoft ダイジェスト認証 (Windows)](https://msdn.microsoft.com/library/aa378745(VS.85).aspx)

-   [\[MS-DPSP\]: ダイジェストのプロトコルの拡張機能](https://msdn.microsoft.com/library/cc227906(PROT.13).aspx)

### <a name="BKMK_SchannelSSP"></a>Schannel セキュリティ サポート プロバイダー
Secure Channel (Schannel) は、ユーザーがセキュリティで保護された Web サーバーにアクセスしようとしたときなど、Web ベースのサーバー認証に使用されます。

TLS プロトコル、SSL プロトコル、Private Communications テクノロジ (PCT) プロトコル、および、データグラム トランスポート層 (DTLS) プロトコルは、公開キーの暗号化に基づいています。 Schannel では、これらすべてのプロトコルを提供します。 すべての Schannel プロトコルでは、クライアント/サーバー モデルを使用します。 Schannel SSP では、公開キー証明書を使用して利用者を認証します。 利用者を認証時に Schannel SSP は、基本設定の次の順序でプロトコルを選択します。

-   トランスポート層セキュリティ (TLS) バージョン 1.0

-   トランスポート層セキュリティ (TLS) バージョン 1.1

-   トランスポート層セキュリティ (TLS) バージョン 1.2

-   Secure Socket Layer (SSL) 2.0

-   Secure Socket Layer (SSL) バージョン 3.0

-   プライベート通信テクノロジ (PCT)

    **注:** PCT は既定で無効になります。

選択されているプロトコルは、クライアントとサーバーをサポートできる望ましい認証プロトコルです。 たとえば、サーバーは、すべての Schannel プロトコルをサポートしているし、クライアントは、SSL 3.0 および SSL 2.0 のみをサポート、認証プロセスは SSL 3.0 を使用します。

DTLS は、アプリケーションによって明示的に呼び出されるときに使用されます。 DTLS と、Schannel プロバイダーで使用されているその他のプロトコルの詳細については、次を参照してください。[Schannel セキュリティ サポート プロバイダーのテクニカル リファレンス](../tls/schannel-security-support-provider-technical-reference.md)します。

場所: %windir%\Windows\System32\Schannel.dll

このプロバイダーがで指定されているバージョンでは既定で含まれている、**に適用されます**このトピックでは、Windows Server 2003 と Windows XP の先頭にリストします。

> [!NOTE]
> TLS 1.2 は、このプロバイダーでは、Windows Server 2008 R2 および Windows 7 で導入されました。 DTLS は、Windows Server 2012 および Windows 8 でプロバイダーにで導入されました。

**TLS と SSL プロトコルと、Schannel SSP の他のリソース**

-   [セキュリティで保護されたチャネル (Windows)](https://msdn.microsoft.com/library/aa380123(VS.85).aspx)

-   [TLS/SSL のテクニカル リファレンス](https://technet.microsoft.com/library/cc784149(v=ws.10).aspx)

-   [\[MS-TLSP\]: トランスポート層セキュリティ (TLS) のプロファイル](https://msdn.microsoft.com/library/dd207968(PROT.13).aspx)

### <a name="BKMK_NegoSSP"></a>セキュリティ サポート プロバイダーをネゴシエーションします。
Simple and Protected GSS-API Negotiation Mechanism (SPNEGO) の基礎とネゴシエート SSP のという、特定の認証プロトコルのネゴシエーションに使用します。 アプリケーションは、ネットワークにログオンする SSPI を呼び出す、SSP が要求を処理することを指定できます。 指定した場合、アプリケーションをネゴシエート SSP、要求を分析し、顧客に構成されたセキュリティ ポリシーに基づいて、要求を処理する適切なプロバイダーを選択します。

SPNEGO は rfc2478 で指定されます。

サポートされているバージョンの Windows オペレーティング システムでは、ネゴシエート セキュリティ サポート プロバイダーを選択し、Kerberos プロトコルと NTLM します。 選択をネゴシエート Kerberos は、認証に関係するシステムのいずれかでそのプロトコルは使用できませんか、呼び出し元アプリケーションが、Kerberos プロトコルを使用するための十分な情報に備わっていない場合を除き、既定でプロトコルです。

場所: %windir%\Windows\System32\lsasrv.dll

このプロバイダーがで指定されているバージョンでは既定で含まれている、**に適用されます**このトピックでは、Windows Server 2003 と Windows XP の先頭にリストします。

**ネゴシエート SSP の他のリソース**

-   [Microsoft ネゴシエート (Windows)](https://msdn.microsoft.com/library/aa378748(VS.85).aspx)

-   [\[MS-SPNG\]: シンプルで保護された GSS-API ネゴシエーション メカニズム (SPNEGO) 拡張機能](https://msdn.microsoft.com/library/cc247021(PROT.13).aspx)

-   [\[MS-N2HT\]: ネゴシエートおよび Nego2 HTTP 認証プロトコルの仕様](https://msdn.microsoft.com/library/dd303576(PROT.13).aspx)

### <a name="BKMK_CredSSP"></a>Credential Security Support Provider
新しいターミナル サービスとリモート デスクトップ サービス セッションを起動するときに、Credential Security Service Provider (CredSSP) は、シングル サインオン (SSO) のユーザー エクスペリエンスを提供します。 CredSSP は、クライアントのポリシーに基づく (を通じてサーバー側 SSP) では、ターゲット サーバーへ (を使用して、クライアント側の SSP) のクライアント コンピューターからユーザーの資格情報を委任アプリケーションできます。 CredSSP ポリシーのグループ ポリシーを使用して構成し、資格情報の委任が既定でオフにします。

場所: %windir%\Windows\System32\credssp.dll

このプロバイダーがで指定されているバージョンでは既定で含まれている、**に適用されます**このトピックの冒頭にリストします。

**資格情報の SSP の他のリソース**

-   [\[MS-CSSP\]: 資格情報のセキュリティ サポート プロバイダー (CredSSP) プロトコルの仕様](https://msdn.microsoft.com/library/cc226764(PROT.13).aspx)

-   [資格情報セキュリティ サービス プロバイダーと SSO のターミナル サービスのログオン](https://technet.microsoft.com/library/cc749211(v=ws.10).aspx)

### <a name="BKMK_NegoExtsSSP"></a>セキュリティ サポート プロバイダーの拡張機能をネゴシエートします。
拡張機能をネゴシエート (NegoExts) がネゴシエート NTLM または Kerberos プロトコル以外の Ssp を使用する認証パッケージ アプリケーションおよびシナリオによって実装される Microsoft およびその他のソフトウェアの企業です。

ネゴシエート パッケージに、この拡張機能は、次のシナリオを許可します。

-   **フェデレーション システム内でのリッチ クライアントの可用性** ドキュメントを SharePoint サイトにアクセスできるし、フル機能を備えた Microsoft Office アプリケーションを使用して、編集することができます。

-   **Microsoft Office のサービスのリッチ クライアントをサポートします。** ユーザーは、Microsoft Office のサービスにログインし、フル機能を備えた Microsoft Office アプリケーションを使用します。

-   **Microsoft のホスト型 Exchange サーバーと Outlook します。** Exchange Server は、Web でホストされるために確立されたドメインの信頼関係はありません。 Outlook では、Windows Live サービスを使用してユーザーを認証します。

-   **クライアント コンピューターとサーバー間でのリッチ クライアントの可用性** オペレーティング システムのネットワークと認証のコンポーネントが使用されます。

Windows ネゴシエート パッケージは、Kerberos と NTLM の場合と同様に、同じ方法で NegoExts SSP を扱います。 NegoExts.dll が起動時にローカル システム機関 (LSA) に読み込まれます。 認証要求を受信すると、要求のソースに基づく NegoExts はサポートされている Ssp 間ネゴシエートします。 資格情報とポリシー、暗号化、およびセキュリティ トークンを作成する場所、適切な SSP にその情報を送信を収集します。

NegoExts でサポートされている Ssp は、Kerberos、NTLM などのスタンドアロンの Ssp ではありません。 そのため、NegoExts SSP 内で何らかの理由での認証方法が失敗した場合、認証エラー メッセージを表示またはログに記録します。 再ネゴシエーションまたは代替の認証方法のことはできません。

場所: %windir%\Windows\System32\negoexts.dll

このプロバイダーがで指定されているバージョンでは既定で含まれている、**に適用されます**Windows Server 2008 および Windows Vista を除く、このトピックの冒頭にリストします。

### <a name="BKMK_PKU2USSP"></a>PKU2U セキュリティ サポート プロバイダー
PKU2U プロトコルが導入され、Windows 7 および Windows Server 2008 R2 で、SSP として実装されます。 この SSP は、ピア ツー ピア認証、特に、メディアおよびファイルが Windows 7 で導入された、ホーム グループと呼ばれる機能を共有できます。 この機能は、ドメインのメンバーではないコンピューター間で共有を許可します。

場所: %windir%\Windows\System32\pku2u.dll

このプロバイダーがで指定されているバージョンでは既定で含まれている、**に適用されます**Windows Server 2008 および Windows Vista を除く、このトピックの冒頭にリストします。

**その他のリソースへの PKU2U プロトコルとへの PKU2U SSP**

-   [オンライン ID 統合の概要](https://technet.microsoft.com/library/dd560662(v=ws.10).aspx)

## <a name="BKMK_SecuritySupportProviderSelection"></a>セキュリティ サポート プロバイダーの選択
Windows SSPI は、インストールされているセキュリティ サポート プロバイダーによってサポートされているプロトコルのいずれかを使用できます。 ただし、サポートため、すべてのオペレーティング システム、同じ SSP パッケージを Windows Server を実行している任意のコンピューターとして、クライアントとサーバーは、両方をサポートするプロトコルを使用するネゴシエートする必要があります。 Windows Server では、クライアント コンピューターおよび許可するようにクライアント コンピューターとクライアントの認証に Kerberos プロトコルをサポートしていないアプリケーションが引き続き可能ですが、オペレーティング システムときに、Kerberos プロトコル、強力な標準ベース プロトコルを使用するアプリケーションが優先されます。

2 つの場所が通信して認証を実行する前にコンピューターはプロトコルに同意する必要があります、両方をサポートできることします。 SSPI を使用するプロトコルのいずれかの各コンピューターの適切な SSP が必要 たとえば、クライアント コンピューターとサーバーが Kerberos 認証プロトコルを使用するが必要があります両方 Kerberos v5 をサポートします。 Windows Server 関数を使用して**EnumerateSecurityPackages**それら Ssp の機能は、どの Ssp は、コンピューターと新機能でサポートを識別します。

認証プロトコルの選択は、次の 2 つの方法のいずれかで処理できます。

1.  [1 つの認証プロトコル](#BKMK_SingleAuth)

2.  [オプションをネゴシエーションします。](#BKMK_Negotiate)

### <a name="BKMK_SingleAuth"></a>1 つの認証プロトコル
サーバーで 1 つの使用可能なプロトコルが指定した場合、指定されたプロトコルまたは通信が失敗した場合、クライアント コンピューターをサポートする必要があります。 1 つの使用可能なプロトコルが指定した場合、認証が行われたとおり。

1.  クライアント コンピューターは、サービスへのアクセスを要求します。

2.  サーバーは、要求に応答し、使用されるプロトコルを指定します。

3.  クライアント コンピューターは、返信と、指定したプロトコルをサポートしているかどうかをチェックの内容を調べます。 かどうか、クライアント コンピューターは、指定したプロトコルをサポートして、認証が続行されます。 クライアント コンピューターが、プロトコルをサポートしていない場合、認証されず、リソースにアクセスするクライアント コンピューターが承認されているかどうかに関係なく。

### <a name="BKMK_Negotiate"></a>オプションをネゴシエーションします。
しようとする、使用可能なプロトコルを見つけるには、クライアントとサーバーを許可するようにネゴシエート オプションを使用できます。 これは、Simple and Protected GSS-API Negotiation Mechanism (SPNEGO) に基づいています。 認証プロトコルのネゴシエーションにオプションで開始されると、認証、SPNEGO が行われたとおり。

1.  クライアント コンピューターは、サービスへのアクセスを要求します。

2.  サーバーは、それをサポートする認証プロトコルと認証チャレンジまたは、最初に選択されているプロトコルに基づいて、応答の一覧で応答します。 たとえば、サーバーは、Kerberos プロトコルと NTLM、ボックスの一覧し、Kerberos 認証の応答を送信します。

3.  クライアント コンピューターでは、返信するかどうかをサポートしている、指定したプロトコルのいずれかのチェックの内容について説明します。

    -   クライアント コンピューターに優先プロトコルをサポートしている場合は、認証が続行されます。

    -   場合は、クライアント コンピューターは、優先プロトコルをサポートしていませんが、サーバーが表示されているその他のプロトコルのいずれかのサポートは、クライアント コンピューターにサーバーに認識をサポートしている認証プロトコルと認証を実行することができます。

    -   クライアント コンピューターはサポートしていない場合、リストされているプロトコルのいずれかの認証は失敗します。

## <a name="see-also"></a>参照してください。
[Windows 認証のアーキテクチャ](https://technet.microsoft.com/library/dn169024(v=ws.10).aspx)


