---
title: TLS (Schannel SSP)
ms.prod: windows-server
ms.topic: article
ms.assetid: ebd3c40c-b4c0-4f6d-a00c-f90eda4691df
manager: alanth
author: justinha
ms.technology: security-authentication
ms.date: 05/16/2018
ms.openlocfilehash: 3547c77e8c58bcbb219a7b017c3186f198007805
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80820165"
---
# <a name="tls-schannel-ssp-changes-in-windows-10-and-windows-server-2016"></a>Windows 10 および Windows Server 2016 での TLS (Schannel SSP) の変更点

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows 10

## <a name="cipher-suite-changes"></a>暗号スイートの変更

Windows 10、バージョン1511、および Windows Server 2016 では、モバイルデバイス管理 (MDM) を使用した暗号スイート順序の構成のサポートが追加されています。

暗号スイートの優先順位の変更については、「 [Schannel の暗号スイート](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx)」を参照してください。

次の暗号スイートのサポートが追加されました。

- TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 (RFC 5289) (Windows 10、バージョン1507、Windows Server 2016)
- TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384 (RFC 5289) (Windows 10、バージョン1507、Windows Server 2016)

次の暗号スイートの DisabledByDefault の変更:

- TLS_DHE_DSS_WITH_AES_256_CBC_SHA256 (RFC 5246) (Windows 10、バージョン 1703)
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA256 (RFC 5246) (Windows 10、バージョン 1703)
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA (RFC 5246) (Windows 10、バージョン 1703)
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA (RFC 5246) (Windows 10、バージョン 1703)
- TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA (RFC 5246) (Windows 10、バージョン 1703)
- Windows 10 バージョン1709の TLS_RSA_WITH_RC4_128_SHA
- Windows 10 バージョン1709の TLS_RSA_WITH_RC4_128_MD5

Windows 10、バージョン1507、および Windows Server 2016 以降では、既定で SHA 512 証明書がサポートされています。

### <a name="rsa-key-changes"></a>RSA キーの変更

Windows 10、バージョン1507、および Windows Server 2016 クライアント RSA キーサイズのレジストリ構成オプションを追加します。

