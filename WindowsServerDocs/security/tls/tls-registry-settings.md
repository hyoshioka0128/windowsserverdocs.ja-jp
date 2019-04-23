---
title: トランスポート層セキュリティ (TLS) レジストリ設定
description: Windows Server のセキュリティ
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-tls-ssl
ms.tgt_pltfrm: na
ms.topic: article
author: justinha
ms.author: justinha
manager: brianlic-msft
ms.date: 02/28/2019
ms.openlocfilehash: 0d618d465ee45245e98fbc6aa58b32b974be08e8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880883"
---
# <a name="transport-layer-security-tls-registry-settings"></a>トランスポート層セキュリティ (TLS) レジストリ設定

>適用対象:Windows Server 2019、Windows Server 2016、Windows 10 の Windows Server (半期チャネル)

IT プロフェッショナル向けのこのリファレンス トピックには、トランスポート層セキュリティ (TLS) プロトコルと、Schannel セキュリティ サポートを通じて、Secure Sockets Layer (SSL) プロトコルの Windows 実装に対するサポートされているレジストリ設定の情報が含まれています。プロバイダー (SSP) です。 レジストリ サブキーとエントリを管理し、Schannel SSP をトラブルシューティングするこのトピックに関するヘルプについて具体的には、TLS と SSL プロトコル。 

>[!Caution]
>この情報は、トラブルシューティングを行うとき、または必要な設定が適用されていることを確認するときに参照してください。 他の手段がない限り、レジストリは直接編集しないことをお勧めします。
>レジストリに対する変更は、レジストリ エディターまたは Windows オペレーティング システムによる検証は行われずに適用されます。 このため、不適切な値が設定される場合があり、これにより回復不能なシステム エラーが発生することがあります。 可能な場合は、レジストリを直接編集するのではなく、グループ ポリシー、Microsoft 管理コンソール (MMC) などの Windows ツールを使用して作業を行います。 レジストリを編集する必要がある場合は、細心の注意が必要です。 

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

レジストリ パス:HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

## <a name="ciphers"></a>Ciphers

