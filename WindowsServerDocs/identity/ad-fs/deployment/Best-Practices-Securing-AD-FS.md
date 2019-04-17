---
ms.assetid: b7bf7579-ca53-49e3-a26a-6f9f8690762f
title: "AD FS と Web アプリケーション プロキシをセキュリティで保護するためのベスト プラクティス"
description: "このドキュメントでは、セキュリティで保護の計画と Active Directory フェデレーション サービス (AD FS) と Web アプリケーション プロキシの展開のベスト プラクティスを提供します。"
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 6026246228b22fdea6001528ab7621a1704f1983
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
## <a name="best-practices-for-securing-active-directory-federation-services"></a>Active Directory フェデレーション サービスをセキュリティで保護するためのベスト プラクティス

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このドキュメントでは、セキュリティで保護の計画と Active Directory フェデレーション サービス (AD FS) と Web アプリケーション プロキシの展開のベスト プラクティスを提供します。  これらのコンポーネントと特定のユース ケースとセキュリティ要件を持つ組織に追加のセキュリティ構成に関する推奨事項の既定の動作に関する情報が含まれています。

このドキュメントは、AD FS と WAP で Windows Server 2012 R2 および Windows Server 2016 (プレビュー) に適用されます。  これらの推奨事項は、オンプレミス ネットワークの上または Microsoft Azure などのホスト型クラウド環境に、インフラストラクチャが配置されているかどうかに使用できます。

## <a name="standard-deployment-topology"></a>標準の展開トポロジ
展開については、オンプレミス環境では、境界ネットワークまたはエクストラネットのネットワーク内の 1 つまたは複数の Web アプリケーション プロキシ (WAP) サーバーとは、1 つまたは複数、企業内部ネットワークで AD FS サーバーで構成される標準の展開トポロジお勧めします。  AD FS と WAP、各レイヤーでは、ハードウェアまたはソフトウェア ロード バランサーは、サーバー ファームの前に配置し、トラフィックをルーティングを処理します。  ファイアウォールは、各 (FS およびプロキシ) ファームの前に、ロード バランサーの外部 IP アドレスの前面には必要に応じて、配置されます。

![AD FS の標準のトポロジ](media/Best-Practices-Securing-AD-FS/adfssec1.png)

