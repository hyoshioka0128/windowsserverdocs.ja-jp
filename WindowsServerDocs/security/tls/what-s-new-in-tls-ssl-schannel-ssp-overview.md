---
title: "TLS、SSL (Schannel SSP) の概要"
description: "Windows Server のセキュリティ"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-tls-ssl
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c8836345-16bb-4dcc-8d2b-2b9b687456a3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: b846ed54a1f7c8ef7a85ea9f836ffa75d0036ae6
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="overview-of-tls---ssl-schannel-ssp"></a>TLS、SSL (Schannel SSP) の概要

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

IT プロフェッショナル向けのこのトピックでは機能で、Schannel セキュリティ サポート プロバイダー (SSP)、Windows Server 2012 R2、Windows Server 2012、Windows 8.1、および Windows 8 のトランスポート層セキュリティ (TLS)、Secure Sockets Layer (SSL)、データグラム トランスポート層セキュリティ (DTLS) 認証プロトコルを含むの変更について説明します。

Schannel は、SSL、TLS および DTLS インターネット標準の認証プロトコルを実装するセキュリティ サポート プロバイダー (SSP) です。 セキュリティ サポート プロバイダー インターフェイス (SSPI) は、認証など、セキュリティ関連の機能を実行する Windows システムで使用される API です。 SSPI は、Schannel SSP を含むいくつかのセキュリティ サポート プロバイダー (Ssp) を共通のインターフェイスとして機能します。

For more information about Microsoft's implementation of TLS and SSL in the Schannel SSP, see the [TLS/SSL Technical Reference (2003)](https://technet.microsoft.com/library/cc784149(v=ws.10).aspx).


##<a name="tlsssl-schannel-ssp-features"></a>TLS/SSL (Schannel SSP) の機能
Schannel ssp の TLS の機能を次に示します

### <a name="tls-session-resumption"></a>TLS セッションの再開
トランスポート層セキュリティ (TLS) プロトコルを Schannel セキュリティ サポート プロバイダーのコンポーネントは、アプリケーション間で信頼できないネットワークを経由で送信されるデータの保護に使用されます。 TLS と SSL は、サーバーと、クライアント コンピューターを認証して、認証された当事者間のメッセージの暗号化にも使用できます。

頻繁に TLS をサーバーに接続するデバイスは、セッションの有効期限のために再接続する必要があります。 Windows 8.1 および Windows Server 2012 R2 は、RFC 5077 (サーバー側の状態なし TLS セッションの再開) をサポートできるようになりました。 この変更は、Windows Phone および Windows RT デバイスを提供します。

-   サーバー上の削減リソース使用率

-   クライアント接続の効率を向上させ、帯域幅の制限

-   接続の再開のための TLS ハンドシェイクに費やされた時間を短縮します。

> [!NOTE]
> RFC 5077 のクライアント側の実装は、Windows 8 で追加されました。