TLS/SSL 暗号は、暗号の順位を構成することで制御する必要があります。 詳細については、次を参照してください。[構成 TLS 暗号の順位](manage-tls.md#configuring-tls-cipher-suite-order)します。

Schannel SSP で使用される既定の暗号スイートの順序については、次を参照してください。 [in TLS/SSL (Schannel SSP) 暗号スイート](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx)します。 

##<a name="ciphersuites"></a>CipherSuites

TLS/SSL 暗号の構成を行う必要があるグループ ポリシーを MDM または PowerShell を使用して参照してください[TLS 暗号スイートの順序の構成](manage-tls.md#configuring-tls-cipher-suite-order)詳細についてはします。

Schannel SSP で使用される既定の暗号スイートの順序については、次を参照してください。 [in TLS/SSL (Schannel SSP) 暗号スイート](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx)します。 


## <a name="clientcachetime"></a>ClientCacheTime

このエントリは、クライアント側のキャッシュ エントリの有効期限が切れるまでのオペレーティング システムの時間をミリ秒単位で制御します。 値 0 の場合、セキュリティで保護された接続のキャッシュが無効になります。 既定では、このエントリはレジストリに存在しません。 

クライアントが初めて Schannel SSP 経由でサーバーに接続すると、フル TLS/SSL ハンドシェイクが実行されます。 これが完了すると、マスター シークレット、暗号スイート、および証明書は、クライアントおよびサーバーそれぞれのセッション キャッシュに格納されます。

Windows Server 2008 および Windows Vista 以降、既定のクライアント キャッシュ時間は、10 時間です。

レジストリ パス:HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

既定のクライアント キャッシュ時間

## <a name="enableocspstaplingforsni"></a>EnableOcspStaplingForSni

オンライン証明書状態プロトコル (OCSP) のホチキス止めなどインターネット インフォメーション サービス (IIS)、サーバー証明書を TLS ハンドシェイク中に、クライアントに送信するときにサーバー証明書の現在の失効状態を提供する、web サーバーを使用できます。 この機能は、web サーバーはサーバー証明書の現在の OCSP の状態をキャッシュでき、複数の web クライアントに送信するために、OCSP サーバーの負荷を短縮します。 各 web クライアントが、この機能を使用せずには、OCSP サーバーからサーバー証明書の現在の OCSP の状態を取得してみてください。 これは、OCSP サーバー上の高負荷を生成します。 

だけでなく、IIS web サービスは、http.sys をしてからこの設定は、Active Directory フェデレーション サービス (AD FS) など、Web アプリケーション プロキシ (WAP) も効果的です。 

既定では、単純なセキュリティで保護された (SSL/TLS) バインドを持つ IIS の web サイトの OCSP のサポートが有効にします。 ただし、このサポートが有効になっていません既定では、IIS web サイトがセキュリティで保護された (SSL/TLS) バインドの種類は次の一方または両方を使用する場合。
- Server Name Indication が必要
- 集中証明書ストアを使用する

この場合は、TLS ハンドシェイク中に server こんにちはの応答は含まれませんホチキス止め OCSP の状態は既定では。 この動作は、パフォーマンスが向上します。Windows OCSP ホチキス止めの実装は、何百ものサーバー証明書にスケールされます。 SNI と CCS 何千もを何千ものサーバー証明書を持つ可能性のある web サイトの IIS を有効にする、ために、既定で有効にするには、この動作を設定とパフォーマンスの問題が発生する可能性があります。

適用可能なバージョン:Windows Server 2012 および Windows 8 以降のすべてのバージョン。 

レジストリ パス: [hkey_local_machine \system\currentcontrolset\control\securityproviders\schannel]

次のキーを追加します。

"EnableOcspStaplingForSni"= dword:00000001

を無効にするには、DWORD 値を 0 に設定します。

"EnableOcspStaplingForSni"dword:00000000 を =

>[!NOTE] 
>このレジストリ キーを有効にするには、潜在的なパフォーマンスに影響があります。

## <a name="fipsalgorithmpolicy"></a>FIPSAlgorithmPolicy

このエントリは、連邦情報処理規格 (FIPS) コンプライアンスを制御します。 既定値は 0 です。

適用可能なバージョン:Windows Server 2012 および Windows 8 以降のすべてのバージョン。 

レジストリ パス:HKLM SYSTEM\CurrentControlSet\Control\LSA

Windows Server FIPS 暗号スイート:参照してください[Schannel SSP の暗号スイートとプロトコルをサポートされている](https://technet.microsoft.com/library/dn786419.aspx)します。

## <a name="hashes"></a>Hashes

TLS/SSL ハッシュ アルゴリズムは、暗号の順位を構成することで制御する必要があります。 参照してください[構成 TLS 暗号の順位](manage-tls.md#configuring-tls-cipher-suite-order)詳細についてはします。

## <a name="issuercachesize"></a>IssuerCacheSize

このエントリは、発行者のキャッシュのサイズを制御し、発行者のマッピングで使用されます。 Schannel SSP は、クライアント証明書の直接の発行者だけでなく、クライアントの証明書チェーンに含まれるすべての発行者をマップしようとします。 発行者は、通常、アカウントにはマップされていませんが、その場合、サーバーは同じ発行者名を繰り返しマップしようとすることがあり、その回数は 1 秒あたり数百回に及びます。 

これを回避するために、サーバーにはネガティブ キャッシュが用意されており、発行者名がアカウントにマップされていないと、その発行者はキャッシュに追加されます。Schannel SSP は、キャッシュ エントリの有効期限が切れるまで、この発行者名をマップしません。 このレジストリ エントリは、キャッシュ サイズを指定します。 既定では、このエントリはレジストリに存在しません。 既定値は 100 です。 

適用可能なバージョン:Windows Server 2008 および Windows Vista 以降のすべてのバージョン。

レジストリ パス:HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

## <a name="issuercachetime"></a>IssuerCacheTime

このエントリは、キャッシュ タイムアウト間隔をミリ秒単位で制御します。 Schannel SSP は、クライアント証明書の直接の発行者だけでなく、クライアントの証明書チェーンに含まれるすべての発行者をマップしようとします。 発行者は、通常、アカウントにはマップされていませんが、その場合、サーバーは同じ発行者名を繰り返しマップしようとすることがあり、その回数は 1 秒あたり数百回に及びます。

これを回避するために、サーバーにはネガティブ キャッシュが用意されており、発行者名がアカウントにマップされていないと、その発行者はキャッシュに追加されます。Schannel SSP は、キャッシュ エントリの有効期限が切れるまで、この発行者名をマップしません。 パフォーマンス上の理由から、このキャッシュは保持されるため、同じ発行者はマップされなくなります。 既定では、このエントリはレジストリに存在しません。 既定値は 10 分です。

適用可能なバージョン:Windows Server 2008 および Windows Vista 以降のすべてのバージョン。

レジストリ パス:HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

## <a name="keyexchangealgorithm---client-rsa-key-sizes"></a>KeyExchangeAlgorithm - クライアント RSA キー サイズ

このエントリは、クライアントの RSA キー サイズを制御します。 

キー交換アルゴリズムの使用は、暗号の順位を構成することで制御する必要があります。

Windows 10 バージョン 1507、Windows Server 2016 で追加します。

レジストリ パス:HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\KeyExchangeAlgorithms\PKCS

TLS クライアントの最低限サポートされている範囲の RSA キーのビット長を指定するには、作成、 **ClientMinKeyBitLength**エントリ。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後は、必要なビット長を DWORD 値を変更します。 構成しなかった場合、1024 ビットが最小になります。 

TLS クライアントの最大サポートされている範囲の RSA キーのビット長を指定するには、作成、 **ClientMaxKeyBitLength**エントリ。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後は、必要なビット長を DWORD 値を変更します。 構成されていない場合、最大は適用されません。

## <a name="keyexchangealgorithm---diffie-hellman-key-sizes"></a>KeyExchangeAlgorithm - Diffie-hellman キーのサイズ

このエントリは、Diffie-hellman キーのサイズを制御します。 

キー交換アルゴリズムの使用は、暗号の順位を構成することで制御する必要があります。

Windows 10 バージョン 1507、Windows Server 2016 で追加します。

レジストリ パス:HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\KeyExchangeAlgorithms\Diffie-Hellman

TLS クライアントの最低限サポートされている範囲の 1 つの Helman キーのビット長を指定するには、作成、 **ClientMinKeyBitLength**エントリ。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後は、必要なビット長を DWORD 値を変更します。 構成しなかった場合、1024 ビットが最小になります。 
 
TLS クライアントの最大サポートされている範囲の 1 つの Helman キーのビット長を指定するには、作成、 **ClientMaxKeyBitLength**エントリ。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後は、必要なビット長を DWORD 値を変更します。 構成されていない場合、最大は適用されません。 
 
TLS サーバーの既定値の 1 つ Helman キー ビット長を指定するには、作成、 **ServerMinKeyBitLength**エントリ。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後は、必要なビット長を DWORD 値を変更します。 構成しなかった場合、2048 ビットは既定値になります。 

## <a name="maximumcachesize"></a>MaximumCacheSize

このエントリは、キャッシュ要素の最大数を制御します。 MaximumCacheSize を 0 に設定すると、サーバー側のセッション キャッシュが無効になり、再接続できなくなります。 前の MaximumCacheSize を増やすと、既定値によって Lsass.exe が消費するメモリ量が多くなります。 通常、各セッション キャッシュ要素には、2 ~ 4 KB のメモリが必要です。 既定では、このエントリはレジストリに存在しません。 既定値は、20,000 要素です。 

適用可能なバージョン:Windows Server 2008 および Windows Vista 以降のすべてのバージョン。

レジストリ パス:HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

## <a name="messaging--fragment-parsing"></a>– メッセージ フラグメントの解析

________________________________________
このエントリは、最大許容される断片化の TLS ハンドシェイク メッセージのサイズを制御します。 許可されているサイズを超えるメッセージは受け入れられません、TLS ハンドシェイクが失敗します。 これらのエントリのレジストリに既定ではありません。 

値を 0x0 に設定すると断片化されたメッセージは処理されず、TLS ハンドシェイクが失敗すると、します。 これにより、TLS クライアントまたはサーバーの現在のコンピューター、TLS の Rfc に準拠します。 

最大許容サイズを大きくできる最大 2 ^24-1 バイトです。 お勧めでありの各セキュリティ コンテキストの追加のメモリを消費する、クライアントまたはサーバーを読み取り、大量のネットワークからの未検証のデータを格納することができます。 

7 および Windows Server 2008 R2、Windows で追加します。
Windows XP、Windows Vista、または断片化した TLS/SSL ハンドシェイク メッセージを解析する Windows Server 2008 の Internet Explorer を使用する更新プログラムは使用できます。

レジストリ パス:HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Messaging

TLS クライアントが受け入れる断片化の TLS ハンドシェイク メッセージのサイズの上限を指定するには、作成、 **MessageLimitClient**エントリ。 エントリを作成した後は、必要なビット長を DWORD 値を変更します。 構成しなかった場合、既定値は 0x8000 バイトになります。 

クライアント認証がない場合、TLS サーバーが受け入れる断片化の TLS ハンドシェイク メッセージのサイズの上限を指定するには、作成、 **MessageLimitServer**エントリ。 エントリを作成した後は、必要なビット長を DWORD 値を変更します。 構成しなかった場合、既定値は 0x4000 バイトになります。 

クライアント認証がある場合に、TLS サーバーが受け入れる断片化の TLS ハンドシェイク メッセージのサイズの上限を指定するには、作成、 **MessageLimitServerClientAuth**エントリ。 エントリを作成した後は、必要なビット長を DWORD 値を変更します。 構成しなかった場合、既定値は 0x8000 バイトになります。 

## <a name="sendtrustedissuerlist"></a>SendTrustedIssuerList

このエントリは、信頼された発行者一覧の送信時に使用されるフラグを制御します。 クライアント認証に対して数百の証明機関を信頼しているサーバーの場合、発行者が多すぎて、そのサーバーは、クライアント認証を要求するときに、発行者の一部をクライアント コンピューターに送信できません。 このレジストリ キーは、この状況で設定できます。これにより、Schannel SSP は部分的な一覧を送信するのではなく、まったく送信しなくなります。

信頼された発行者の一覧を送信しないと、クライアント証明書が要求されたときにクライアントが送信する内容に影響する可能性があります。 たとえば、Internet Explorer がクライアント認証要求を受信するときに表示されるのは、サーバーによって送信された証明機関のいずれかにチェーンでつながっているクライアント証明書のみです。 サーバーが一覧を送信しなかった場合、Internet Explorer には、クライアントにインストールされているすべてのクライアントの証明書が表示されます。 

この動作が望ましいことがあります。 たとえば、PKI 環境にクロス証明書が含まれる場合、クライアント証明書とサーバーの証明書のルート CA は同じではありません。したがって、Internet Explorer は、サーバーの CA のいずれかにチェーンでつながっている証明書を選択できません。 信頼された発行者の一覧を送信しないようにサーバーを構成すると、Internet Explorer はその証明書すべてを送信します。

既定では、このエントリはレジストリに存在しません。

既定の信頼された発行者の一覧の送信動作

| Windows のバージョン | 時間 |
|-----------------|------|
| Windows Server 2012 および Windows 8 以降 | FALSE |
| Windows Server 2008 R2 および Windows 7 およびそれ以前 | TRUE |

適用可能なバージョン:Windows Server 2008 および Windows Vista 以降のすべてのバージョン。

レジストリ パス:HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

## <a name="servercachetime"></a>ServerCacheTime

このエントリは、サーバー側のキャッシュ エントリの有効期限が切れるまでのオペレーティング システムの時間をミリ秒単位で制御します。 値を 0 に設定すると、サーバー側のセッション キャッシュが無効になり、再接続できなくなります。 前の ServerCacheTime を増やすと、既定値によって Lsass.exe が消費するメモリ量が多くなります。 通常、各セッション キャッシュ要素には、2 ~ 4 KB のメモリが必要です。 既定では、このエントリはレジストリに存在しません。 

適用可能なバージョン:Windows Server 2008 および Windows Vista 以降のすべてのバージョン。

レジストリ パス:HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

既定のサーバー キャッシュ時間:10 時間

## <a name="ssl-20"></a>SSL 2.0

このサブキーは、SSL 2.0 の使用を制御します。

SSL 2.0 は以降、Windows 10、バージョン 1607 および Windows Server 2016 が削除され、現在サポートされていません。
SSL 2.0 を既定の設定では、次を参照してください。 [in TLS/SSL (Schannel SSP) プロトコル](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx)します。 

レジストリ パス:HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

SSL 2.0 プロトコルを有効にするには作成、**有効**クライアントまたはサーバーのいずれかのサブキーを次の表に示すように入力します。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後は、DWORD 値を 1 に変更します。 

SSL 2.0 サブキーの表

| サブキー | 説明 |
|--------|-------------|
| クライアント | SSL クライアントで SSL 2.0 の使用を制御します。 |
| Server | SSL のサーバーで SSL 2.0 の使用を制御します。 |

SSL 2.0 のクライアントまたはサーバーを無効にするには、DWORD 値を 0 に変更します。 SSL 2.0 を使用する SSPI アプリが要求している場合は拒否されます。 

SSL 2.0 を既定で無効にして、作成、 **DisabledByDefault**エントリと変更、DWORD の値を 1 にします。 SSPI のアプリ明示的 SSL 2.0 を使用する場合、ネゴシエートされる場合があります。 

SSL 2.0 のレジストリで無効になっている、次の例です。

![SSL 2.0 を無効になっています](images/ssl-2-registry-setting.png)


## <a name="ssl-30"></a>SSL 3.0

このサブキーは、SSL 3.0 の使用を制御します。

以降、Windows 10、バージョン 1607 および Windows Server 2016 では、SSL 3.0 は、既定で無効されています。 SSL 3.0 の既定の設定を参照してください。 [in TLS/SSL (Schannel SSP) プロトコル](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx)します。 

レジストリ パス:HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

SSL 3.0 プロトコルを有効にするには作成、**有効**クライアントまたはサーバーのいずれかのサブキーを次の表に示すように入力します。  
既定では、このエントリはレジストリに存在しません。 エントリを作成した後は、DWORD 値を 1 に変更します。 

SSL 3.0 サブキーの表

| サブキー | 説明 |
|--------|-------------|
| クライアント | SSL クライアントで SSL 3.0 の使用を制御します。 |
| Server | SSL のサーバーで SSL 3.0 の使用を制御します。 |

をクライアントまたはサーバーの SSL 3.0 を無効にするには、DWORD 値を 0 に変更します。
SSL 3.0 を使用する SSPI アプリが要求している場合は拒否されます。 

既定で SSL 3.0 を無効にして、作成、 **DisabledByDefault**エントリと変更、DWORD 値 1 をします。 SSL 3.0 を使用する SSPI アプリケーションが明示的に要求している場合はネゴシエート可能性があります。 

SSL 3.0 がレジストリで無効になっている、次の例です。

![SSL 3.0 を無効になっています](images/ssl-3-registry-setting.png)

## <a name="tls-10"></a>TLS 1.0

このサブキーは、TLS 1.0 の使用を制御します。

TLS 1.0 の既定の設定を参照してください。 [in TLS/SSL (Schannel SSP) プロトコル](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx)します。

レジストリ パス:HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

TLS 1.0 プロトコルを有効にするのには、作成、**有効**クライアントまたはサーバーのいずれかのサブキーの次の表に示すエントリ。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後は、DWORD 値を 1 に変更します。 

TLS 1.0 サブキーの表

| サブキー | 説明 |
|--------|-------------|
| クライアント | TLS クライアントで TLS 1.0 の使用を制御します。 |
| Server | TLS サーバーで TLS 1.0 の使用を制御します。 |

TLS 1.0 クライアントまたはサーバーを無効にするには、DWORD 値を 0 に変更します。
TLS 1.0 を使用する SSPI アプリが要求している場合は拒否されます。 

を既定で TLS 1.0 を無効にするのには、作成、 **DisabledByDefault**エントリと変更、DWORD の値を 1 にします。 SSPI アプリは、TLS 1.0 を使用して明示的に要求している場合はネゴシエート可能性があります。 

次の例は、レジストリで無効になっている TLS 1.0 を示しています。

![TLS 1.0 を無効になっています](images/tls-registry-setting.png)

## <a name="tls-11"></a>TLS 1.1

このサブキーは、TLS 1.1 の使用を制御します。

TLS 1.1 の既定の設定を参照してください。 [in TLS/SSL (Schannel SSP) プロトコル](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx)します。

レジストリ パス:HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

TLS 1.1 プロトコルを有効にするのには、作成、**有効**クライアントまたはサーバーのいずれかのサブキーの次の表に示すエントリ。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後は、DWORD 値を 1 に変更します。 

TLS 1.1 サブキーの表

| サブキー | 説明 |
|--------|-------------|
| クライアント | TLS クライアントで TLS 1.1 の使用を制御します。 |
| Server | TLS サーバーで TLS 1.1 の使用を制御します。 |

TLS 1.1 クライアントまたはサーバーを無効にするには、DWORD 値を 0 に変更します。
TLS 1.1 を使用する SSPI アプリが要求している場合は拒否されます。 

を既定で TLS 1.1 を無効にするのには、作成、 **DisabledByDefault**エントリと変更、DWORD の値を 1 にします。 TLS 1.1 を使用する SSPI アプリケーションが明示的に要求している場合はネゴシエート可能性があります。 

次の例は、レジストリで無効になっている TLS 1.1 を示しています。

![TLS 1.1 が無効になっています](images/tls-11-registry-setting.png)

## <a name="tls-12"></a>TLS 1.2

このサブキーは、TLS 1.2 の使用を制御します。

TLS 1.2 の既定の設定を参照してください。 [in TLS/SSL (Schannel SSP) プロトコル](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx)します。

レジストリ パス:HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

TLS 1.2 プロトコルを有効にするのには、作成、**有効**クライアントまたはサーバーのいずれかのサブキーの次の表に示すエントリ。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後は、DWORD 値を 1 に変更します。 

TLS 1.2 サブキーの表

| サブキー | 説明 |
|--------|-------------|
| クライアント | TLS クライアントで TLS 1.2 の使用を制御します。 |
| Server | TLS サーバーで TLS 1.2 の使用を制御します。 |

TLS 1.2 クライアントまたはサーバーを無効にするには、DWORD 値を 0 に変更します。
TLS 1.2 を使用する SSPI アプリが要求している場合は拒否されます。 

TLS 1.2 を既定で無効にするのには、作成、 **DisabledByDefault**エントリと変更、DWORD の値を 1 にします。 TLS 1.2 を使用する SSPI アプリケーションが明示的に要求している場合はネゴシエート可能性があります。 

次の例は、レジストリで無効になっている TLS 1.2 を示しています。

![TLS 1.2 が無効になっています](images/tls-12-registry-setting.png)

## <a name="dtls-10"></a>DTLS 1.0

このサブキーは、DTLS 1.0 の使用を制御します。

DTLS 1.0 の既定の設定を参照してください。 [in TLS/SSL (Schannel SSP) プロトコル](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx)します。

レジストリ パス:HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

DTLS 1.0 プロトコルを有効にするのには、作成、**有効**クライアントまたはサーバーのいずれかのサブキーの次の表に示すエントリ。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後は、DWORD 値を 1 に変更します。 

DTLS 1.0 サブキーの表

| サブキー | 説明 |
|--------|-------------|
| クライアント | DTLS クライアントで DTLS 1.0 の使用を制御します。 |
| Server | DTLS サーバーで DTLS 1.0 の使用を制御します。 |

DTLS 1.0 クライアントまたはサーバーを無効にするには、DWORD 値を 0 に変更します。
DTLS 1.0 を使用する SSPI アプリが要求している場合は拒否されます。 

DTLS 1.0 を既定で無効にするのには、作成、 **DisabledByDefault**エントリと変更、DWORD の値を 1 にします。 DTLS 1.0 を使用する SSPI アプリケーションが明示的に要求している場合はネゴシエート可能性があります。 

次の例は、レジストリで無効になっている DTLS 1.0 を示しています。

![DTLS 1.0 を無効になっています](images/dtls-10-registry-setting.png)

## <a name="dtls-12"></a>DTLS 1.2

このサブキーは、DTLS 1.2 の使用を制御します。

DTLS 1.2 の既定の設定を参照してください。 [in TLS/SSL (Schannel SSP) プロトコル](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx)します。

レジストリ パス:HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

DTLS 1.2 プロトコルを有効にするのには、作成、**有効**クライアントまたはサーバーのいずれかのサブキーの次の表に示すエントリ。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後は、DWORD 値を 1 に変更します。 

DTLS 1.2 サブキーの表

| サブキー | 説明 |
|--------|-------------|
| クライアント | DTLS クライアントで DTLS 1.2 の使用を制御します。 |
| Server | DTLS サーバーで DTLS 1.2 の使用を制御します。 |


DTLS 1.2 クライアントまたはサーバーを無効にするには、DWORD 値を 0 に変更します。
DTLS 1.0 を使用する SSPI アプリが要求している場合は拒否されます。 

DTLS 1.2 を既定で無効にするのには、作成、 **DisabledByDefault**エントリと変更、DWORD の値を 1 にします。 DTLS 1.2 を使用する SSPI アプリケーションが明示的に要求している場合はネゴシエート可能性があります。 

次の例は、レジストリで無効になっている DTLS 1.1 を示しています。

![DTLS 1.1 が無効になっています](images/dtls-11-registry-setting.png)