## <a name="ports-required"></a>必要なポート
以下の図は、ファイアウォールのポートおよび AD FS と WAP 展開のコンポーネント間での間で有効にする必要がありますを示しています。  展開が Azure AD を含めない場合]、[Office 365、同期要件を無視することができます。

>ポート 49443 はのみに必要なかどうかはユーザー証明書認証を使用する Azure AD のオプションは、Office 365 します。

![AD FS の標準のトポロジ](media/Best-Practices-Securing-AD-FS/adfssec2.png)

### <a name="azure-ad-connect-and-federation-serverswap"></a>Azure AD Connect と WAP/フェデレーション サーバー
次の表は、ポートと Azure AD Connect サーバーとフェデレーション/WAP サーバー間の通信に必要なプロトコルについて説明します。  

プロトコル |ポート |説明
--------- | --------- |---------
HTTP|80 (TCP または UDP)|(証明書失効リスト) SSL 証明書を確認する Crl のダウンロードに使用します。
HTTPS|443(TCP/UDP)|Azure AD と同期するために使用します。
WinRM|5985| WinRM リスナ

### <a name="wap-and-federation-servers"></a>WAP サーバーとフェデレーション サーバー
次の表は、ポートと、フェデレーション サーバーと WAP サーバー間の通信に必要なプロトコルについて説明します。

プロトコル |ポート |説明
--------- | --------- |---------
HTTPS|443(TCP/UDP)|認証に使用します。

### <a name="wap-and-users"></a>WAP とユーザー
次の表は、ポートとプロトコルのユーザーと WAP サーバー間の通信に必要なについて説明します。

プロトコル |ポート |説明
--------- | --------- |--------- |
HTTPS|443(TCP/UDP)|デバイスの認証に使用します。
TCP|49443 (TCP)|証明書の認証に使用されます。

詳細については、必要なポートとプロトコルのドキュメントを参照するハイブリッド展開に必要な[ここ](https://azure.microsoft.com/en-us/documentation/articles/active-directory-aadconnect-ports/)します。

詳細については、ポートと Azure AD に必要なプロトコルと Office 365 の展開、ドキュメントを参照してください[ここ](https://support.office.com/en-us/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US)します。

### <a name="endpoints-enabled"></a>エンドポイントが有効になっています。

AD FS と WAP がインストールされているときに、フェデレーション サービスとプロキシに AD FS エンドポイントの既定のセットが有効になります。  これらの既定値が最もよく使用される必要な使用シナリオに基づいて選ばれ、それらを変更する必要はありません。  

### <a name="optional-min-set-of-endpoints-proxy-enabled-for-azure-ad--office-365"></a>[オプション]Azure AD を有効になっているエンドポイントのプロキシの最小セット/Office 365
組織の Azure AD のみの AD FS と WAP を展開する Office 365 のシナリオを制限したり、さらより最小限の攻撃対象領域を実現するために、プロキシで有効になっている AD FS エンドポイントの数。
これらのシナリオでプロキシで有効にする必要がありますエンドポイントの一覧を次に示します。

|エンドポイント|目的
|-----|-----
|adfs/ls|ブラウザー ベースの認証フローと、Microsoft Office の現在のバージョンがこのエンドポイントを使用して Azure AD 用と Office 365 の認証
|/adfs/services/trust/2005/usernamemixed|Office 2013 May 2015 の更新プログラムよりも古い Office クライアントと Exchange Online のために使用します。  それ以降のクライアントは、パッシブ \adfs\ls エンドポイントを使用します。
|/adfs/services/trust/13/usernamemixed|Office 2013 May 2015 の更新プログラムよりも古い Office クライアントと Exchange Online のために使用します。  それ以降のクライアントは、パッシブ \adfs\ls エンドポイントを使用します。
|adfs/oauth2|この 1 つの使用 (オンプレミスまたはクラウド内) の最新のアプリのように構成した (AAD) 経由ではない AD FS に直接認証
|/adfs/services/trust/mex|Office 2013 May 2015 の更新プログラムよりも古い Office クライアントと Exchange Online のために使用します。  それ以降のクライアントは、パッシブ \adfs\ls エンドポイントを使用します。
|/adfs/ls/federationmetadata/2007-06/federationmetadata.xml |パッシブ フロー; ための要件Office を AD FS 証明書を確認する] 365、Azure AD で使用され、


次の PowerShell コマンドレットを使用して、プロキシでは、AD FS エンドポイントを無効にすることができます。
    
    PS:\>Set-AdfsEndpoint -TargetAddressPath <address path> -Proxy $false

例えば：
    
    PS:\>Set-AdfsEndpoint -TargetAddressPath /adfs/services/trust/13/certificatemixed -Proxy $false
    

### <a name="extended-protection-for-authentication"></a>認証に対する保護の強化
認証の拡張保護は、中央の (MITM) 攻撃を軽減して、AD FS では既定で有効になっている機能です。

#### <a name="to-verify-the-settings-you-can-do-the-following"></a>設定を確認するには、次の操作を行うことができます。
使って、設定を確認することができます、PowerShell コマンドレットの下。  
    
   `PS:\>Get-ADFSProperties`

プロパティは`ExtendedProtectionTokenCheck`します。  既定の設定ができるようにする、互換性の問題、機能をサポートしていないブラウザーとせず、セキュリティ上のメリットを実現できます。  

### <a name="congestion-control-to-protect-the-federation-service"></a>輻輳制御、フェデレーション サービスを保護するには
フェデレーション サービス プロキシ (WAP の一部) は、大量の要求から AD FS サービスを保護する輻輳制御を提供します。  フェデレーション サーバーが過負荷の状態と Web アプリケーション プロキシとフェデレーション サーバーの間の待機時間によって検出された場合、Web アプリケーション プロキシは外部クライアントの認証要求を拒否します。  この機能は既定では推奨される待機時間のしきい値のレベルを構成します。

#### <a name="to-verify-the-settings-you-can-do-the-following"></a>設定を確認するには、次の操作を行うことができます。
1.  Web アプリケーション プロキシ コンピューターには、管理者特権のコマンド ウィンドウを開始します。
2.  %Windir%\adfs\config、ADFS ディレクトリに移動します。
3.  輻輳制御設定を変更するには、その既定値から '<congestionControl latencyThresholdInMSec="8000" minCongestionWindowSize="64" enabled="true" />' です。
4.  保存して、ファイルを閉じます。
5.  AD FS サービスを再起動するには、'net stop adfssrv' し、'net start adfssrv' を実行しています。
リファレンスについては、この機能に関するガイダンスを参照して[ここ](https://msdn.microsoft.com/en-us/library/azure/dn528859.aspx )します。

### <a name="standard-http-request-checks-at-the-proxy"></a>プロキシで標準の HTTP 要求を確認します。
プロキシには、すべてのトラフィックに対して次の標準的なチェックも実行します。

- FS-p 自体が短い証明書を使って AD FS を認証します。  境界ネットワーク サーバーのセキュリティ侵害疑いのシナリオで取り消すことができます"プロキシ信頼"不要になったを信頼するようにからの入力方向の要求可能性のある AD FS には、プロキシが侵害された場合。 任意の目的で、AD FS サーバーの認証が成功にできるように、各プロキシの証明書を失効プロキシ信頼を取り消す
- FS P では、すべての接続を終了し、内部ネットワーク上の AD FS サービスへの新しい HTTP 接続を作成します。 これは、外部デバイスと AD FS サービスの間でセッション レベルのバッファーを提供します。 外部デバイスは、AD FS サービスに直接接続ことはありません。
- FS P は、AD FS サービスが必要としない HTTP ヘッダーを具体的にはフィルター処理する HTTP 要求の検証を実行します。

## <a name="recommended-security-configurations"></a>推奨されるセキュリティ構成
すべての AD FS を確認し、WAP サーバーは、AD FS インフラストラクチャの最も重要なセキュリティに関する推奨事項は、AD FS と WAP サーバー現在、このページで、AD FS の重要なとして指定されたそのオプションの更新プログラムと同様に、すべてのセキュリティ更新プログラムを保持するインプレースのための手段があることを確認する、最新の更新プログラムを受信します。

経由での Azure AD 接続のヘルスを AD FS では、Azure AD Premium の機能は、インフラストラクチャを監視し、最新の状態を Azure AD のお客様に対して推奨される方法です。  Azure AD 接続のヘルスには、モニタおよびアラートの場合は、AD FS または WAP コンピューターに存在しない重要な更新プログラムのいずれか専用の AD FS と WAP をトリガーするが含まれます。

AD FS はありますの Azure AD 接続の正常性のインストールについて[ここ](https://azure.microsoft.com/en-us/documentation/articles/active-directory-aadconnect-health-agent-install/)します。

## <a name="additional-security-configurations"></a>追加のセキュリティ構成
次の追加機能は、既定の展開で提供される追加の保護を提供するオプションで構成できます。

### <a name="extranet-soft-lockout-protection-for-accounts"></a>アカウントの保護を「ソフト」のエクストラネット ロックアウト
エクストラネット ロックアウト機能を使用して Windows Server 2012 R2 で AD FS 管理者が、許可された最大数の障害が発生した認証要求 (ExtranetLockoutThreshold) を設定できますと ' 監視ウィンドウの期間 (ExtranetObservationWindow)。 認証要求のこの最大数 (ExtranetLockoutThreshold) に達すると、所定の時間 (ExtranetObservationWindow) の AD FS に対して指定したアカウントの資格情報を認証しようとしています。AD FS が停止します。 つまり、AD FS のユーザーの認証に依存している企業のリソースにアクセスできなくなるからこのアカウントを保護、この操作は、AD アカウントのロックアウトからこのアカウントを保護します。 これらの設定は、AD FS サービスを認証できるすべてのドメインに適用されます。

AD FS のエクストラネット ロックアウト (例) を設定するのには、次の Windows PowerShell コマンドを使用できます。 

    PS:\>Set-AdfsProperties -EnableExtranetLockout $true -ExtranetLockoutThreshold 15 -ExtranetObservationWindow ( new-timespan -Minutes 30 )

この機能のパブリックのドキュメントは、リファレンスについては、[ここ](https://technet.microsoft.com/en-us/library/dn486806.aspx )します。 

### <a name="differentiate-access-policies-for-intranet-and-extranet-access"></a>イントラネットとエクストラネット アクセス用のアクセス ポリシーを区別するため
AD FS では、プロキシ経由でインターネット付属しているローカルの企業ネットワーク vs 要求である要求のアクセス ポリシーを区別するために権限を持ちます。  これは、1 つのアプリケーションまたはグローバルに実行できます。  ビジネスに大きな値アプリケーションまたは機密情報や個人を特定できる情報を持つアプリケーションは、多要素認証を必要とする検討してください。  これは、AD FS 管理スナップインを使用して実行できます。  

### <a name="require-multi-factor-authentication-mfa"></a>多要素認証 (MFA) が必要
AD FS は、プロキシ経由で受信中の要求を具体的には、個々 のアプリケーション、および両方の Azure AD に条件付きアクセス (多要素認証) などの強力な認証を必要とするように構成できる/Office 365 と社内リソースにします。  MFA のサポートされている方法には、Microsoft Azure MFA とサード パーティ製の両方のプロバイダーが含まれます。  追加の情報を提供するよう求められます (など、1 つが含まれている、SMS テキスト メッセージによる時刻のコード)、AD FS のアクセスを許可するようにプラグインのプロバイダー固有の動作とします。  

サポートされている外部 MFA プロバイダーを含めるに記載されている[この](https://technet.microsoft.com/en-us/library/dn758113.aspx)] ページで、だけでなく HDI グローバルします。

### <a name="hardware-security-module-hsm"></a>ハードウェア セキュリティ モジュール (HSM)
既定の構成で決してトークンに署名するキー AD FS の使用は、イントラネット上のフェデレーション サーバーでままにします。  DMZ のまたはプロキシ マシン上に存在することはありません。  必要に応じて追加の保護を提供するには、これらのキーを AD FS に接続されているハードウェア セキュリティ モジュールで保護できます。  Microsoft は、HSM の製品を生成しない、ただしは、複数の AD FS をサポートする市場します。  この推奨事項を実装するために、X509 を作成するベンダーのガイダンスに従う署名と暗号化、証明書は、カスタム証明書を指定する次のように、AD FS インストール powershell コマンドレットを使用します。

    PS:\>Install-AdfsFarm -CertificateThumbprint <String> -DecryptionCertificateThumbprint <String> -FederationServiceName <String> -ServiceAccountCredential <PSCredential> -SigningCertificateThumbprint <String>

どこ：


- `CertificateThumbprint` SSL 証明書は、します。
- `SigningCertificateThumbprint` 保護された HSM キーの署名証明書は、します。
- `DecryptionCertificateThumbprint` 保護された HSM キーの暗号化の証明書は、します。



