---
title: TLS (Schannel SSP)
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: ebd3c40c-b4c0-4f6d-a00c-f90eda4691df
manager: alanth
author: justinha
ms.technology: security-authentication
ms.date: 05/16/2018
ms.openlocfilehash: 030fd81e0c6ba0423f1fa73e680006766cf2b180
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890773"
---
# <a name="tls-schannel-ssp-changes-in-windows-10-and-windows-server-2016"></a>Windows 10 および Windows Server 2016 での TLS (Schannel SSP) の変更

>適用先:Windows Server (半期チャネル)、Windows Server 2016 および Windows 10

## <a name="cipher-suite-changes"></a>暗号スイートの変更

Windows 10、バージョン 1511 および Windows Server 2016 は、モバイル デバイス管理 (MDM) を使用して暗号の順位の構成のサポートを追加します。

暗号スイートの優先度の順序の変更、次を参照してください。 [Schannel の暗号スイート](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx)します。

次の暗号スイートのサポートが追加されました。

- TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 (RFC 5289) で Windows 10 バージョン 1507、Windows Server 2016
- TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384 (RFC 5289) で Windows 10 バージョン 1507、Windows Server 2016

DisabledByDefault は、次の暗号スイートを変更します。

- TLS_DHE_DSS_WITH_AES_256_CBC_SHA256 (RFC 5246) で Windows 10 バージョン 1703
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA256 (RFC 5246) で Windows 10 バージョン 1703
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA (RFC 5246) で Windows 10 バージョン 1703
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA (RFC 5246) で Windows 10 バージョン 1703
- TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA (RFC 5246) で Windows 10 バージョン 1703
- Windows 10 バージョン 1709 で TLS_RSA_WITH_RC4_128_SHA
- Windows 10 バージョン 1709 で TLS_RSA_WITH_RC4_128_MD5

SHA 512 証明書は Windows 10 バージョン 1507、Windows Server 2016 以降、既定でサポートされます。

### <a name="rsa-key-changes"></a>RSA キーの変更

Windows 10 バージョン 1507、Windows Server 2016 は、RSA キーのサイズがクライアントのレジストリ構成のオプションを追加します。

