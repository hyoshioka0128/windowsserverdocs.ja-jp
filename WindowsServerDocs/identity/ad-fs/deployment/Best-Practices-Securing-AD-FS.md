---
ms.assetid: b7bf7579-ca53-49e3-a26a-6f9f8690762f
title: AD FS と Web アプリケーションプロキシをセキュリティで保護するためのベストプラクティス
description: このドキュメントでは、Active Directory フェデレーションサービス (AD FS) (AD FS) と Web アプリケーションプロキシのセキュリティで保護された計画と展開のベストプラクティスについて説明します。
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: b96a66c9e28454752fd4999fcfe74cbb15a3ae7d
ms.sourcegitcommit: c5709021aa98abd075d7a8f912d4fd2263db8803
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/18/2020
ms.locfileid: "76265814"
---
# <a name="best-practices-for-securing-active-directory-federation-services"></a>Active Directory フェデレーションサービス (AD FS) をセキュリティで保護するためのベストプラクティス

このドキュメントでは、Active Directory フェデレーションサービス (AD FS) (AD FS) と Web アプリケーションプロキシのセキュリティで保護された計画と展開のベストプラクティスについて説明します。  この情報には、これらのコンポーネントの既定の動作、および特定のユースケースとセキュリティ要件を持つ組織の追加のセキュリティ構成に関する推奨事項に関する情報が含まれています。

このドキュメントは、Windows Server 2012 R2 および Windows Server 2016 (preview) の AD FS および WAP に適用されます。  これらの推奨事項は、インフラストラクチャがオンプレミスネットワークにデプロイされているか、Microsoft Azure などのクラウドでホストされている環境に展開されているかどうかによって使用できます。

## <a name="standard-deployment-topology"></a>標準の展開トポロジ
オンプレミス環境でのデプロイでは、内部企業ネットワーク上の1つ以上の AD FS サーバーで構成される標準の展開トポロジを使用することをお勧めします。また、1つ以上の Web アプリケーションプロキシ (WAP) サーバーを DMZ またはエクストラネットネットワークに配置することをお勧めします。  各レイヤー、AD FS および WAP では、ハードウェアまたはソフトウェアのロードバランサーがサーバーファームの前に配置され、トラフィックルーティングを処理します。  ファイアウォールは、各 (FS および proxy) ファームの前にあるロードバランサーの外部 IP アドレスの前に、必要に応じて配置されます。

![AD FS Standard トポロジ](media/Best-Practices-Securing-AD-FS/adfssec1.png)

>[!NOTE]
> AD FS には、読み取り専用ドメインコントローラーではなく、完全書き込み可能なドメインコントローラーを機能させる必要があります。 計画されたトポロジに読み取り専用ドメインコントローラーが含まれている場合は、読み取り専用ドメインコントローラーを認証に使用できますが、LDAP 要求の処理には書き込み可能なドメインコントローラーへの接続が必要です。

## <a name="ports-required"></a>必要なポート
次の図は、AD FS と WAP の展開のコンポーネント間で有効にする必要があるファイアウォールポートを示しています。  展開に Azure AD/Office 365 が含まれていない場合は、同期の要件を無視できます。

>ポート49443は、ユーザー証明書認証が使用されている場合にのみ必要であることに注意してください。これは Azure AD と Office 365 では省略可能です。

![AD FS Standard トポロジ](media/Best-Practices-Securing-AD-FS/adfssec2.png)

>[!NOTE]
> ポート 808 (Windows Server 2012R2) またはポート 1501 (Windows Server 2016 以降) は、ローカル WCF エンドポイントが構成データをサービスプロセスと Powershell に転送するために使用 AD FS Net.tcp ポートです。 このポートは、Set-adfsproperties | を実行すると表示されます。[NetTcpPort] を選択します。 これは、ファイアウォールで開く必要のないローカルポートですが、ポートスキャンで表示されます。 

### <a name="azure-ad-connect-and-federation-serverswap"></a>Azure AD Connect とフェデレーションサーバー/WAP
この表は、Azure AD Connect サーバーとフェデレーション/WAP サーバー間の通信に必要なポートとプロトコルについて説明しています。  

プロトコル |ポート |説明
--------- | --------- |---------
HTTP|80 (TCP/UDP)|SSL 証明書を検証するための CRL (証明書失効リスト) をダウンロードするために使用されます。
HTTPS|443 (TCP/UDP)|Azure AD と同期するために使用されます。
WinRM|5985| WinRM リスナー

