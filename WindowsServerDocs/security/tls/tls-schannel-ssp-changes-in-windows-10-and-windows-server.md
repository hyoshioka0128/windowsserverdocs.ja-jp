---
title: TLS (Schannel SSP)
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: ebd3c40c-b4c0-4f6d-a00c-f90eda4691df
manager: alanth
author: justinha
ms.technology: security-authentication
ms.date: 11/09/2016
ms.openlocfilehash: 6e1a229bfc7063597f8994c71bbaec5637d084a4
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# <a name="tls-schannel-ssp-changes-in-windows-10-and-windows-server-2016"></a>Windows 10 および Windows Server 2016 での TLS (Schannel SSP) の変更します。

>適用対象: Windows Server 2016 および Windows 10

## <a name="cipher-suite-changes"></a>暗号スイートの変更

Windows 10 バージョン 1511 および Windows Server 2016 は、モバイル デバイス管理 (MDM) を使用して暗号の順位の構成のサポートを追加します。

暗号スイートの優先順位の順序の変更、次を参照してください。[Schannel の暗号スイート](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx)します。

次の暗号スイートのサポートが追加されました。

- TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 (RFC 5289) Windows 10 バージョン 1507 および Windows Server 2016
- TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384 (RFC 5289) Windows 10 バージョン 1507 および Windows Server 2016

暗号スイートでは、次の DisabledByDefault を変更します。

- TLS_DHE_DSS_WITH_AES_256_CBC_SHA256 (RFC 5246) Windows 10 バージョン 1703 では
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA256 (RFC 5246) Windows 10 バージョン 1703 では
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA (RFC 5246) Windows 10 バージョン 1703 では
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA (RFC 5246) Windows 10 バージョン 1703 では
- TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA (RFC 5246) Windows 10 バージョン 1703 では
- Windows 10、バージョン 1709 で TLS_RSA_WITH_RC4_128_SHA
- Windows 10、バージョン 1709 で TLS_RSA_WITH_RC4_128_MD5

Windows 10 バージョン 1507 および Windows Server 2016 以降、sha-512 証明書を既定でサポートします。

### <a name="rsa-key-changes"></a>RSA キーの変更

Windows 10 バージョン 1507 および Windows Server 2016 は、RSA キーのサイズがクライアントのレジストリの構成オプションを追加します。

