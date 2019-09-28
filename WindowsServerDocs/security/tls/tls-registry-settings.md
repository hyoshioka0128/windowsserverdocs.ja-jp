---
title: トランスポート層セキュリティ (TLS) のレジストリ設定
description: Windows Server のセキュリティ
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: security-tls-ssl
ms.tgt_pltfrm: na
ms.topic: article
author: justinha
ms.author: justinha
manager: brianlic-msft
ms.date: 02/28/2019
ms.openlocfilehash: 60202e537093bd21515043ba56f70f3895c91d42
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403410"
---
# <a name="transport-layer-security-tls-registry-settings"></a>トランスポート層セキュリティ (TLS) のレジストリ設定

>適用対象:Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows 10

IT プロフェッショナル向けのこのリファレンストピックでは、Schannel セキュリティサポートを通じて、トランスポート層セキュリティ (TLS) プロトコルと Secure Sockets Layer (SSL) プロトコルの Windows 実装でサポートされているレジストリ設定情報を示します。プロバイダー (SSP)。 このトピックで説明するレジストリサブキーとエントリは、Schannel SSP、特に TLS および SSL プロトコルの管理とトラブルシューティングに役立ちます。 

> [!CAUTION]
> この情報は、トラブルシューティングを行うとき、または必要な設定が適用されていることを確認するときに参照してください。
> 他の手段がない限り、レジストリは直接編集しないことをお勧めします。
> レジストリに対する変更は、レジストリ エディターまたは Windows オペレーティング システムによる検証は行われずに適用されます。
> このため、不適切な値が設定される場合があり、これにより回復不能なシステム エラーが発生することがあります。
> 可能な場合は、レジストリを直接編集するのではなく、グループ ポリシー、Microsoft 管理コンソール (MMC) などの Windows ツールを使用して作業を行います。
> レジストリを編集する必要がある場合は、細心の注意が必要です。

## <a name="certificatemappingmethods"></a>CertificateMappingMethods 

既定では、このエントリはレジストリに存在しません。 既定値は以下に示す 4 つの証明書マッピング メソッドで、このメソッドすべてがサポートされています。

サーバー アプリケーションにクライアント認証が必要な場合、Schannel は、クライアント コンピューターによって指定された証明書をユーザー アカウントに自動的にマップしようとします。 クライアント証明書を使用してサインインするユーザーを認証するには、マッピングを作成します。これにより、証明書の情報が Windows ユーザー アカウントに関連付けられます。 証明書のマッピングを作成して有効にすると、そのユーザーは、クライアントがクライアント証明書を提示するたびに、サーバー アプリケーションによって適切な Windows ユーザー アカウントに自動的に関連付けられます。

ほとんどの場合、証明書は次の 2 つの方法のいずれかでユーザー アカウントにマップされます。 

- 1 つの証明書が 1 つのユーザー アカウントにマップされる (1 対 1 のマッピング)
- 複数の証明書が 1 つのユーザー アカウントにマップされる (多対 1 のマッピング)

既定では、Schannel プロバイダーは、4 つの証明書マッピング メソッドを次の優先順位で使用します。

1. Kerberos service-for-user (S4U) 証明書マッピング
2. ユーザー プリンシパル名マッピング
3. 1 対 1 のマッピング (サブジェクト/発行者マッピングとも呼ばれます)
4. 多対 1 のマッピング

適用可能なバージョン:このトピックの最初に示した「**適用先**」を参照。

レジストリパス:HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

## <a name="ciphers"></a>Ciphers

