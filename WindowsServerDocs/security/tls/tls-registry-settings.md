---
title: "トランスポート層セキュリティ (TLS) のレジストリ設定"
description: "Windows Server のセキュリティ"
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
ms.date: 08/07/2017
ms.openlocfilehash: 8ccfacc367a5d32438bebf22798479a07f6cbdfc
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# <a name="transport-layer-security-tls-registry-settings"></a>トランスポート層セキュリティ (TLS) のレジストリ設定

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2008 R2、Windows Server 2008、Windows 10、Windows 8.1、Windows 8、Windows 7、Windows Vista

IT プロフェッショナル向けのこのリファレンス トピックには、トランスポート層セキュリティ (TLS) プロトコルと Secure Sockets Layer (SSL) プロトコルを介して、Schannel セキュリティ サポート プロバイダー (SSP) の Windows 実装のサポートされているレジストリ設定情報が含まれています。 レジストリ サブキーとエントリについてのこのトピックのヘルプ トピックを管理して、Schannel SSP のトラブルシューティングを行う具体的には、TLS と SSL プロトコルです。 

>[!Caution]
>この情報は、トラブルシューティングを行うや、必要な設定が適用されているかを確認するときに使用する参照として提供されます。 ない直接レジストリを編集するその他の選択肢がない限り、ことをお勧めします。
>レジストリに対する変更は検証されませんによって、レジストリ エディターまたは Windows オペレーティング システムによって適用されます。 その結果、正しくない値を格納できるになり、このことができます回復不能なエラーで、システム。 可能であれば、直接、レジストリの編集ではなくを使用してグループ ポリシーまたはその他の Windows ツール (MMC) Microsoft 管理コンソールなどのタスクを実行します。 レジストリを編集する必要がある場合、は、細心の注意を使用します。 

## <a name="certificatemappingmethods"></a>CertificateMappingMethods 

既定では、このエントリはレジストリに存在しません。 既定値は、以下に示すすべての 4 つの証明書マッピング メソッドがサポートされていることです。

サーバー アプリケーションは、クライアント認証を必要とする場合、Schannel は自動的にクライアント コンピューターがユーザー アカウントに付属している証明書をマップする試みます。 関連する Windows ユーザー アカウントに証明書の情報のマッピングを作成することで、クライアント証明書を使用してログオンするユーザーを認証することができます。 作成して、証明書のマッピングを有効にすると、クライアントが、クライアント証明書を提示するたびに、サーバー アプリケーションに自動的にそのユーザー アカウントに関連付けられて、適切な Windows ユーザー。

ほとんどの場合、証明書は 2 つの方法のいずれかでユーザー アカウントにマップします。 

- 単一の証明書は、1 人のユーザー アカウント (1 対 1 のマッピング) にマップされます。
- 複数の証明書は、1 つのユーザー アカウント (多対 1 のマッピング) にマップされます。

既定では、Schannel プロバイダーは次の 4 つの証明書マッピング メソッドは、基本設定の順序で一覧表示を使用します。

1. Kerberos サービスからユーザー用 (S4U) 証明書のマッピング
2. ユーザー プリンシパル名マッピング
3. 1 対 1 のマッピング (とも呼ばれるサブジェクト/発行者マッピング)
4. 多対 1 のマッピング

適用可能なバージョン: で指定されていると、**適用先**このトピックの冒頭にあるリスト。

レジストリ パス: HKLM system \currentcontrolset\control\securityproviders\schannel

## <a name="ciphers"></a>暗号