詳細については、次を参照してください。[KeyExchangeAlgorithm - クライアント RSA キー サイズ](tls-registry-settings.md#keyexchangealgorithm---client-rsa-key-sizes)します。

### <a name="diffie-hellman-key-changes"></a>Diffie-hellman キーの変更

Windows 10 バージョン 1507 および Windows Server 2016 Diffie-hellman キーのサイズのレジストリの構成オプションを追加します。

詳細については、次を参照してください。[KeyExchangeAlgorithm - Diffie-hellman キー サイズ](tls-registry-settings.md#keyexchangealgorithm---diffie-hellman-key-sizes)します。

### <a name="schusestrongcrypto-option-changes"></a>SCH_USE_STRONG_CRYPTO オプションの変更

Windows 10 バージョン 1507 および Windows Server 2016 で[SCH_USE_STRONG_CRYPTO](https://msdn.microsoft.com/library/windows/desktop/aa379810.aspx)オプションを今すぐを無効に null の場合、MD5、DES、および暗号をエクスポートします。

## <a name="elliptical-curve-changes"></a>楕円曲線変更します。

Windows 10 バージョン 1507 および Windows Server 2016 の追加 [コンピューターの構成、楕円曲線のグループ ポリシーの構成 > 管理用テンプレート > ネットワーク > SSL 構成設定。 ECC 曲線順一覧楕円曲線は優先的に使用する順序を指定しますだけでなくにより、サポートされているカーブを有効になっていません。 
 
次の楕円曲線のサポートが追加されました。

- BrainpoolP256r1 (RFC 7027) Windows 10 バージョン 1507 および Windows Server 2016
- BrainpoolP384r1 (RFC 7027) Windows 10 バージョン 1507 および Windows Server 2016 
- BrainpoolP512r1 (RFC 7027) Windows 10 バージョン 1507 および Windows Server 2016
- Curve25519 (RFC ドラフト-ietf-tls-curve25519) で Windows 10 バージョン 1607 および Windows Server 2016

## <a name="dispatch-level-support-for-sealmessage--unsealmessage"></a>SealMessage & UnsealMessage ディスパッチ レベルのサポート

Windows 10 バージョン 1507 および Windows Server 2016、ディスパッチ レベルで SealMessage/UnsealMessage のサポートを追加します。

## <a name="dtls-12"></a>DTLS 1.2

Windows 10 バージョン 1607 および Windows Server 2016 DTLS 1.2 (RFC 6347) のサポートを追加します。

## <a name="httpsys-thread-pool"></a>HTTP.SYS スレッド プール 

Windows 10 バージョン 1607 および Windows Server 2016 HTTP.SYS.

レジストリのパス: 

HKLM\SYSTEM\CurrentControlSet\Control\LSA

CPU コアあたりの最大スレッド プール サイズを指定するには、作成、**MaxAsyncWorkerThreadsPerCpu**エントリ。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後、DWORD 値を目的のサイズに変更します。 構成しなかった場合、最大値は 1 CPU コアあたり 2 つのスレッドです。

## <a name="next-protocol-negotiation-npn-support"></a>次のプロトコル ネゴシエーション (NPN) サポート

Windows 10 バージョン 1703 以降では、[次へ] プロトコル ネゴシエーション (NPN) は削除されました. 現在サポートされていません

## <a name="pre-shared-key-psk"></a>事前共有キー (PSK)

Windows 10 バージョン 1607 および Windows Server 2016 PSK キー交換アルゴリズム (RFC 4279) のサポートを追加します。

次の PSK 暗号スイートのサポートが追加されました。

- TLS_PSK_WITH_AES_128_CBC_SHA256 (RFC 5487) で Windows 10 バージョン 1607 および Windows Server 2016
- Windows 10 バージョン 1607 および Windows Server 2016 で TLS_PSK_WITH_AES_256_CBC_SHA384(RFC 5487)
- TLS_PSK_WITH_NULL_SHA256 (RFC 5487) で Windows 10 バージョン 1607 および Windows Server 2016
- TLS_PSK_WITH_NULL_SHA384 (RFC 5487) で Windows 10 バージョン 1607 および Windows Server 2016
- TLS_PSK_WITH_AES_128_GCM_SHA256 (RFC 5487) で Windows 10 バージョン 1607 および Windows Server 2016
- TLS_PSK_WITH_AES_256_GCM_SHA384 (RFC 5487) で Windows 10 バージョン 1607 および Windows Server 2016

## <a name="session-resumption-without-server-side-state-server-side-performance-improvements"></a>サーバー側の状態のサーバー側のパフォーマンスが向上なしのセッションの再開

Windows 10 バージョン 1507 および Windows Server 2016、Windows Server 2012 と比較してセッション チケットを 1 秒あたり 30% 以上のセッションの再開を提供します。

## <a name="session-hash-and-extended-master-secret-extension"></a>セッションのハッシュと拡張マスター シークレットの拡張機能

Windows 10 バージョン 1507 および Windows Server 2016 は、RFC 7627 のサポートを追加します。トランスポート層セキュリティ (TLS) セッション ハッシュし、マスター シークレットの拡張機能を拡張します。

この変更のため Windows 10 および Windows Server 2016 が必要ですサード パーティの[CNG SSL プロバイダー](https://msdn.microsoft.com/library/windows/desktop/ff468652.aspx) NCRYPT_SSL_INTERFACE_VERSION_3 をサポートするために、この新しいインターフェイスを記述して、更新プログラム。


## <a name="ssl-support"></a>SSL のサポート

Windows 10 バージョン 1607 および Windows Server 2016 以降では、TLS クライアントとサーバーの SSL 3.0 は、既定で無効にします。 つまり、アプリケーションまたはサービス具体的には、SSPI を使用して SSL 3.0 を要求しない限り、ことはありませんが、クライアントの提供または SSL 3.0 をそのまま使用およびサーバーは SSL 3.0 を選択しません。

SSL 2.0 は、Windows 10 バージョン 1607 および Windows Server 2016 以降は削除されましたおよび現在サポートされていません。

## <a name="changes-to-windows-tls-adherence-to-tls-12-requirements-for-connections-with-non-compliant-tls-clients"></a>TLS の非対応のクライアント接続での TLS 1.2 要件に準拠している Windows TLS の変更

TLS 1.2 では、クライアントを使用して、["signature_algorithms"拡張子](https://tools.ietf.org/html/rfc5246#section-7.4.1.4.1)(つまり、サーバー証明書とサーバー キーの交換など)、デジタル署名する/署名ハッシュ アルゴリズム ペアを使用することは、サーバーに示すためにします。 TLS 1.2 RFC では、サーバー証明書のメッセージが"signature_algorithms"拡張機能を尊重することも必要です。

「クライアントに"signature_algorithms"拡張機能が提供されている場合、サーバーによって提供されるすべての証明書署名が必要その拡張機能に表示されるハッシュ/署名アルゴリズム ペアでします。」

実際には、一部のサード パーティ製 TLS クライアントしないすべての署名を含めるし、"signature_algorithms"拡張機能に許容されるアルゴリズム ペアのハッシュには、TLS 1.2 RFC と失敗の遵守、または拡張機能を完全に省略 (後者ことを示しますサーバーにクライアントに RSA、DSA、ECDSA と SHA1 のみがサポートしている)。

TLS サーバーの 1 つの証明書が、サーバーが常に、クライアントの要件を満たす証明書を提供することはできませんが、エンドポイントごとに構成が多くの場合のみです。

Windows 10 および Windows Server 2016、Windows TLS スタックする前に忠実に準拠させる、TLS 1.2 RFC 要件では、RFC 非対応の TLS クライアントとの相互運用性の問題と結果の接続が失敗します。 Windows 10 と Windows Server 2016 で制約を緩和し、サーバーの唯一のオプションが表示される場合、サーバーで TLS 1.2 の RFC に準拠していない証明書を送信できます。 クライアントは続行またはハンドシェイクを終了し、可能性があります。

サーバーとクライアント証明書を検証するとき、Windows TLS スタック TLS 1.2 RFC に厳密に準拠しているでき、のみネゴシエートされた署名とハッシュ アルゴリズム、サーバーとクライアント証明書にできます。