### <a name="wap-and-federation-servers"></a>WAP とフェデレーションサーバー
この表は、フェデレーション サーバーと WAP サーバー間の通信に必要なポートとプロトコルについて説明しています。

プロトコル |ポート |説明
--------- | --------- |---------
HTTPS|443 (TCP/UDP)|認証で使用されます。

### <a name="wap-and-users"></a>WAP とユーザー
この表は、ユーザーと WAP サーバー間の通信に必要なポートとプロトコルについて説明しています。

プロトコル |ポート |説明
--------- | --------- |--------- |
HTTPS|443 (TCP/UDP)|デバイスの認証で使用されます。
TCP|49443 (TCP)|証明書の認証で使用されます。

ハイブリッド展開に必要なポートとプロトコルの詳細については、[こちら](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-ports/)のドキュメントを参照してください。

Azure AD と Office 365 の展開に必要なポートとプロトコルの詳細については、[こちら](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US)のドキュメントを参照してください。

### <a name="endpoints-enabled"></a>有効なエンドポイント

AD FS と WAP がインストールされている場合、フェデレーションサービスとプロキシでは、AD FS エンドポイントの既定のセットが有効になります。  これらの既定値は、最も一般的に必要とされるシナリオに基づいて選択されたものであり、変更する必要はありません。  

### <a name="optional-min-set-of-endpoints-proxy-enabled-for-azure-ad--office-365"></a>OptionalAzure AD/Office 365 に対して有効なエンドポイントプロキシの最小セット
Azure AD と Office 365 のシナリオにのみ AD FS と WAP を展開する組織では、より少ない攻撃対象を実現するために、プロキシで有効になっている AD FS エンドポイントの数をさらに制限することができます。
次に示すのは、これらのシナリオでプロキシで有効にする必要があるエンドポイントの一覧です。

|エンドポイント|目的
|-----|-----
|/adfs/ls|ブラウザーベースの認証フローと現在のバージョン Microsoft Office Azure AD と Office 365 認証にこのエンドポイントを使用します
|/adfs/services/trust/2005/usernamemixed|Office 2013 より前の Office クライアントで Exchange Online を使用する場合は2015更新プログラムを使用します。  その後のクライアントは、パッシブ \adfs\ls エンドポイントを使用します。
|/adfs/services/trust/13/usernamemixed|Office 2013 より前の Office クライアントで Exchange Online を使用する場合は2015更新プログラムを使用します。  その後のクライアントは、パッシブ \adfs\ls エンドポイントを使用します。
|/adfs/oauth2|この1つは、(AAD を通じてではなく) AD FS に直接認証するように構成した最新のアプリ (オンプレミスまたはクラウド) に対して使用されます。
|/adfs/services/trust/mex|Office 2013 より前の Office クライアントで Exchange Online を使用する場合は2015更新プログラムを使用します。  その後のクライアントは、パッシブ \adfs\ls エンドポイントを使用します。
|/adfs/ls/federationmetadata/2007-06/federationmetadata.xml |パッシブフローの要件および AD FS 証明書を確認するために Office 365/Azure AD によって使用されます。


プロキシで AD FS エンドポイントを無効にするには、次の PowerShell コマンドレットを使用します。
    
    PS:\>Set-AdfsEndpoint -TargetAddressPath <address path> -Proxy $false

たとえば次のようになります。
    
    PS:\>Set-AdfsEndpoint -TargetAddressPath /adfs/services/trust/13/certificatemixed -Proxy $false
    

### <a name="extended-protection-for-authentication"></a>認証の拡張保護
認証の拡張保護は、中間 (MITM) 攻撃のマンを軽減する機能であり、既定で AD FS で有効になっています。

#### <a name="to-verify-the-settings-you-can-do-the-following"></a>設定を確認するには、次の操作を行います。
この設定は、以下の PowerShell コマンドレットを使用して確認できます。  
    
   `PS:\>Get-ADFSProperties`

プロパティが `ExtendedProtectionTokenCheck` です。  既定の設定は [許可] です。これにより、機能をサポートしていないブラウザーとの互換性の問題がなくても、セキュリティ上の利点を実現できます。  

