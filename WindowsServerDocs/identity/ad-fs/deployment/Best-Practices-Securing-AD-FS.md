---
ms.assetid: b7bf7579-ca53-49e3-a26a-6f9f8690762f
title: AD FS と Web アプリケーション プロキシをセキュリティで保護するためのベスト プラクティス
description: このドキュメントでは、セキュリティで保護の計画と Active Directory フェデレーション サービス (AD FS) と Web アプリケーション プロキシの展開のベスト プラクティスを提供します。
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3cc4194b562dad17d0c2021f4aaf061114e2c94b
ms.sourcegitcommit: 9bece8049b1766bd9bb0d5eb5921413a2de2ca61
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67351297"
---
## <a name="best-practices-for-securing-active-directory-federation-services"></a>Active Directory フェデレーション サービスをセキュリティで保護するためのベスト プラクティス


このドキュメントでは、セキュリティで保護の計画と Active Directory フェデレーション サービス (AD FS) と Web アプリケーション プロキシの展開のベスト プラクティスを提供します。  これらのコンポーネントと組織の特定のユース ケースとセキュリティ要件には追加のセキュリティ構成に関する推奨事項の既定の動作に関する情報が含まれています。

このドキュメントは、AD FS と WAP で Windows Server 2012 R2 および Windows Server 2016 (プレビュー) に適用されます。  オンプレミス ネットワークまたは Microsoft Azure などのホスト型クラウド環境に、インフラストラクチャが配置されているかどうか、これらの推奨事項を使用できます。

## <a name="standard-deployment-topology"></a>標準の展開トポロジ
オンプレミスの環境で展開、DMZ またはエクストラネットのネットワーク内の 1 つまたは複数の Web アプリケーション プロキシ (WAP) サーバーでは、1 つ以上、企業内部ネットワークの AD FS サーバーで構成される標準の展開トポロジはお勧めします。  AD FS と WAP では、各レイヤーでは、ハードウェアまたはソフトウェア ロード バランサーは、サーバー ファームの前に配置し、トラフィック ルーティングを処理します。  ファイアウォールは、各 (FS とプロキシ) ファームの前に、ロード バランサーの外部 IP アドレスの前に必要に応じて配置されます。

![AD FS の標準のトポロジ](media/Best-Practices-Securing-AD-FS/adfssec1.png)