詳細については、次を参照してください。 [KeyExchangeAlgorithm - クライアントの RSA キー サイズ](tls-registry-settings.md#keyexchangealgorithm---client-rsa-key-sizes)します。

### <a name="diffie-hellman-key-changes"></a>Diffie-hellman キーの変更

Windows 10 バージョン 1507、Windows Server 2016 は、Diffie-hellman キーのサイズのレジストリ構成のオプションを追加します。

詳細については、次を参照してください。 [KeyExchangeAlgorithm - Diffie-hellman キー サイズ](tls-registry-settings.md#keyexchangealgorithm---diffie-hellman-key-sizes)します。

### <a name="schusestrongcrypto-option-changes"></a>SCH_USE_STRONG_CRYPTO オプションの変更

Windows 10、バージョン 1507、Windows Server 2016 と[SCH_USE_STRONG_CRYPTO](https://msdn.microsoft.com/library/windows/desktop/aa379810.aspx)オプションを今すぐ無効にします。 null の場合、MD5、DES、および暗号をエクスポートします。

## <a name="elliptical-curve-changes"></a>楕円曲線を変更します。

Windows 10 バージョン 1507、Windows Server 2016 の コンピュータの構成、楕円曲線グループ ポリシー構成の追加 > 管理用テンプレート > ネットワーク > SSL 構成設定。 ECC 曲線の注文リスト楕円曲線の優先順序を指定だけでなくにより、サポートされている曲線が有効になりません。 
 
次の楕円曲線のサポートが追加されました。

- BrainpoolP256r1 (RFC 7027) で Windows 10 バージョン 1507、Windows Server 2016
- BrainpoolP384r1 (RFC 7027) で Windows 10 バージョン 1507、Windows Server 2016 
- BrainpoolP512r1 (RFC 7027) で Windows 10 バージョン 1507、Windows Server 2016
- Curve25519 (RFC ドラフト-ietf-tls-curve25519) で Windows 10、バージョン 1607 および Windows Server 2016

## <a name="dispatch-level-support-for-sealmessage--unsealmessage"></a>SealMessage & UnsealMessage ディスパッチ レベルのサポート

Windows 10 バージョン 1507、Windows Server 2016 は、ディスパッチ レベル SealMessage/UnsealMessage サポートを追加します。

## <a name="dtls-12"></a>DTLS 1.2

Windows 10、バージョン 1607 および Windows Server 2016 DTLS 1.2 (RFC 6347) のサポートを追加します。

## <a name="httpsys-thread-pool"></a>HTTP。SYS スレッド プール 

Windows 10、バージョン 1607 および Windows Server 2016 は、HTTP の TLS ハンドシェイクを処理するために使用されるスレッド プールのサイズのレジストリ構成を追加します。SYS です。

レジストリ パス: 

HKLM\SYSTEM\CurrentControlSet\Control\LSA

CPU コアあたりの最大スレッド プール サイズを指定するには、作成、 **MaxAsyncWorkerThreadsPerCpu**エントリ。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後は、目的のサイズに DWORD 値を変更します。 構成しなかった場合、最大値は CPU コアあたり 2 スレッドです。

## <a name="next-protocol-negotiation-npn-support"></a>[次へ] のプロトコル ネゴシエーション (NPN) サポート

[次へ] プロトコル ネゴシエーション (NPN) は Windows 10 バージョン 1703 以降が削除され、現在サポートされていません。

## <a name="pre-shared-key-psk"></a>事前共有キー (PSK)

Windows 10、バージョン 1607 および Windows Server 2016 は、キー交換アルゴリズムの PSK (RFC 4279) のサポートを追加します。

次の PSK 暗号スイートのサポートが追加されました。

- TLS_PSK_WITH_AES_128_CBC_SHA256 (RFC 5487) で Windows 10、バージョン 1607 および Windows Server 2016
- Windows 10、バージョン 1607 および Windows Server 2016 で TLS_PSK_WITH_AES_256_CBC_SHA384(RFC 5487)
- TLS_PSK_WITH_NULL_SHA256 (RFC 5487) で Windows 10、バージョン 1607 および Windows Server 2016
- TLS_PSK_WITH_NULL_SHA384 (RFC 5487) で Windows 10、バージョン 1607 および Windows Server 2016
- TLS_PSK_WITH_AES_128_GCM_SHA256 (RFC 5487) で Windows 10、バージョン 1607 および Windows Server 2016
- TLS_PSK_WITH_AES_256_GCM_SHA384 (RFC 5487) で Windows 10、バージョン 1607 および Windows Server 2016

## <a name="session-resumption-without-server-side-state-server-side-performance-improvements"></a>サーバー側の状態のサーバー側のパフォーマンスの向上せず、セッションの再開

Windows 10 バージョン 1507、Windows Server 2016 は、Windows Server 2012 と比較したセッション チケットを 1 秒あたりの 30% 以上のセッションの再開を提供します。

## <a name="session-hash-and-extended-master-secret-extension"></a>セッションのハッシュと拡張のマスター シークレットの拡張機能

Windows 10 バージョン 1507、Windows Server 2016 は、RFC 7627 のサポートを追加します。トランスポート層セキュリティ (TLS) セッション ハッシュし、マスター シークレットの拡張機能を拡張します。

この変更により Windows 10 および Windows Server 2016 でサード パーティが必要[CNG SSL プロバイダー](https://msdn.microsoft.com/library/windows/desktop/ff468652.aspx) NCRYPT_SSL_INTERFACE_VERSION_3 をサポートし、この新しいインターフェイスの記述に更新します。


## <a name="ssl-support"></a>SSL のサポート

Windows 10、バージョン 1607 および Windows Server 2016 以降、TLS クライアントとサーバーの SSL 3.0 が既定で無効にします。 つまり、アプリケーションまたはサービス要求、SSPI を使用して、SSL 3.0 が具体的には、しない限りことはありませんが、クライアントの提供または SSL 3.0 を受け入れる、サーバーが SSL 3.0 を選択することはありません。

SSL 2.0 は以降 Windows 10 バージョン 1607 および Windows Server 2016 が削除され、現在サポートされていません。

## <a name="changes-to-windows-tls-adherence-to-tls-12-requirements-for-connections-with-non-compliant-tls-clients"></a>Windows TLS は非準拠の TLS クライアントとの接続の TLS 1.2 の要件に準拠しているへの変更

TLS 1.2 では、クライアントを使用して、 ["signature_algorithms"拡張子](https://tools.ietf.org/html/rfc5246#section-7.4.1.4.1)をサーバーに (つまり、サーバー証明書とサーバー キー交換)、デジタル署名でどの署名/ハッシュ アルゴリズムの組み合わせを使用することを示します。 TLS 1.2 の RFC では、サーバー証明書のメッセージが"signature_algorithms"拡張機能を優先することも必要です。

「クライアントに"signature_algorithms"拡張機能が提供されている場合、サーバーによって提供されるすべての証明書によって署名その拡張機能に表示されるハッシュ/署名アルゴリズム ペア。」

実際には、一部のサード パーティ製 TLS クライアントに準拠するすべての署名を含めるし、ハッシュ アルゴリズムのペアを許容する"signature_algorithms"拡張機能では、TLS 1.2 の RFC と失敗しているまたはしないで、拡張機能を完全に省略 (後者することを示しますサーバー、クライアントが RSA や DSA、ECDSA と SHA1 のみをサポートする)。

TLS サーバーの 1 つの証明書が、サーバーが常に、クライアントの要件を満たす証明書を提供することはできませんが、エンドポイントごとに構成が多くの場合のみです。

前の Windows 10 および Windows Server 2016、Windows の TLS スタックに厳密に従う、TLS 1.2 の RFC 要件では、RFC 準拠の TLS クライアントとの相互運用性の問題で接続エラーになります。 Windows 10 と Windows Server 2016 では、制約が緩和され、サーバーの唯一のオプションがある場合、サーバーで TLS 1.2 の RFC に準拠していない証明書を送信できます。 クライアントは続行またはハンドシェイクを終了し可能性があります。

サーバーとクライアント証明書を検証するには、Windows TLS スタックは厳密に TLS 1.2 の RFC に準拠しているし、サーバーとクライアント証明書では、ネゴシエートされた署名とハッシュ アルゴリズムのみでいます。