ステートレスな TLS セッションの再開の詳細については、IETF のドキュメントを参照してください。[RFC 5077 します。](http://www.ietf.org/rfc/rfc5077)

### <a name="application-protocol-negotiation"></a>アプリケーション プロトコルのネゴシエーション
 Windows Server 2012 R2 および Windows 8.1 サポート クライアント側の TLS アプリケーション プロトコルのネゴシエーションのためアプリケーションは、HTTP 2.0 標準開発の一部としてプロトコルを利用し、ユーザーが Google、Twitter などのオンライン サービスにアクセスできます SPDY プロトコルを実行しているアプリを使用します。

**そのしくみ**

クライアントとサーバーのアプリケーションは、優先順位の降順でサポートされているアプリケーション プロトコル ID のリストを提供することによって、アプリケーション プロトコルのネゴシエーション拡張を有効にします。 TLS クライアントは、ClientHello メッセージにクライアントでサポートされるプロトコルの一覧にアプリケーション レイヤー プロトコル ネゴシエーション (ALPN) 拡張機能を含めることによって、アプリケーション プロトコルのネゴシエーションをサポートしていることを示します。

TLS クライアントがサーバーに要求するとき、TLS サーバーはサポートされているプロトコルも、クライアントがサポートする最も優先されるアプリケーション プロトコルの一覧を読み取ります。 このようなプロトコルが見つかった場合、サーバーは、選択したプロトコルの ID を持つ応答し、通常どおりにハンドシェイクを続行します。 共通のアプリケーション プロトコルがない場合は、サーバーは、致命的なハンドシェイク エラー アラートを送信します。

### <a name="BKMK_TrustedIssuers"></a>クライアント認証用の信頼された発行者の管理
クライアント コンピューターの認証が SSL または TLS を使用して必要な場合は、信頼された証明書の発行者の一覧を送信するサーバーを構成できます。 この一覧は、サーバーが信頼する証明書発行者のセットが含まれていて、複数の証明書がある場合はオンにするクライアント証明書か、クライアント コンピューターへのヒントします。 さらに、構成済みの信頼された発行者の一覧に対して、クライアント コンピューターをサーバーに送信する証明書チェーンを検証する必要があります。

Windows Server 2012 および Windows 8 では、前に、Schannel SSP (HTTP.sys と IIS を含む) を使用するアプリケーションやプロセスは、クライアント認証証明書信頼リスト (CTL) を介してサポートしている信頼された発行者の一覧を提供できます。

Windows Server 2012 と Windows 8 での変更点を基になる認証プロセスにできるようにします。

-   CTL ベースの信頼された発行者の一覧の管理がサポートされていません。

-   既定で信頼された発行者の一覧を送信する動作は無効になって: SendTrustedIssuerList レジストリ キーの既定値は 0 (既定でオフ) 1 ではなく。

-   Windows オペレーティング システムの以前のバージョンに互換性は維持されます。

**どのような値はこの追加しますか。**

Windows Server 2012 以降では、CTL の使用は、証明書ストア ベースの実装で置き換えられましたがします。 これにより、certutil.exe などのコマンド ライン ツールと共に、PowerShell プロバイダーの既存の証明書管理コマンドレットを通じて他の一般的な管理がしやすくします。

Schannel SSP (16 KB) をサポートしている信頼された証明機関の一覧の最大サイズは変わりませんが、Windows Server 2012 での Windows Server 2008 R2 と同様が関連のない証明書が、メッセージに含まれないようにクライアント認証の発行者の新しい専用の証明書を格納します。

**そのしくみですか。**

Windows Server 2012 で、信頼された発行者の一覧が構成されている証明書ストアを使用します。1 つの既定のグローバル コンピューターの証明書ストア、もう 1 つはサイトごとにオプションにします。 一覧のソースは次のように決定されます。

-   ソースとして使用する場合は、サイト用に構成された特定の資格情報ストアが、

-   アプリケーションで定義されたストアに証明書が存在しないかどうかは、Schannel のチェック、**クライアント認証の発行者**、ローカル コンピューター上に保存し、証明書が存在する場合は、ソースとしてそのストアを使用します。 どちらのストアに証明書が見つからない場合は、信頼されたルート ストアがチェックされます。

-   グローバルまたはローカルのどちらのストアに証明書が含まれている場合、Schannel プロバイダーは使用、**信頼されたルート証明書機関**信頼された発行者の一覧のソースとして保存します。 (これは、Windows Server 2008 R2 の動作です)。

場合、**信頼されたルート証明書機関**使用されたストアにルート (自己署名) と証明機関 (CA) 発行元の証明書の両方が含まれています、CA 発行者証明書は、既定では、サーバーに送信されます。

**信頼された発行者の証明書ストアを使用する Schannel を構成する方法**

Windows Server 2012 での Schannel SSP のアーキテクチャは既定でストアを使用して上記のよう、信頼された発行者の一覧を管理します。 証明書を管理、PowerShell プロバイダーと Certutil などのコマンド ライン ツールの既存の証明書管理コマンドレットを使用することができます。

For information about managing certificates using the PowerShell provider, see [AD CS Administration Cmdlets in Windows](https://technet.microsoft.com/library/hh848365(v=wps.620).aspx).

For information about managing certificates using the certificate utility, see [certutil.exe](https://technet.microsoft.com/library/cc732443.aspx).

For information about what data, including the application-defined store, is defined for an Schannel credential, see [SCHANNEL_CRED structure (Windows)](https://msdn.microsoft.com/library/windows/desktop/aa379810(v=vs.85).aspx).

**信頼モードの既定の設定**

これは、次の 3 つのクライアント認証信頼モード、Schannel プロバイダーでサポートされています。 The trust mode controls how validation of the client's certificate chain is performed and is a system-wide setting controlled by the REG_DWORD "ClientAuthTrustMode" under HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\Schannel.

|値|信頼モード|説明|
|-----|-------|--------|
|0|コンピューター信頼 (既定)|クライアント証明書が信頼された発行者の一覧で証明書によって発行されたことが必要です。|
|1|排他的ルート信頼|あるクライアント証明書を呼び出し元によって指定の信頼された発行者ストアに含まれているルート証明書にチェーンする必要があります。 証明書は、信頼された発行者の一覧で、発行者によっても発行する必要があります。|
|2|排他的 CA 信頼|中間 CA 証明書またはルート証明書に、呼び出し元が指定したクライアント証明書チェーンの信頼された発行者ストアいる必要があります。|

For information about authentication failures due to trusted issuers configuration issues, see Knowledge Base article [280256](https://support.microsoft.com/kb/2802568).

### <a name="BKMK_SNI"></a>TLS が Server Name Indicator (SNI) 拡張機能のサポートします。
Server Name Indication 機能は、多数の仮想イメージを 1 台のサーバーで実行しているときに、サーバーの適切な ID を許可するように TLS と SSL プロトコルを拡張します。 正しく保護するには、クライアント コンピューターとサーバー間の通信は、クライアント コンピューターは、サーバーからデジタル証明書を要求します。 サーバー証明書を送信要求に応答して後、クライアント コンピューターがチェック、通信を暗号化するために使用およびの通常の要求と応答 exchange を実行します。 ただし、仮想ホスティング シナリオでは、いくつかのドメインが異なる可能性がある証明書がそれぞれは 1 つのサーバーでホストされます。 この場合、サーバーには、クライアント コンピューターに送信する証明書をあらかじめ知る方法がありません。 SNI により、クライアント コンピューターは、ターゲット ドメインをプロトコル内で事前に通知して、これにより、サーバーを正しく適切な証明書を選択します。

**どのような値はこの追加しますか。**

この追加機能。

-   単一の IP とポートの組み合わせでの複数の SSL Web サイトをホストすることができます。

-   複数の SSL Web サイトが 1 つの Web サーバーでホストされている場合は、メモリ使用量を削減します。

-   [SSL Web サイトに同時に接続できるユーザーします。

-   クライアントの認証プロセス中に正しい証明書を選択するためコンピューター インターフェイス上でエンド ユーザーにヒントを出すことができます。

**そのしくみ**

Schannel SSP では、クライアントに許可した接続状態のメモリ内キャッシュを保持します。 これにより、クライアント コンピューターにアクセスする際に、フル SSL ハンドシェイク適用なし、SSL サーバーにすばやく再接続できます。  以前のオペレーティング システム バージョンと比較して 1 つの Windows Server 2012 でホストされるように多くのサイトではこの証明書の管理を効率的に使用できます。

どれを選ぶためのヒントをエンド ユーザーに提供する可能性の証明書の発行者名のリストを構築することにより、エンド ユーザーが証明書の選択が強化されました。 この一覧は、グループ ポリシーを使用して構成可能です。

### <a name="BKMK_DTLS"></a>データグラム トランスポート層セキュリティ (DTLS)
Schannel セキュリティ サポート プロバイダーに、DTLS バージョン 1.0 プロトコルが追加されました。 DTLS プロトコルは、データグラム プロトコルの通信プライバシーを提供します。 このプロトコルは、クライアント/サーバーにより、盗聴、改ざん、メッセージ偽造などを防ぐように設計された方法で通信するためにアプリケーションをできます。 DTLS プロトコルは、トランスポート層セキュリティ (TLS) プロトコルに基づいており、IPsec を使用する必要が少なく、カスタム アプリケーション層のセキュリティ プロトコルを設計または同等のセキュリティ保証を提供します。

**どのような値はこの追加しますか。**

データグラムは、ゲームまたはセキュリティで保護されたビデオ会議などのメディアをストリーミングで共通です。 Schannel プロバイダーに DTLS プロトコルを追加すると、クライアント コンピューターとサーバー間の通信をセキュリティ保護に使い慣れた Windows SSPI モデルを使用する機能を提供します。 DTLS は意図的にセキュリティの発明を最小限にし、コードとインフラストラクチャの再利用の量を最大化する、可能な限り TLS にするよう設計されています。

**そのしくみ**

UDP 経由で DTLS を使用するアプリケーションでは、Windows Server 2012 および Windows 8 で SSPI モデルを使用できます。 特定の暗号スイートは構成では、TLS の構成方法に似ています。 Schannel で引き続き、FIPS 140 認定は、Windows Vista で導入された機能を活用する CNG 暗号化プロバイダーを使用します。

### <a name="BKMK_Deprecated"></a>推奨されなくなった機能
Windows Server 2012 および Windows 8 用の Schannel SSP ではありません機能または推奨されなくなった機能です。

## <a name="see-also"></a>参照してください。
-   [プライベート クラウド セキュリティ モデル: ラッパー機能](https://social.technet.microsoft.com/wiki/contents/articles/6756.private-cloud-security-model-wrapper-functionality.aspx)