詳細については、「 [Keyexchangealgorithm-クライアント RSA キーのサイズ](tls-registry-settings.md#keyexchangealgorithm---client-rsa-key-sizes)」を参照してください。

### <a name="diffie-hellman-key-changes"></a>Diffie-hellman キーの変更

Windows 10、バージョン1507、および Windows Server 2016 Diffie-hellman キーサイズのレジストリ構成オプションを追加します。

詳細については、「 [Keyexchangealgorithm-diffie-hellman キーのサイズ](tls-registry-settings.md#keyexchangealgorithm---diffie-hellman-key-sizes)」を参照してください。

### <a name="sch_use_strong_crypto-option-changes"></a>SCH_USE_STRONG_CRYPTO オプションの変更

Windows 10、バージョン1507、および Windows Server 2016 では、 [SCH_USE_STRONG_CRYPTO](https://msdn.microsoft.com/library/windows/desktop/aa379810.aspx)オプションによって、NULL、MD5、DES、およびエクスポートの暗号が無効になります。

## <a name="elliptical-curve-changes"></a>楕円曲線の変化

Windows 10、バージョン1507、および Windows Server 2016 コンピューターの構成 > 管理用テンプレート > ネットワーク > SSL 構成設定の下にある楕円曲線のグループポリシー構成を追加します。 [ECC 曲線の順序] の一覧では、楕円曲線を優先する順序を指定します。また、有効になっていないサポートされる曲線も有効にします。 
 
次の楕円曲線のサポートが追加されました。

- BrainpoolP256r1 (RFC 7027) (Windows 10、バージョン1507、Windows Server 2016)
- BrainpoolP384r1 (RFC 7027) (Windows 10、バージョン1507、Windows Server 2016) 
- BrainpoolP512r1 (RFC 7027) (Windows 10、バージョン1507、Windows Server 2016)
- Curve25519 (RFC draft-ietf-Curve25519) (Windows 10、バージョン1607、Windows Server 2016)

## <a name="dispatch-level-support-for-sealmessage--unsealmessage"></a>SealMessage & UnsealMessage のディスパッチレベルサポート

Windows 10、バージョン1507、および Windows Server 2016 では、ディスパッチレベルで SealMessage/UnsealMessage のサポートが追加されています。

## <a name="dtls-12"></a>DTLS 1.2

Windows 10、バージョン1607、および Windows Server 2016 では、DTLS 1.2 (RFC 6347) のサポートが追加されています。

## <a name="httpsys-thread-pool"></a>HTTP.SYS スレッドプール 

Windows 10、バージョン1607、および Windows Server 2016 HTTP の TLS ハンドシェイクを処理するために使用されるスレッドプールのサイズのレジストリ構成を追加します。SYS.DATABASES.

レジストリ パス: 

HKLM\SYSTEM\CurrentControlSet\Control\LSA

CPU コアあたりの最大スレッドプールサイズを指定するには、 **MaxAsyncWorkerThreadsPerCpu**エントリを作成します。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後、DWORD 値を目的のサイズに変更します。 構成されていない場合、最大値は CPU コアあたり2スレッドです。

## <a name="next-protocol-negotiation-npn-support"></a>次のプロトコルネゴシエーション (NPN) のサポート

Windows 10 バージョン1703以降では、次のプロトコルネゴシエーション (NPN) が削除され、サポートされなくなりました。

## <a name="pre-shared-key-psk"></a>事前共有キー (PSK)

Windows 10、バージョン1607、および Windows Server 2016 では、PSK キー交換アルゴリズム (RFC 4279) のサポートが追加されています。

次の PSK 暗号スイートのサポートが追加されました。

- TLS_PSK_WITH_AES_128_CBC_SHA256 (RFC 5487) (Windows 10、バージョン1607、Windows Server 2016)
- TLS_PSK_WITH_AES_256_CBC_SHA384 (RFC 5487) (Windows 10、バージョン1607、Windows Server 2016)
- TLS_PSK_WITH_NULL_SHA256 (RFC 5487) (Windows 10、バージョン1607、Windows Server 2016)
- TLS_PSK_WITH_NULL_SHA384 (RFC 5487) (Windows 10、バージョン1607、Windows Server 2016)
- TLS_PSK_WITH_AES_128_GCM_SHA256 (RFC 5487) (Windows 10、バージョン1607、Windows Server 2016)
- TLS_PSK_WITH_AES_256_GCM_SHA384 (RFC 5487) (Windows 10、バージョン1607、Windows Server 2016)

## <a name="session-resumption-without-server-side-state-server-side-performance-improvements"></a>サーバー側の状態サーバー側のパフォーマンス向上を伴わないセッションの再開

Windows 10、バージョン1507、および Windows Server 2016 では、セッションチケットが Windows Server 2012 と比較して、1秒あたり30% 以上のセッション再開が提供されます。

## <a name="session-hash-and-extended-master-secret-extension"></a>セッションハッシュと拡張マスタシークレット拡張機能

Windows 10、バージョン1507、および Windows Server 2016 では、RFC 7627: Transport Layer Security (TLS) セッションハッシュと拡張マスタシークレット拡張機能のサポートが追加されています。

この変更のため、Windows 10 および Windows Server 2016 では、NCRYPT_SSL_INTERFACE_VERSION_3 をサポートし、この新しいインターフェイスについて説明するために、サードパーティの[CNG SSL プロバイダー](https://msdn.microsoft.com/library/windows/desktop/ff468652.aspx)の更新が必要です。


## <a name="ssl-support"></a>SSL のサポート

Windows 10、バージョン1607、および Windows Server 2016 以降では、TLS クライアントとサーバー SSL 3.0 は既定で無効になっています。 これは、アプリケーションまたはサービスが SSPI を介して SSL 3.0 を明示的に要求しない限り、クライアントは SSL 3.0 を提供または受け入れません。また、サーバーは SSL 3.0 を選択しません。

Windows 10 バージョン1607および Windows Server 2016 以降では、SSL 2.0 は削除されており、サポートされなくなりました。

## <a name="changes-to-windows-tls-adherence-to-tls-12-requirements-for-connections-with-non-compliant-tls-clients"></a>準拠していない TLS クライアントとの接続に関する Windows TLS 1.2 の要件に対する変更

TLS 1.2 では、クライアントは["signature_algorithms" 拡張機能](https://tools.ietf.org/html/rfc5246#section-7.4.1.4.1)を使用して、署名/ハッシュアルゴリズムペアがデジタル署名 (つまり、サーバー証明書とサーバーキー交換) で使用できることをサーバーに示します。 TLS 1.2 RFC では、サーバー証明書メッセージが "signature_algorithms" 拡張機能を優先する必要もあります。

"クライアントが" signature_algorithms "拡張機能を提供した場合、サーバーによって提供されるすべての証明書は、その拡張機能に表示されるハッシュ/署名アルゴリズムペアによって署名されている必要があります。"

実際には、一部のサードパーティの TLS クライアントが TLS 1.2 RFC に準拠しておらず、"signature_algorithms" 拡張で受け入れようとしているすべての署名とハッシュアルゴリズムのペアを含めることができません。また、拡張機能を完全に省略することもできます (後者の場合、クライアントは、RSA、DSA、ECDSA を使用した SHA1

TLS サーバーでは、多くの場合、エンドポイントごとに1つの証明書が構成されます。つまり、サーバーがクライアントの要件を満たす証明書を常に提供することはできません。

Windows 10 および Windows Server 2016 より前では、Windows TLS スタックは TLS 1.2 RFC 要件に厳密に準拠しており、その結果、RFC 非準拠の TLS クライアントとの相互運用性の問題に対する接続エラーが発生します。 Windows 10 および Windows Server 2016 では、制約が緩和され、サーバーは TLS 1.2 RFC に準拠していない証明書をサーバーの唯一のオプションとして送信できます。 その後、クライアントはハンドシェイクを続行または終了できます。

サーバーとクライアントの証明書を検証するとき、Windows TLS スタックは TLS 1.2 RFC に厳密に準拠し、サーバーとクライアントの証明書でネゴシエートされた署名とハッシュアルゴリズムのみを許可します。