## <a name="ports-required"></a>必要なポート
以下の図は、ファイアウォールのポート間と AD FS と WAP のデプロイのコンポーネント間で有効にする必要がありますを示しています。  Azure AD が、展開に含まれていない場合]、[Office 365、同期の要件を無視できます。

>ポート 49443 はのみに必要なユーザー証明書認証を使用されるかどうかは Azure AD の省略可能と Office 365 です。

![AD FS の標準のトポロジ](media/Best-Practices-Securing-AD-FS/adfssec2.png)

>[!NOTE]
> ポート 808 (Windows Server 2012R2) またはポート 1501 (Windows Server 2016 以降) は、Powershell およびサービスのプロセス構成データを転送するローカルの WCF エンドポイントの Net.TCP ポート AD FS を使用します。 このポートを表示するには Get-adfsproperties を実行しているを |NetTcpPort を選択します。 これはローカルのポートをファイアウォールで開く必要はありませんが、ポート スキャンが表示されます。 

### <a name="azure-ad-connect-and-federation-serverswap"></a>Azure AD Connect とフェデレーション サーバー/WAP
このテーブルは、ポートと、Azure AD Connect サーバーとフェデレーション/WAP サーバー間の通信に必要なプロトコルについて説明します。  

プロトコル |ポート |説明
--------- | --------- |---------
HTTP|80 (TCP または UDP)|(証明書失効リスト) の SSL 証明書を確認する Crl をダウンロードするために使用します。
HTTPS|443(TCP/UDP)|Azure AD と同期するために使用します。
WinRM|5985| WinRM リスナー

### <a name="wap-and-federation-servers"></a>WAP とフェデレーション サーバー
このテーブルは、ポートとのフェデレーション サーバーと WAP サーバー間の通信に必要なプロトコルについて説明します。

プロトコル |ポート |説明
--------- | --------- |---------
HTTPS|443(TCP/UDP)|認証に使用します。

### <a name="wap-and-users"></a>WAP とユーザー
このテーブルは、ポートとユーザーと WAP サーバー間の通信に必要なプロトコルについて説明します。

プロトコル |ポート |説明
--------- | --------- |--------- |
HTTPS|443(TCP/UDP)|デバイスの認証に使用します。
TCP|49443 (TCP)|証明書の認証に使用されます。

必要なポートとのハイブリッド展開は、ドキュメントを参照してください。 必要なプロトコルの詳細については[ここ](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-ports/)します。

詳細については、ポートと、Azure AD に必要なプロトコルと Office 365 デプロイのドキュメントを参照してください[ここ](https://support.office.com/en-us/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US)。

### <a name="endpoints-enabled"></a>エンドポイントが有効になっています。

AD FS と WAP をインストールすると、プロキシとフェデレーション サービスで AD FS エンドポイントの既定のセットが有効にします。  これらの既定値が、特に一般的な必要な使用シナリオに応じて、選択し、それらを変更する必要はありません。  

### <a name="optional-min-set-of-endpoints-proxy-enabled-for-azure-ad--office-365"></a>[省略可能]Azure AD を有効になっているエンドポイント プロキシの最小セットまたは Office 365
組織が Azure AD に対してのみ、AD FS と WAP を展開し、Office 365 のシナリオが、さらに低く攻撃対象領域を実現するために、プロキシを有効になっている AD FS エンドポイントの数で制限できます。
これらのシナリオで、プロキシで有効にする必要がありますエンドポイントの一覧を次に示します。

|エンドポイント|目的
|-----|-----
|/adfs/ls|ブラウザー ベースの認証フローと、このエンドポイントを使用して、Azure AD の現在のバージョンの Microsoft Office と Office 365 認証
|/adfs/services/trust/2005/usernamemixed|Office 2013 の 2015 年 5 月の更新プログラムよりも古い Office クライアントでは、Exchange Online の使用。  それ以降のクライアントは、パッシブ \adfs\ls エンドポイントを使用します。
|/adfs/services/trust/13/usernamemixed|Office 2013 の 2015 年 5 月の更新プログラムよりも古い Office クライアントでは、Exchange Online の使用。  それ以降のクライアントは、パッシブ \adfs\ls エンドポイントを使用します。
|/adfs/oauth2|この 1 つが使用されます (オンプレミスまたはクラウド内) の最新のアプリの (AAD) 経由ではなく、AD FS から直接認証を構成します。
|/adfs/services/trust/mex|Office 2013 の 2015 年 5 月の更新プログラムよりも古い Office クライアントでは、Exchange Online の使用。  それ以降のクライアントは、パッシブ \adfs\ls エンドポイントを使用します。
|/adfs/ls/federationmetadata/2007-06/federationmetadata.xml |任意のパッシブなフローの要件Office 365/Azure の AD FS 証明書を確認する AD で使用され、


次の PowerShell コマンドレットを使用して、プロキシでは、AD FS のエンドポイントを無効にすることができます。
    
    PS:\>Set-AdfsEndpoint -TargetAddressPath <address path> -Proxy $false

例:
    
    PS:\>Set-AdfsEndpoint -TargetAddressPath /adfs/services/trust/13/certificatemixed -Proxy $false
    

### <a name="extended-protection-for-authentication"></a>認証の拡張保護
認証の拡張保護は、中間 (MITM) 攻撃を軽減して、既定では、AD FS が有効になっている機能です。

#### <a name="to-verify-the-settings-you-can-do-the-following"></a>設定を確認するには、次の操作を行うことができます。
使用して、設定を検証できる、以下の PowerShell コマンドレット。  
    
   `PS:\>Get-ADFSProperties`

プロパティが`ExtendedProtectionTokenCheck`します。  既定値は、許可するため、セキュリティ上の利点は、機能をサポートしないブラウザーと互換性の問題なく実現できます。  

### <a name="congestion-control-to-protect-the-federation-service"></a>輻輳制御、フェデレーション サービスを保護するには
フェデレーション サービス プロキシ (WAP の一部) は、大量の要求から AD FS サービスを保護する輻輳制御を提供します。  Web アプリケーション プロキシは、Web アプリケーション プロキシとフェデレーション サーバー間の待機時間によって検出されると、フェデレーション サーバーがオーバー ロードの場合、外部クライアントの認証要求が拒否されます。  この機能は、既定では、推奨される待機時間のしきい値のレベルで構成されます。

#### <a name="to-verify-the-settings-you-can-do-the-following"></a>設定を確認するには、次の操作を行うことができます。
1.  Web アプリケーション プロキシ コンピューターに、管理者特権でコマンド ウィンドウを起動します。
2.  %Windir%\adfs\config、ADFS ディレクトリに移動します。
3.  輻輳制御の設定を変更するには、その既定値から '<congestionControl latencyThresholdInMSec="8000" minCongestionWindowSize="64" enabled="true" />'。
4.  ファイルを保存し、閉じます。
5.  'Net stop adfssrv'、'net start adfssrv' を実行して、AD FS サービスを再起動します。
参考までに、この機能に関するガイダンスについては、「[ここ](https://msdn.microsoft.com/library/azure/dn528859.aspx )します。

### <a name="standard-http-request-checks-at-the-proxy"></a>プロキシで標準の HTTP 要求を確認します
プロキシには、すべてのトラフィックに対して、次の標準チェックも実行します。

- FS-P 自体は、短期的な証明書を使用して AD FS を認証します。  Dmz サーバーのセキュリティ侵害を疑いがあるのでは、取り消すことができます"プロキシ信頼"されなくを信頼するように要求からは受信可能性のある AD FS には、プロキシが侵害されました。 AD FS サーバーに目的を問わず正常に認証できないように、各プロキシの証明書を失効プロキシ信頼を取り消す
- FS P は、すべての接続を終了し、内部ネットワーク上の AD FS サービスへの新しい HTTP 接続を作成します。 これは、外部のデバイスと、AD FS サービス間のセッション レベル バッファーを提供します。 外部のデバイスは、AD FS サービスに直接接続されません。
- FS P は、具体的には、AD FS サービスが不要な HTTP ヘッダーを除外する HTTP 要求の検証を実行します。

## <a name="recommended-security-configurations"></a>推奨されるセキュリティ構成
すべての AD FS と WAP サーバーは、AD FS インフラストラクチャの最も重要なセキュリティ推奨事項がすべてのセキュリティ更新プログラムだけでなくこれらのオプションを使用して、AD FS および WAP サーバーを最新にする手段があることを確認するには、最新の更新プログラムを受信することを確認します。更新プログラムのこのページで AD FS の重要なこととして指定します。

監視し、最新の Azure AD のお客様に対して推奨される方法、インフラストラクチャでは、Azure AD Connect Health for AD FS、Azure AD Premium の機能を使用します。  Azure AD Connect Health には、モニターと、AD FS または WAP コンピューターが不足している場合、重要な更新プログラムのいずれか専用の AD FS と WAP をトリガーするアラートが含まれています。

AD FS の Azure AD Connect Health をインストールする方法について[ここ](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-health-agent-install/)します。

## <a name="additional-security-configurations"></a>追加のセキュリティ構成
既定のデプロイで提供されている追加の保護を提供する、次の追加機能を必要に応じて構成できます。

### <a name="extranet-soft-lockout-protection-for-accounts"></a>アカウントの保護を「ソフト」エクストラネットのロックアウト
エクストラネットのロックアウト機能を使用して Windows Server 2012 R2 で AD FS 管理者が失敗した認証要求 (ExtranetLockoutThreshold) の数の上限を設定できます、' 監視ウィンドウの期間 (ExtranetObservationWindow)。 認証要求の最大数 (ExtranetLockoutThreshold) に達すると、特定の期間 (ExtranetObservationWindow) の AD FS に対して指定されたアカウントの資格情報を認証しようとしています。 AD FS を停止します。 つまり、ユーザーの認証用に AD FS に依存している企業リソースへのアクセスを失わずからこのアカウントを保護、この操作は、アカウントのロックアウトが AD からこのアカウントを保護します。 これらの設定は、AD FS サービスを認証できるすべてのドメインに適用されます。

AD FS エクストラネット ロックアウト (例) を設定するのには、次の Windows PowerShell コマンドを使用できます。 

    PS:\>Set-AdfsProperties -EnableExtranetLockout $true -ExtranetLockoutThreshold 15 -ExtranetObservationWindow ( new-timespan -Minutes 30 )

この機能のパブリック ドキュメントは、リファレンスについては、[ここ](https://technet.microsoft.com/library/dn486806.aspx )します。 

### <a name="differentiate-access-policies-for-intranet-and-extranet-access"></a>イントラネットとエクストラネット アクセスのアクセス ポリシーを区別します。
AD FS では、プロキシ経由でインターネットから到着したローカルの企業ネットワーク vs 要求で送信される要求のアクセス ポリシーを区別するために権限を持ちます。  これは、アプリケーションごと、またはグローバルに実行できます。  ビジネスに大きな値のアプリケーションや機密情報や個人を特定できる情報とアプリケーションの場合は、多要素認証を必要とする検討してください。  これは、AD FS 管理スナップインを使用して実行できます。  

### <a name="require-multi-factor-authentication-mfa"></a>多要素認証 (MFA) が必要です。
AD FS は、具体的には、プロキシ経由送信される要求を個々 のアプリケーション、および両方の Azure AD への条件付きアクセス (多要素認証) などの強力な認証を必要とするように構成できます/Office 365 とオンプレミスのリソース。  MFA のサポートされている方法には、Microsoft Azure MFA とサード パーティの両方のプロバイダーが含まれます。  ユーザーは追加の情報を提供するように求められます (など、1 つを格納している、SMS テキスト コードを時間) と AD FS がプロバイダー固有のアクセスを許可するプラグインと連携します。  

サポートされている外部の MFA プロバイダーは、記載されている[この](https://technet.microsoft.com/library/dn758113.aspx) ページで、だけでなく HDI グローバルです。

### <a name="hardware-security-module-hsm"></a>ハードウェア セキュリティ モジュール (HSM)
既定の構成でしないトークンの署名に使用する AD FS のキーは、イントラネット上のフェデレーション サーバーままにします。  境界ネットワークまたはプロキシ コンピューター上に存在することはできません。  必要に応じて追加の保護を提供するには、これらのキーを AD FS に接続されている、ハードウェア セキュリティ モジュールで保護できます。  Microsoft には、HSM の製品がなければ、ただしは、いくつか AD FS をサポートする市場にします。  この推奨事項を実装するために、X509 を作成するベンダーのガイダンスに従うの署名と暗号化、証明書が、次のように、カスタムの証明書を指定する、AD FS インストール powershell コマンドレットを使用します。

    PS:\>Install-AdfsFarm -CertificateThumbprint <String> -DecryptionCertificateThumbprint <String> -FederationServiceName <String> -ServiceAccountCredential <PSCredential> -SigningCertificateThumbprint <String>

それぞれの文字の説明は次のとおりです。


- `CertificateThumbprint` SSL 証明書は、します。
- `SigningCertificateThumbprint` HSM で保護されたキーの署名証明書は、します。
- `DecryptionCertificateThumbprint` HSM で保護されたキーの暗号化証明書は、します。