TLS/SSL 暗号は、暗号の順位を構成することによって制御する必要があります。 詳細については、次を参照してください。[構成 TLS 暗号の順位](manage-tls.md#configuring-tls-cipher-suite-order)します。

Schannel SSP で使用される既定の暗号スイートの順序の詳細については、次を参照してください。[TLS/SSL (Schannel SSP) の暗号スイート](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx)します。 

##<a name="ciphersuites"></a>CipherSuites

TLS と SSL 暗号の構成を行う必要がありますを参照してグループ ポリシー、MDM または、PowerShell を使用して[構成 TLS 暗号の順位](manage-tls.md#configuring-tls-cipher-suite-order)詳細についてはします。

Schannel SSP で使用される既定の暗号スイートの順序の詳細については、次を参照してください。[TLS/SSL (Schannel SSP) の暗号スイート](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx)します。 


## <a name="clientcachetime"></a>ClientCacheTime

このエントリは、オペレーティング システムに必要な時間 (ミリ秒単位) のクライアント側キャッシュ エントリの有効期限が切れる時間数を制御します。 値 0 は、セキュリティで保護された接続のキャッシュをオフにします。 既定では、このエントリはレジストリに存在しません。 

クライアントが、完全、Schannel SSP 経由でサーバーに接続を初めて TLS/SSL のハンドシェイクを実行します。 これが完了したら、マスター シークレット、暗号スイート、および証明書は、それぞれのクライアントとサーバー上のセッション キャッシュに保存されます。

Windows Server 2008 および Windows Vista 以降、既定のクライアント キャッシュ時間は、10 時間です。

レジストリ パス: HKLM system \currentcontrolset\control\securityproviders\schannel

既定のクライアント キャッシュ時間

## <a name="fipsalgorithmpolicy"></a>FIPSAlgorithmPolicy

このエントリは、連邦情報処理 (FIPS) コンプライアンスを制御します。 既定値は0です。

適用可能なバージョン: で指定されていると、**適用先**このトピックの冒頭にあるリスト。 

レジストリ パス: HKLM system \currentcontrolset\control\lsa

Windows Server FIPS 暗号スイート。を参照してください[サポートされている暗号スイートおよび Schannel SSP のプロトコル](https://technet.microsoft.com/library/dn786419.aspx)します。

## <a name="hashes"></a>ハッシュ

TLS と SSL のハッシュ アルゴリズムは、暗号の順位を構成することによって制御する必要があります。 参照してください[構成 TLS 暗号の順位](manage-tls.md#configuring-tls-cipher-suite-order)詳細についてはします。

## <a name="issuercachesize"></a>IssuerCacheSize

このエントリは、発行者のキャッシュのサイズを制御し、発行者のマッピングで使用されます。 Schannel SSP がすべてのクライアントの証明書チェーン内の発行者をマップしようとした場合、クライアント証明書の直接の発行者だけでなくします。 発行者は、一般的な場合は、アカウントにマップされないときに、サーバー可能性がありますマップしようとする同じ発行者名を繰り返し、1 秒あたり数百ものです。 

これを防止するため、キャッシュ エントリの有効期限が切れる発行者の名前がアカウントにマップされない場合は、キャッシュに追加されます Schannel SSP はしないマップしようとするまでは再度発行者名サーバー ネガティブ キャッシュをしています。 このレジストリ エントリでは、キャッシュ サイズを指定します。 既定では、このエントリはレジストリに存在しません。 既定値は 100 です。 

適用可能なバージョン: で指定されていると、**適用先**このトピックの冒頭にあるリスト。

レジストリ パス: HKLM system \currentcontrolset\control\securityproviders\schannel

## <a name="issuercachetime"></a>IssuerCacheTime

このエントリは、キャッシュ タイムアウト間隔 (ミリ秒単位) の長さを制御します。 Schannel SSP がすべてのクライアントの証明書チェーン内の発行者をマップしようとした場合、クライアント証明書の直接の発行者だけでなくします。 場合はここで、発行者をマップしないように、アカウントは、一般的な場合は、サーバーがマップしようとする同じ発行者名を繰り返し、1 秒あたり数百ものです。

これを防止するため、キャッシュ エントリの有効期限が切れる発行者の名前がアカウントにマップされない場合は、キャッシュに追加されます Schannel SSP はしないマップしようとするまでは再度発行者名サーバー ネガティブ キャッシュをしています。 システムは、同じ発行者をマップしようとしています。を続行しないように、パフォーマンス上の理由から、このキャッシュが保持されます。 既定では、このエントリはレジストリに存在しません。 既定値は、10 分です。

適用可能なバージョン: で指定されていると、**適用先**このトピックの冒頭にあるリスト。

レジストリ パス: HKLM system \currentcontrolset\control\securityproviders\schannel

## <a name="keyexchangealgorithm---client-rsa-key-sizes"></a>KeyExchangeAlgorithm - クライアント RSA キーのサイズ

このエントリは、クライアントの RSA キーのサイズを制御します。 

キー交換アルゴリズムの使用は、暗号の順位を構成することによって制御必要があります。

Windows 10 バージョン 1507 および Windows Server 2016 で追加します。

レジストリ パス: HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\KeyExchangeAlgorithms\PKCS

TLS クライアントの最小サポートされている範囲の RSA キー ビット長を指定するには、作成、**ClientMinKeyBitLength**エントリ。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後は、必要なビット長を DWORD 値を変更します。 構成しなかった場合、1024 ビットが最小になります。 

TLS クライアントの最大サポートされている範囲の RSA キー ビット長を指定するには、作成、**ClientMaxKeyBitLength**エントリ。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後は、必要なビット長を DWORD 値を変更します。 構成しなかった場合、最大数は強制されません。

## <a name="keyexchangealgorithm---diffie-hellman-key-sizes"></a>KeyExchangeAlgorithm - Diffie-hellman キー サイズ

このエントリは、Diffie-hellman キーのサイズを制御します。 

キー交換アルゴリズムの使用は、暗号の順位を構成することによって制御必要があります。

Windows 10 バージョン 1507 および Windows Server 2016 で追加します。

レジストリ パス: HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\KeyExchangeAlgorithms\Diffie しました。

TLS クライアントの最小サポートされている範囲の 1 つの Helman ビットのキー長を指定するには、作成、**ClientMinKeyBitLength**エントリ。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後は、必要なビット長を DWORD 値を変更します。 構成しなかった場合、1024 ビットが最小になります。 
 
TLS クライアントの最大サポートされている範囲の 1 つの Helman ビットのキー長を指定するには、作成、**ClientMaxKeyBitLength**エントリ。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後は、必要なビット長を DWORD 値を変更します。 構成しなかった場合、最大数は強制されません。 
 
TLS サーバーの既定値の 1 つ Helman キー ビット長を指定するには、作成、**ServerMinKeyBitLength**エントリ。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後は、必要なビット長を DWORD 値を変更します。 構成しなかった場合、2048 ビットを既定となります。 

## <a name="maximumcachesize"></a>MaximumCacheSize

このエントリは、キャッシュ要素の最大数を制御します。 MaximumCacheSize を 0 に設定では、サーバー側のセッション キャッシュを無効になり、再接続できなくなります。 増やす MaximumCacheSize、既定値によって Lsass.exe が消費するメモリを追加します。 通常、各セッション キャッシュ要素には、2 ~ 4 KB のメモリーが必要です。 既定では、このエントリはレジストリに存在しません。 既定値は 20,000 要素です。 

適用可能なバージョン: で指定されていると、**適用先**このトピックの冒頭にあるリスト。

レジストリ パス: HKLM system \currentcontrolset\control\securityproviders\schannel

## <a name="messaging--fragment-parsing"></a>メッセージング – フラグメント解析

________________________________________
このエントリは、受け付けられる断片化された TLS ハンドシェイク メッセージのサイズが最大値を制御します。 メッセージが許可されているサイズよりも大きい受け付けられません、TLS ハンドシェイクが失敗します。 これらのエントリのレジストリに既定ではありません。 

0x0 に値を設定するときに断片化されたメッセージは処理されず、TLS ハンドシェイクが失敗すると、します。 これにより、TLS クライアントまたはサーバーの現在のマシン TLS の Rfc に準拠します。 

最大 2 サイズを増やすことが許可される最大 ^24-1 バイトです。 読み取り、大量のネットワークから未検証のデータを格納するには、クライアントまたはサーバーを許可しないことをお勧めは、各セキュリティ コンテキストでの他のメモリを消費します。 

7 および Windows Server 2008 R2、Windows で追加します。
Windows XP、Windows Vista、または断片化された TLS/SSL のハンドシェイク メッセージを解釈する Windows Server 2008 での Internet Explorer をできるようにする更新プログラムは使用できます。

レジストリ パス: HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Messaging

TLS クライアントが受け入れる断片化の TLS ハンドシェイク メッセージのサイズの上限を指定するには、作成、**MessageLimitClient**エントリ。 エントリを作成した後は、必要なビット長を DWORD 値を変更します。 構成しなかった場合、既定値は 0x8000 バイトになります。 

最大クライアント認証がない場合、TLS サーバーが受け入れる断片化の TLS ハンドシェイク メッセージのサイズを指定するには、作成、**MessageLimitServer**エントリ。 エントリを作成した後は、必要なビット長を DWORD 値を変更します。 構成しなかった場合、既定値は 0x4000 バイトになります。 

最大クライアント認証がある場合、TLS サーバーが受け入れる断片化の TLS ハンドシェイク メッセージのサイズを指定するには、作成、**MessageLimitServerClientAuth**エントリ。 エントリを作成した後は、必要なビット長を DWORD 値を変更します。 構成しなかった場合、既定値は 0x8000 バイトになります。 

## <a name="sendtrustedissuerlist"></a>SendTrustedIssuerList

このエントリは、信頼された発行者の一覧が送信されるときに使用されるフラグを制御します。 数百台のクライアント認証用の証明機関を信頼するサーバーの場合が多すぎる発行者、サーバーに送信できるようにするのにはすべてのクライアント認証を要求するときに、クライアント コンピューターにします。 このような場合は、このレジストリ キーを設定することができますと部分的な一覧を送信するには、代わりに、Schannel SSP はしないリストで、クライアントに送信します。

信頼された発行者の一覧を送信しないクライアント証明書が要求されたときに送信するクライアントに影響可能性があります。 たとえば、Internet Explorer では、クライアントの認証要求を受信したときにのみが表示されます、サーバーによって送信される証明機関のいずれかにチェーンでつながっているクライアント証明書。 サーバーでは、一覧を送信しなかった場合は、Internet Explorer では、すべてのクライアントにインストールされているクライアント証明書が表示されます。 

この動作は、望ましい可能性があります。 たとえば、PKI 環境にクロス証明書が含まれている場合、クライアントとサーバー証明書はありません、同じルート CA です。そのため、Internet Explorer では、最大いずれかのサーバーの Ca にチェーンされている証明書を選択できません。 信頼された発行者の一覧を送信しないようにサーバーを構成すると、Internet Explorer は、すべての証明書を送信します。

既定では、このエントリはレジストリに存在しません。

既定の信頼された発行者の一覧を送信する動作

| Windows のバージョン | 時間 |
|-----------------|------|
| Windows Server 2012 および Windows 8 以降 | FALSE |
| Windows Server 2008 R2 および Windows 7 およびそれ以前 | 場合は TRUE。 |

適用可能なバージョン: で指定されていると、**適用先**このトピックの冒頭にあるリスト。

レジストリ パス: HKLM system \currentcontrolset\control\securityproviders\schannel

## <a name="servercachetime"></a>ServerCacheTime

このエントリは、オペレーティング システムのサーバー側キャッシュ エントリが期限切れに必要な時間をミリ秒単位で時間数を制御します。 値 0 は、サーバー側のセッション キャッシュを無効にし、再接続できなくなります。 増やす ServerCacheTime、既定値によって Lsass.exe が消費するメモリを追加します。 通常、各セッション キャッシュ要素には、2 ~ 4 KB のメモリーが必要です。 既定では、このエントリはレジストリに存在しません。 

適用可能なバージョン: で指定されていると、**適用先**このトピックの冒頭にあるリスト。

レジストリ パス: HKLM system \currentcontrolset\control\securityproviders\schannel

既定のサーバー キャッシュ時間: 10 時間

## <a name="ssl-20"></a>SSL 2.0

このサブキーは、SSL 2.0 の使用を制御します。

SSL 2.0 は、Windows 10 バージョン 1607 および Windows Server 2016 以降は削除されましたおよび現在サポートされていません。
SSL 2.0 の既定の設定を参照してください。[TLS/SSL (Schannel SSP) のプロトコル](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx)します。 

レジストリ パス: HKLM system \currentcontrolset\control\securityproviders\schannel\protocols

SSL 2.0 プロトコルを有効にするには作成、**有効**、該当するサブキー内のエントリ。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後、DWORD 値を 1 に変更します。 プロトコルを無効にするには、DWORD 値を 0 に変更します。

SSL 2.0 サブキーの表

| サブキー | 説明 |
|--------|-------------|
| クライアント | SSL クライアントで SSL 2.0 の使用を制御します。 |
| サーバー | SSL サーバーで SSL 2.0 の使用を制御します。 |
| DisabledByDefault | 既定で SSL 2.0 を無効にするフラグします。 |

## <a name="ssl-30"></a>SSL 3.0

このサブキーは、SSL 3.0 の使用を制御します。

Windows 10 バージョン 1607 および Windows Server 2016 以降では、SSL 3.0 がされた既定で無効にします。 SSL 3.0 を既定の設定を参照してください。[TLS/SSL (Schannel SSP) のプロトコル](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx)します。 

レジストリ パス: HKLM system \currentcontrolset\control\securityproviders\schannel\protocols

SSL 3.0 プロトコルを有効にするには、該当するサブキーに有効エントリを作成します。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後、DWORD 値を 1 に変更します。 プロトコルを無効にするには、DWORD 値を 0 に変更します。

SSL 3.0 サブキーの表

| サブキー | 説明 |
|--------|-------------|
| クライアント | SSL クライアントで SSL 3.0 の使用を制御します。 |
| サーバー | SSL 3.0 の SSL サーバーでの使用を制御します。 |
| DisabledByDefault | 既定では SSL 3.0 を無効にするフラグします。 |

## <a name="tls-10"></a>TLS 1.0

このサブキーは、TLS 1.0 の使用を制御します。

TLS 1.0 の既定の設定を参照してください。を参照してください[TLS/SSL (Schannel SSP) のプロトコル](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx)します。

レジストリ パス: HKLM system \currentcontrolset\control\securityproviders\schannel\protocols

TLS 1.0 プロトコルを無効にするには、作成、**有効**、該当するサブキー内のエントリ。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後、DWORD 値を 0 に変更します。 プロトコルを有効にするには、DWORD 値を 1 に変更します。

TLS 1.0 サブキーの表

| サブキー | 説明 |
|--------|-------------|
| クライアント | TLS クライアントで TLS 1.0 の使用を制御します。 |
| サーバー | TLS サーバーで TLS 1.0 の使用を制御します。 |
| DisabledByDefault | 既定で TLS 1.0 を無効にするフラグします。 |

## <a name="tls-11"></a>TLS 1.1

このサブキーは、TLS 1.1 の使用を制御します。

TLS 1.1 の既定の設定を参照してください。[TLS/SSL (Schannel SSP) のプロトコル](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx)します。

>[!Note] 
>作成する必要がありますを有効にし、Windows Server 2008 R2 を実行しているサーバー上でネゴシエートできる TLS 1.1、**DisabledByDefault**、該当するサブキー (Client、Server) 内のエントリ「0」に設定します。 レジストリ エントリは表示されませんしは既定で「1」に設定します。

レジストリ パス: HKLM system \currentcontrolset\control\securityproviders\schannel\protocols

TLS 1.1 プロトコルを無効にするには、作成、**有効**、該当するサブキー内のエントリ。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後、DWORD 値を 0 に変更します。 プロトコルを有効にするには、DWORD 値を 1 に変更します。

TLS 1.1 サブキーの表

| サブキー | 説明 |
|--------|-------------|
| クライアント | TLS クライアントで TLS 1.1 の使用を制御します。 |
| サーバー | TLS サーバーで TLS 1.1 の使用を制御します。 |
| DisabledByDefault | 既定で TLS 1.1 を無効にするフラグします。 |

## <a name="tls-12"></a>TLS 1.2

このサブキーは、TLS 1.2 の使用を制御します。

TLS 1.2 の既定の設定を参照してください。[TLS/SSL (Schannel SSP) のプロトコル](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx)します。

>[!Note] 
>有効にし、Windows Server 2008 R2 を実行しているサーバー上でネゴシエートできる TLS 1.2 を作成する必要があります、**DisabledByDefault**、該当するサブキー (Client、Server) 内のエントリ「0」に設定します。 レジストリ エントリは表示されませんしは既定で「1」に設定します。

レジストリ パス: HKLM system \currentcontrolset\control\securityproviders\schannel\protocols

TLS 1.2 プロトコルを無効にするには、作成、**有効**、該当するサブキー内のエントリ。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後、DWORD 値を 0 に変更します。 プロトコルを有効にするには、DWORD 値を 1 に変更します。

TLS 1.2 サブキーの表

| サブキー | 説明 |
|--------|-------------|
| クライアント | TLS クライアントで TLS 1.2 の使用を制御します。 |
| サーバー | TLS サーバーで TLS 1.2 の使用を制御します。 |
| DisabledByDefault | TLS 1.2 を既定で無効にするフラグします。 |

## <a name="dtls-10"></a>DTLS 1.0

このサブキーは、DTLS 1.0 の使用を制御します。

DTLS 1.0 の既定の設定を参照してください。[TLS/SSL (Schannel SSP) のプロトコル](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx)します。

レジストリ パス: HKLM system \currentcontrolset\control\securityproviders\schannel\protocols

DTLS 1.0 プロトコルを無効にするには、作成、**有効**、該当するサブキー内のエントリ。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後、DWORD 値を 0 に変更します。 プロトコルを有効にするには、DWORD 値を 1 に変更します。

DTLS 1.0 サブキーの表

| サブキー | 説明 |
|--------|-------------|
| クライアント | DTLS クライアントで DTLS 1.0 の使用を制御します。 |
| サーバー | DTLS 1.0 の DTLS サーバーでの使用を制御します。 |
| DisabledByDefault | 既定で DTLS 1.0 を無効にするフラグします。 |

## <a name="dtls-12"></a>DTLS 1.2

このサブキーは、DTLS 1.2 の使用を制御します。

DTLS 1.2 既定の設定を参照してください。[TLS/SSL (Schannel SSP) のプロトコル](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx)します。

レジストリ パス: HKLM system \currentcontrolset\control\securityproviders\schannel\protocols

DTLS 1.2 プロトコルを無効にするには、作成、**有効**、該当するサブキー内のエントリ。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後、DWORD 値を 0 に変更します。 プロトコルを有効にするには、DWORD 値を 1 に変更します。

DTLS 1.2 サブキーの表

| サブキー | 説明 |
|--------|-------------|
| クライアント | DTLS クライアントで DTLS 1.2 の使用を制御します。 |
| サーバー | DTLS サーバーで DTLS 1.2 の使用を制御します。 |
| DisabledByDefault | DTLS 1.2 を既定で無効にするフラグします。 |