### <a name="congestion-control-to-protect-the-federation-service"></a>フェデレーションサービスを保護するための輻輳制御
フェデレーションサービスプロキシ (WAP の一部) は、大量の要求から AD FS サービスを保護するための輻輳制御を提供します。  Web アプリケーションプロキシとフェデレーションサーバーの間の待機時間によって検出されたフェデレーションサーバーが過負荷になっている場合、Web アプリケーションプロキシは外部クライアントの認証要求を拒否します。  この機能は、既定で推奨される待機時間のしきい値レベルで構成されます。

#### <a name="to-verify-the-settings-you-can-do-the-following"></a>設定を確認するには、次の操作を行います。
1.  Web アプリケーション プロキシ コンピューターで、管理者特権のコマンド ウィンドウを起動します。
2.  %WINDIR%\adfs\config. で、ADFS ディレクトリに移動します。
3.  輻輳制御の設定を既定値から '<congestionControl latencyThresholdInMSec="8000" minCongestionWindowSize="64" enabled="true" />' に変更します。
4.  ファイルを保存し、閉じます。
5.  ' Net stop adfssrv ' を実行し、' net start adfssrv ' を実行して、AD FS サービスを再開します。
この機能に関するガイダンスについては、[こちら](https://msdn.microsoft.com/library/azure/dn528859.aspx )を参照してください。

### <a name="standard-http-request-checks-at-the-proxy"></a>プロキシでの標準 HTTP 要求チェック
また、プロキシは、すべてのトラフィックに対して次の標準チェックを実行します。

- FS-P 自体は、短時間の証明書を使用して AD FS するために認証を行います。  Dmz サーバーが侵害された疑いがあるシナリオでは、AD FS が、侵害された可能性のあるプロキシからの受信要求を信頼しなくなるように、"プロキシの信頼を取り消す" ことができます。 プロキシの信頼を取り消すと、各プロキシの独自の証明書が失効し、AD FS サーバーに対する任意の目的に対して正常に認証できなくなります。
- FS-P は、すべての接続を終了し、内部ネットワーク上の AD FS サービスへの新しい HTTP 接続を作成します。 これにより、外部デバイスと AD FS サービスの間にセッションレベルのバッファーが提供されます。 外部デバイスは、AD FS サービスに直接接続することはありません。
- FS-P は、AD FS サービスで必要とされない HTTP ヘッダーをフィルターで除外する HTTP 要求の検証を実行します。

## <a name="recommended-security-configurations"></a>推奨されるセキュリティ構成
すべての AD FS および WAP サーバーが最新の更新プログラムを確実に受信できるようにする AD FS インフラストラクチャにとって最も重要なセキュリティの推奨事項は、AD FS および WAP サーバーをすべてのセキュリティ更新プログラムで最新の状態に保つための手段と、省略可能なオプションを使用できるようにすることです。このページの AD FS の重要な更新プログラムが指定されています。

Azure AD の顧客がインフラストラクチャを監視して最新の状態に保つには、Azure AD Premium の機能である AD FS の Azure AD Connect Health を使用することをお勧めします。  Azure AD Connect Health には、AD FS または WAP コンピューターに AD FS と WAP 専用の重要な更新プログラムのいずれかがない場合にトリガーされるモニターとアラートが含まれます。

AD FS に Azure AD Connect Health をインストールする方法については、[こちら](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-health-agent-install/)を参照してください。

## <a name="additional-security-configurations"></a>追加のセキュリティ構成
次の追加機能をオプションで構成して、既定のデプロイで提供されているものに対して追加の保護を提供することもできます。

### <a name="extranet-soft-lockout-protection-for-accounts"></a>アカウントのエクストラネットの "ソフト" ロックアウト保護
Windows Server 2012 R2 のエクストラネットロックアウト機能を使用すると、AD FS 管理者は、失敗した認証要求の最大許容数 (ExExtranetObservationWindow Etlockoutthreshold) と ' 観測期間の期間 () を設定できます。 認証要求のこの最大数 (ExExtranetObservationWindow Etlockoutthreshold) に到達すると AD FS、設定した期間 () の AD FS に対して、指定されたアカウントの資格情報の認証が試行されなくなります。 この操作により、このアカウントが AD アカウントのロックアウトから保護されます。つまり、このアカウントは、ユーザーの認証に AD FS に依存する企業リソースへのアクセスが失われるのを防ぐことができます。 これらの設定は、AD FS サービスが認証できるすべてのドメインに適用されます。

次の Windows PowerShell コマンドを使用して、AD FS エクストラネットロックアウト (例) を設定できます。 

    PS:\>Set-AdfsProperties -EnableExtranetLockout $true -ExtranetLockoutThreshold 15 -ExtranetObservationWindow ( new-timespan -Minutes 30 )

参考までに、この機能のパブリックドキュメントは[こちら](https://technet.microsoft.com/library/dn486806.aspx )です。 

### <a name="disable-ws-trust-windows-endpoints-on-the-proxy-ie-from-extranet"></a>プロキシの WS-TRUST Windows エンドポイント (エクストラネットから) を無効にします。

WS-TRUST Windows エンドポイント ( */adfs/services/trust/2005/windowstransport*と */adfs/services/trust/13/windowstransport*) は、HTTPS で WIA バインドを使用する、イントラネットに接続するエンドポイントに限定されます。 それらをエクストラネットに公開すると、これらのエンドポイントに対する要求によってロックアウトの保護がバイパスされる可能性があります。 これらのエンドポイントは、次の PowerShell コマンドを使用して AD アカウントのロックアウトを保護するために、プロキシで無効にする (つまり、エクストラネットから無効にする) 必要があります。 プロキシでこれらのエンドポイントを無効にすることによって、エンドユーザーに対する既知の影響はありません。

    PS:\>Set-AdfsEndpoint -TargetAddressPath /adfs/services/trust/2005/windowstransport -Proxy $false
    PS:\>Set-AdfsEndpoint -TargetAddressPath /adfs/services/trust/13/windowstransport -Proxy $false
    
### <a name="differentiate-access-policies-for-intranet-and-extranet-access"></a>イントラネットアクセスとエクストラネットアクセスのアクセスポリシーを区別する
AD FS には、ローカルの企業ネットワークで発信される要求と、プロキシ経由でインターネットから送信される要求のアクセスポリシーを区別する機能があります。  これは、アプリケーションごとに実行することも、グローバルに行うこともできます。  ビジネス価値の高いアプリケーションや、機密情報または個人を特定できる情報を持つアプリケーションの場合は、multi-factor authentication を要求することを検討してください。  これは、AD FS 管理スナップインを使用して行うことができます。  

### <a name="require-multi-factor-authentication-mfa"></a>Multi-factor authentication (MFA) を要求する
AD FS は、プロキシ経由で受信する要求、個々のアプリケーション、および Azure AD/Office 365 とオンプレミスの両方のリソースへの条件付きアクセスに対して、強力な認証 (多要素認証など) を要求するように構成できます。  MFA のサポートされる方法には、Microsoft Azure MFA とサードパーティプロバイダーの両方が含まれます。  ユーザーは、追加情報 (1 回限りのコードを含む SMS テキストなど) を入力するように求められ、AD FS プロバイダー固有のプラグインを使用してアクセスできるようになります。  

サポートされている外部 MFA プロバイダーには、[この](https://technet.microsoft.com/library/dn758113.aspx)ページに記載されているものと HDI グローバルが含まれます。

### <a name="hardware-security-module-hsm"></a>ハードウェア セキュリティ モジュール (HSM)
既定の構成では、トークンの署名に使用 AD FS キーは、イントラネット上のフェデレーションサーバーを離れることはありません。  これらは、DMZ またはプロキシコンピューターには存在しません。  必要に応じて、追加の保護を提供するために、AD FS にアタッチされたハードウェアセキュリティモジュールでこれらのキーを保護することができます。  Microsoft は HSM 製品を生成しませんが、AD FS をサポートするいくつかの市場があります。  この推奨事項を実装するには、ベンダーのガイダンスに従って署名と暗号化のための X509 証明書を作成し、AD FS インストール powershell コマンドレットを使用して、次のようにカスタム証明書を指定します。

    PS:\>Install-AdfsFarm -CertificateThumbprint <String> -DecryptionCertificateThumbprint <String> -FederationServiceName <String> -ServiceAccountCredential <PSCredential> -SigningCertificateThumbprint <String>

この場合


- SSL 証明書を `CertificateThumbprint`
- `SigningCertificateThumbprint` は、(HSM で保護されたキーを持つ) 署名証明書です。
- `DecryptionCertificateThumbprint` は暗号化証明書 (HSM で保護されたキーを含む) です。