TLS/SSL 暗号は、暗号スイートの順序を構成することによって制御する必要があります。 詳細については、「 [TLS 暗号スイートの順序の構成](manage-tls.md#configuring-tls-cipher-suite-order)」を参照してください。

Schannel SSP によって使用される既定の暗号スイートの順序の詳細については、「 [TLS/SSL (SCHANNEL ssp) の暗号スイート](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx)」を参照してください。 

## <a name="ciphersuites"></a>CipherSuites

TLS/SSL 暗号スイートの構成は、グループポリシー、MDM、または PowerShell を使用して行う必要があります。詳細については、「 [Tls 暗号スイートの順序の構成](manage-tls.md#configuring-tls-cipher-suite-order)」を参照してください。

Schannel SSP によって使用される既定の暗号スイートの順序の詳細については、「 [TLS/SSL (SCHANNEL ssp) の暗号スイート](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx)」を参照してください。 


## <a name="clientcachetime"></a>ClientCacheTime

このエントリは、クライアント側のキャッシュ エントリの有効期限が切れるまでのオペレーティング システムの時間をミリ秒単位で制御します。 値 0 の場合、セキュリティで保護された接続のキャッシュが無効になります。 既定では、このエントリはレジストリに存在しません。 

クライアントが初めて Schannel SSP 経由でサーバーに接続すると、フル TLS/SSL ハンドシェイクが実行されます。 これが完了すると、マスター シークレット、暗号スイート、および証明書は、クライアントおよびサーバーそれぞれのセッション キャッシュに格納されます。

Windows Server 2008 および Windows Vista 以降では、クライアントの既定のキャッシュ時間は10時間です。

レジストリパス:HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

既定のクライアント キャッシュ時間

## <a name="enableocspstaplingforsni"></a>EnableOcspStaplingForSni

オンライン証明書状態プロトコル (OCSP) のホチキス止めは、インターネットインフォメーションサービス (IIS) などの web サーバーが、TLS ハンドシェイク中にサーバー証明書をクライアントに送信するときに、サーバー証明書の現在の失効ステータスを提供することを可能にします。 この機能により、web サーバーはサーバー証明書の現在の OCSP ステータスをキャッシュし、それを複数の web クライアントに送信できるため、OCSP サーバーの負荷が軽減されます。 この機能がないと、各 web クライアントは OCSP サーバーからサーバー証明書の現在の OCSP ステータスを取得しようとします。 これにより、その OCSP サーバーに高い負荷が発生します。 

IIS に加えて、http.sys 経由の web サービスは、Active Directory フェデレーションサービス (AD FS) (AD FS) や Web アプリケーションプロキシ (WAP) などのこの設定の恩恵を受けることもできます。 

既定では、OCSP のサポートは、単純なセキュリティで保護された (SSL/TLS) バインドを持つ IIS web サイトに対して有効になっています。 ただし、IIS web サイトで次の種類の secure (SSL/TLS) バインドのいずれかまたは両方が使用されている場合、このサポートは既定では有効になりません。
- Server Name Indication が必要
- 集中証明書ストアを使用する

この場合、TLS ハンドシェイク中のサーバー hello 応答には、既定で OCSP ホチキス止めステータスは含まれません。 この動作により、パフォーマンスが向上します。Windows OCSP ホチキス止めの実装は、数百のサーバー証明書にスケーリングします。 SNI と CCS を使用すると、何千ものサーバー証明書を持つ可能性のある数千人の web サイトに IIS を拡張できます。この動作を既定で有効に設定すると、パフォーマンスの問題が発生する可能性があります。

適用可能なバージョン:Windows Server 2012 および Windows 8 以降のすべてのバージョン。 

レジストリパス: [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL]

次のキーを追加します。

"EnableOcspStaplingForSni" = dword: 00000001

無効にするには、DWORD 値を0に設定します。

"EnableOcspStaplingForSni" = dword: 00000000

> [!NOTE] 
> このレジストリキーを有効にすると、パフォーマンスに影響する可能性があります。

## <a name="fipsalgorithmpolicy"></a>FIPSAlgorithmPolicy

このエントリは、連邦情報処理規格 (FIPS) コンプライアンスを制御します。 既定値は 0 です。

適用可能なバージョン:Windows Server 2012 および Windows 8 以降のすべてのバージョン。 

レジストリパス:HKLM SYSTEM\CurrentControlSet\Control\LSA

Windows Server FIPS 暗号スイート:「[サポートされている暗号スイートと SCHANNEL SSP のプロトコル](https://technet.microsoft.com/library/dn786419.aspx)」を参照してください。

## <a name="hashes"></a>Hashes

TLS/SSL ハッシュアルゴリズムは、暗号スイートの順序を構成することによって制御する必要があります。 詳細については、「 [TLS 暗号スイートの構成](manage-tls.md#configuring-tls-cipher-suite-order)」を参照してください。

## <a name="issuercachesize"></a>IssuerCacheSize

このエントリは、発行者のキャッシュのサイズを制御し、発行者のマッピングで使用されます。 Schannel SSP は、クライアント証明書の直接の発行者だけでなく、クライアントの証明書チェーン内のすべての発行者をマップしようとします。 発行者は、通常、アカウントにはマップされていませんが、その場合、サーバーは同じ発行者名を繰り返しマップしようとすることがあり、その回数は 1 秒あたり数百回に及びます。 

これを回避するために、サーバーにはネガティブ キャッシュが用意されており、発行者名がアカウントにマップされていないと、その発行者はキャッシュに追加されます。Schannel SSP は、キャッシュ エントリの有効期限が切れるまで、この発行者名をマップしません。 このレジストリ エントリは、キャッシュ サイズを指定します。 既定では、このエントリはレジストリに存在しません。 既定値は 100 です。 

適用可能なバージョン:Windows Server 2008 および Windows Vista 以降のすべてのバージョン。

レジストリパス:HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

## <a name="issuercachetime"></a>IssuerCacheTime

このエントリは、キャッシュ タイムアウト間隔をミリ秒単位で制御します。 Schannel SSP は、クライアント証明書の直接の発行者だけでなく、クライアントの証明書チェーン内のすべての発行者をマップしようとします。 発行者は、通常、アカウントにはマップされていませんが、その場合、サーバーは同じ発行者名を繰り返しマップしようとすることがあり、その回数は 1 秒あたり数百回に及びます。

これを回避するために、サーバーにはネガティブ キャッシュが用意されており、発行者名がアカウントにマップされていないと、その発行者はキャッシュに追加されます。Schannel SSP は、キャッシュ エントリの有効期限が切れるまで、この発行者名をマップしません。 パフォーマンス上の理由から、このキャッシュは保持されるため、同じ発行者はマップされなくなります。 既定では、このエントリはレジストリに存在しません。 既定値は 10 分です。

適用可能なバージョン:Windows Server 2008 および Windows Vista 以降のすべてのバージョン。

レジストリパス:HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

## <a name="keyexchangealgorithm---client-rsa-key-sizes"></a>KeyExchangeAlgorithm-クライアント RSA キーのサイズ

このエントリは、クライアントの RSA キーのサイズを制御します。 

キー交換アルゴリズムの使用は、暗号スイートの順序を構成することによって制御する必要があります。

Windows 10、バージョン1507、および Windows Server 2016 で追加されました。

レジストリパス:HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\KeyExchangeAlgorithms\PKCS

TLS クライアントでサポートされる RSA キーのビット長の最小範囲を指定するには、 **Clientminkeybitlength**エントリを作成します。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後、DWORD 値を目的のビット長に変更します。 構成されていない場合、1024ビットが最小値になります。 

TLS クライアントでサポートされる RSA キーのビット長の最大範囲を指定するには、 **Clientmaxkeybitlength**エントリを作成します。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後、DWORD 値を目的のビット長に変更します。 構成されていない場合、最大値は適用されません。

## <a name="keyexchangealgorithm---diffie-hellman-key-sizes"></a>KeyExchangeAlgorithm-Diffie-hellman キーのサイズ

このエントリは、Diffie-hellman のキーサイズを制御します。 

キー交換アルゴリズムの使用は、暗号スイートの順序を構成することによって制御する必要があります。

Windows 10、バージョン1507、および Windows Server 2016 で追加されました。

レジストリパス:HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\KeyExchangeAlgorithms\Diffie-Hellman

TLS クライアントの最小サポート範囲である Diffie-hellman Man キーの長さを指定するには、 **Clientminkeybitlength**エントリを作成します。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後、DWORD 値を目的のビット長に変更します。 構成されていない場合、1024ビットが最小値になります。 
 
TLS クライアントのサポートされている最大の範囲を指定するには、 **Clientmaxkeybitlength**エントリを作成します。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後、DWORD 値を目的のビット長に変更します。 構成されていない場合、最大値は適用されません。 
 
TLS サーバーの既定値として Diffie-hellman Man キーの長さを指定するには、 **Serverminkeybitlength**エントリを作成します。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後、DWORD 値を目的のビット長に変更します。 構成されていない場合、2048ビットが既定値になります。 

## <a name="maximumcachesize"></a>MaximumCacheSize

このエントリは、キャッシュ要素の最大数を制御します。 MaximumCacheSize を 0 に設定すると、サーバー側のセッション キャッシュが無効になり、再接続できなくなります。 前の MaximumCacheSize を増やすと、既定値によって Lsass.exe が消費するメモリ量が多くなります。 通常、各セッションキャッシュ要素には 2 ~ 4 KB のメモリが必要です。 既定では、このエントリはレジストリに存在しません。 既定値は2万要素です。 

適用可能なバージョン:Windows Server 2008 および Windows Vista 以降のすべてのバージョン。

レジストリパス:HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

## <a name="messaging--fragment-parsing"></a>メッセージング–フラグメント解析

________________________________________
このエントリは、フラグメント化された TLS ハンドシェイクメッセージが許容される最大サイズを制御します。 許容されるサイズを超えるメッセージは受け入れられず、TLS ハンドシェイクは失敗します。 既定では、これらのエントリはレジストリに存在しません。 

値を0x0 に設定すると、フラグメント化されたメッセージは処理されず、TLS ハンドシェイクが失敗します。 これにより、現在のコンピューター上の TLS クライアントまたはサーバーが TLS Rfc に準拠していません。 

最大許容サイズは、最大 2 ^ 24-1 バイトまで増やすことができます。 クライアントまたはサーバーが大量の未確認データをネットワークから読み取り、保存できるようにすることはお勧めできません。また、セキュリティコンテキストごとに追加のメモリを消費します。 

Windows 7 および Windows Server 2008 R2 で追加されました。
Windows XP、Windows Vista、または Windows Server 2008 の Internet Explorer で、断片化された TLS/SSL ハンドシェイクメッセージを解析するための更新プログラムが利用可能になります。

レジストリパス:HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Messaging

TLS クライアントが受け入れる、フラグメント化された TLS ハンドシェイクメッセージの最大許容サイズを指定するには、 **Messagelimitclient**エントリを作成します。 エントリを作成した後、DWORD 値を目的のビット長に変更します。 構成されていない場合、既定値は0x8000 バイトになります。 

クライアント認証がない場合に TLS サーバーが受け入れる、フラグメント化された TLS ハンドシェイクメッセージの最大許容サイズを指定するには、 **Messagelimitserver**エントリを作成します。 エントリを作成した後、DWORD 値を目的のビット長に変更します。 構成されていない場合、既定値は 0x4000 bytes になります。 

クライアント認証があるときに TLS サーバーが受け入れる、フラグメント化された TLS ハンドシェイクメッセージの最大許容サイズを指定するには、 **Messagelimitserverclientauth**エントリを作成します。 エントリを作成した後、DWORD 値を目的のビット長に変更します。 構成されていない場合、既定値は0x8000 バイトになります。 

## <a name="sendtrustedissuerlist"></a>SendTrustedIssuerList

このエントリは、信頼された発行者一覧の送信時に使用されるフラグを制御します。 クライアント認証に対して数百の証明機関を信頼しているサーバーの場合、発行者が多すぎて、そのサーバーは、クライアント認証を要求するときに、発行者の一部をクライアント コンピューターに送信できません。 このレジストリ キーは、この状況で設定できます。これにより、Schannel SSP は部分的な一覧を送信するのではなく、まったく送信しなくなります。

信頼された発行者の一覧を送信しないと、クライアント証明書が要求されたときにクライアントが送信する内容に影響する可能性があります。 たとえば、Internet Explorer がクライアント認証要求を受信するときに表示されるのは、サーバーによって送信された証明機関のいずれかにチェーンでつながっているクライアント証明書のみです。 サーバーが一覧を送信しなかった場合、Internet Explorer には、クライアントにインストールされているすべてのクライアントの証明書が表示されます。 

この動作が望ましいことがあります。 たとえば、PKI 環境にクロス証明書が含まれている場合、クライアント証明書とサーバー証明書のルート CA は同じではありません。したがって、Internet Explorer は、サーバーの Ca のいずれかにチェーンされている証明書を選択することはできません。 信頼された発行者の一覧を送信しないようにサーバーを構成すると、Internet Explorer はその証明書すべてを送信します。

既定では、このエントリはレジストリに存在しません。

既定の信頼された発行者リストの動作

| Windows のバージョン | Time |
|-----------------|------|
| Windows Server 2012 および Windows 8 以降 | false |
| Windows Server 2008 R2 および Windows 7 以前 | true |

適用可能なバージョン:Windows Server 2008 および Windows Vista 以降のすべてのバージョン。

レジストリパス:HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

## <a name="servercachetime"></a>ServerCacheTime

このエントリは、サーバー側のキャッシュ エントリの有効期限が切れるまでのオペレーティング システムの時間をミリ秒単位で制御します。 値を 0 に設定すると、サーバー側のセッション キャッシュが無効になり、再接続できなくなります。 前の ServerCacheTime を増やすと、既定値によって Lsass.exe が消費するメモリ量が多くなります。 通常、各セッションキャッシュ要素には 2 ~ 4 KB のメモリが必要です。 既定では、このエントリはレジストリに存在しません。 

適用可能なバージョン:Windows Server 2008 および Windows Vista 以降のすべてのバージョン。

レジストリパス:HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

既定のサーバーキャッシュ時間:10 時間

## <a name="ssl-20"></a>SSL 2.0

このサブキーは、SSL 2.0 の使用を制御します。

Windows 10、バージョン1607、および Windows Server 2016 以降では、SSL 2.0 は削除されており、サポートされなくなりました。
SSL 2.0 の既定の設定については、「 [TLS/SSL (SCHANNEL SSP) のプロトコル](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx)」を参照してください。 

レジストリパス:HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

SSL 2.0 プロトコルを有効にするには、次の表に示すように、クライアントまたはサーバーのサブキーに**Enabled**エントリを作成します。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後、DWORD 値を1に変更します。 

SSL 2.0 サブキーの表

| サブキー | 説明 |
|--------|-------------|
| クライアント | Ssl クライアントでの SSL 2.0 の使用を制御します。 |
| Server | Ssl サーバーでの SSL 2.0 の使用を制御します。 |

クライアントまたはサーバーの SSL 2.0 を無効にするには、DWORD 値を0に変更します。 SSPI アプリが SSL 2.0 を使用するように要求すると、拒否されます。 

SSL 2.0 を既定で無効にするには、 **DisabledByDefault**エントリを作成し、DWORD 値を1に変更します。 SSPI アプリ explcitly が SSL 2.0 を使用するように要求すると、ネゴシエートされる場合があります。 

次の例では、レジストリで SSL 2.0 が無効になっています。

![SSL 2.0 無効](images/ssl-2-registry-setting.png)


## <a name="ssl-30"></a>SSL 3.0

このサブキーは、SSL 3.0 の使用を制御します。

Windows 10、バージョン1607、および Windows Server 2016 以降では、SSL 3.0 は既定で無効になっています。 SSL 3.0 の既定の設定については、「 [TLS/SSL (SCHANNEL SSP) のプロトコル](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx)」を参照してください。 

レジストリパス:HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

SSL 3.0 プロトコルを有効にするには、次の表に示すように、クライアントまたはサーバーのサブキーに**Enabled**エントリを作成します。  
既定では、このエントリはレジストリに存在しません。 エントリを作成した後、DWORD 値を1に変更します。 

SSL 3.0 サブキーの表

| サブキー | 説明 |
|--------|-------------|
| クライアント | Ssl クライアントでの SSL 3.0 の使用を制御します。 |
| Server | Ssl サーバーでの SSL 3.0 の使用を制御します。 |

クライアントまたはサーバーの SSL 3.0 を無効にするには、DWORD 値を0に変更します。
SSPI アプリが SSL 3.0 を使用するように要求すると、拒否されます。 

SSL 3.0 を既定で無効にするには、 **DisabledByDefault**エントリを作成し、DWORD 値を1に変更します。 SSPI アプリが SSL 3.0 の使用を明示的に要求した場合は、ネゴシエートされる可能性があります。 

次の例では、レジストリで SSL 3.0 が無効になっています。

![SSL 3.0 無効](images/ssl-3-registry-setting.png)

## <a name="tls-10"></a>TLS 1.0

このサブキーは、TLS 1.0 の使用を制御します。

TLS 1.0 の既定の設定については、「 [tls/SSL (SCHANNEL SSP) のプロトコル](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx)」を参照してください。

レジストリパス:HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

TLS 1.0 プロトコルを有効にするには、次の表に示すように、クライアントまたはサーバーのサブキーのいずれかに**Enabled**エントリを作成します。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後、DWORD 値を1に変更します。 

TLS 1.0 サブキーの表

| サブキー | 説明 |
|--------|-------------|
| クライアント | Tls クライアントでの TLS 1.0 の使用を制御します。 |
| Server | Tls サーバーでの TLS 1.0 の使用を制御します。 |

クライアントまたはサーバーの TLS 1.0 を無効にするには、DWORD 値を0に変更します。
SSPI アプリが TLS 1.0 を使用するように要求すると、そのアプリは拒否されます。 

TLS 1.0 を既定で無効にするには、 **DisabledByDefault**エントリを作成し、DWORD 値を1に変更します。 SSPI アプリが TLS 1.0 の使用を明示的に要求した場合は、ネゴシエートされる可能性があります。 

次の例では、レジストリで TLS 1.0 が無効になっています。

![TLS 1.0 無効](images/tls-registry-setting.png)

## <a name="tls-11"></a>TLS 1.1

このサブキーは、TLS 1.1 の使用を制御します。

TLS 1.1 の既定の設定については、「 [tls/SSL (SCHANNEL SSP) のプロトコル](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx)」を参照してください。

レジストリパス:HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

TLS 1.1 プロトコルを有効にするには、次の表に示すように、クライアントまたはサーバーのサブキーのいずれかに**Enabled**エントリを作成します。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後、DWORD 値を1に変更します。 

TLS 1.1 サブキーの表

| サブキー | 説明 |
|--------|-------------|
| クライアント | Tls クライアントでの TLS 1.1 の使用を制御します。 |
| Server | Tls サーバーでの TLS 1.1 の使用を制御します。 |

クライアントまたはサーバーの TLS 1.1 を無効にするには、DWORD 値を0に変更します。
SSPI アプリが TLS 1.1 を使用するように要求すると、そのアプリは拒否されます。 

TLS 1.1 を既定で無効にするには、 **DisabledByDefault**エントリを作成し、DWORD 値を1に変更します。 SSPI アプリが TLS 1.1 の使用を明示的に要求した場合は、ネゴシエートされる可能性があります。 

次の例では、レジストリで TLS 1.1 が無効になっています。

![TLS 1.1 無効](images/tls-11-registry-setting.png)

## <a name="tls-12"></a>TLS 1.2

このサブキーは、TLS 1.2 の使用を制御します。

TLS 1.2 の既定の設定については、「 [tls/SSL (SCHANNEL SSP) のプロトコル](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx)」を参照してください。

レジストリパス:HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

TLS 1.2 プロトコルを有効にするには、次の表に示すように、クライアントまたはサーバーのサブキーのいずれかに**Enabled**エントリを作成します。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後、DWORD 値を1に変更します。 

TLS 1.2 サブキーの表

| サブキー | 説明 |
|--------|-------------|
| クライアント | Tls クライアントでの TLS 1.2 の使用を制御します。 |
| Server | Tls サーバーでの TLS 1.2 の使用を制御します。 |

クライアントまたはサーバーの TLS 1.2 を無効にするには、DWORD 値を0に変更します。
SSPI アプリが TLS 1.2 を使用するように要求すると、そのアプリは拒否されます。 

TLS 1.2 を既定で無効にするには、 **DisabledByDefault**エントリを作成し、DWORD 値を1に変更します。 SSPI アプリが TLS 1.2 の使用を明示的に要求した場合は、ネゴシエートされる可能性があります。 

次の例では、レジストリで TLS 1.2 が無効になっています。

![TLS 1.2 無効](images/tls-12-registry-setting.png)

## <a name="dtls-10"></a>DTLS 1.0

このサブキーは、DTLS 1.0 の使用を制御します。

DTLS 1.0 の既定の設定については、「 [TLS/SSL (SCHANNEL SSP) のプロトコル](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx)」を参照してください。

レジストリパス:HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

DTLS 1.0 プロトコルを有効にするには、次の表に示すように、クライアントまたはサーバーのサブキーのいずれかに**Enabled**エントリを作成します。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後、DWORD 値を1に変更します。 

DTLS 1.0 サブキーの表

| サブキー | 説明 |
|--------|-------------|
| クライアント | DTLS クライアントでの DTLS 1.0 の使用を制御します。 |
| Server | DTLS サーバーでの DTLS 1.0 の使用を制御します。 |

クライアントまたはサーバーの DTLS 1.0 を無効にするには、DWORD 値を0に変更します。
SSPI アプリが DTLS 1.0 を使用するように要求すると、拒否されます。 

既定で DTLS 1.0 を無効にするには、 **DisabledByDefault**エントリを作成し、DWORD 値を1に変更します。 SSPI アプリが DTLS 1.0 の使用を明示的に要求した場合は、ネゴシエートされる可能性があります。 

次の例では、レジストリで DTLS 1.0 が無効になっています。

![DTLS 1.0 無効](images/dtls-10-registry-setting.png)

## <a name="dtls-12"></a>DTLS 1.2

このサブキーは、DTLS 1.2 の使用を制御します。

DTLS 1.2 の既定の設定については、「 [TLS/SSL (SCHANNEL SSP) のプロトコル](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx)」を参照してください。

レジストリパス:HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

DTLS 1.2 プロトコルを有効にするには、次の表に示すように、クライアントまたはサーバーのサブキーのいずれかに**Enabled**エントリを作成します。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後、DWORD 値を1に変更します。 

DTLS 1.2 サブキーの表

| サブキー | 説明 |
|--------|-------------|
| クライアント | DTLS クライアントでの DTLS 1.2 の使用を制御します。 |
| Server | DTLS サーバーでの DTLS 1.2 の使用を制御します。 |


クライアントまたはサーバーの DTLS 1.2 を無効にするには、DWORD 値を0に変更します。
SSPI アプリが DTLS 1.0 を使用するように要求すると、拒否されます。 

既定で DTLS 1.2 を無効にするには、 **DisabledByDefault**エントリを作成し、DWORD 値を1に変更します。 SSPI アプリが DTLS 1.2 の使用を明示的に要求した場合は、ネゴシエートされる可能性があります。 

次の例では、レジストリで DTLS 1.1 が無効になっています。

![DTLS 1.1 無効](images/dtls-11-registry-setting.png)


