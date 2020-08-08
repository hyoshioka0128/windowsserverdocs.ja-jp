---
ms.assetid: ddfbbda3-30ca-4537-af12-667efc6f63ff
title: AD FS の追加の認証方法の構成
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/26/2019
ms.topic: article
ms.openlocfilehash: 66ef77b46065b87e6df08c63b0fb40ca4453c45b
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954258"
---
# <a name="configure-additional-authentication-methods-for-ad-fs"></a>AD FS の追加の認証方法の構成

多要素認証 (MFA) を有効にするには、追加の認証方法を少なくとも 1 つ選択する必要があります。 既定では、Windows Server 2012 R2 の Active Directory フェデレーションサービス (AD FS) (AD FS) で、追加の認証方法として証明書認証 (スマートカードベースの認証) を選択できます。

> [!NOTE]
> 証明書の認証を選択した場合は、スマート カードの証明書が安全にプロビジョニングされており、PIN 要件が含まれていることを確認してください。

Microsoft Azure は、クラウドで同様の機能を提供します。 [Microsoft Azure ID ソリューション](https://aka.ms/m2w274)の詳細をご覧ください。<p>Microsoft Azure でのハイブリッド ID ソリューションの作成:<br /> - [Azure Multi-Factor Authentication について説明します。](https://aka.ms/ey6o9r)<br /> - [クラウド認証を使用して、単一フォレストのハイブリッド環境の id を管理します。](https://aka.ms/g1jat8)<br /> - [機密アプリケーションの追加 Multi-Factor Authentication によってリスクを管理します。](https://aka.ms/kt1bbm)

## <a name="microsoft-and-third-party-additional-authentication-methods"></a>Microsoft とサード パーティによる追加の認証方法
Windows Server 2012 R2 の AD FS で、Microsoft とサードパーティの認証方法を構成して有効にすることもできます。 AD FS にインストールして登録すると、グローバルまたは証明書利用者ごとの認証ポリシーの一部として MFA を適用できます。

以下の一覧は、Windows Server 2012 R2 の AD FS で現在利用できる、Microsoft とサード パーティ プロバイダーの MFA サービスをアルファベット順に示したものです。

|プロバイダー|サービス|詳細情報へのリンク|
|-|-|-|
|aPersona|Microsoft ADFS SSO の aPersona Adaptive Multi-Factor Authentication|[aPersona ASM ADFS アダプター](https://www.apersona.com/adfs)|
|Cyphercor Inc.|AD FS の LoginTC Multi-Factor Authentication|[LoginTC AD FS コネクタ](https://www.logintc.com/docs/connectors/adfs.html)|
|Duo Security|AD FS 用の Duo MFA アダプター|[AD FS のための Duo 認証](https://duo.com/docs/adfs)|
|Futurae|AD FS 用の Futurae Authentication Suite|[Futurae 強力な認証](https://futurae.com)|
|Gemalto|Gemalto アイデンティティ & セキュリティ サービス|[http://www.gemalto.com/identity](http://www.gemalto.com/identity)|
|inWebo Technologies|inWebo エンタープライズ認証サービス|[inWebo エンタープライズ認証](http://www.inwebo.com)|
|Login People|AD FS 2012 R2 用 Login People MFA API コネクタ (パブリック ベータ版)|[https://www.loginpeople.com](https://www.loginpeople.com)|
|Microsoft|Microsoft Azure MFA|[チュートリアル ガイド: 追加の多要素認証による個人情報アプリケーションのリスク管理](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn280946(v=ws.11)) (手順 3 を参照)|
Mideye | ADFS の mideye 認証プロバイダー | [Microsoft Active Directory フェデレーションサービスを使用した2要素認証](https://www.mideye.com/support/administrators/documentation/integration/microsoft-adfs/)|
|Okta | Active Directory フェデレーションサービス (AD FS) 用の okta MFA | [Active Directory フェデレーションサービス (AD FS) 用の okta MFA (ADFS)](https://help.okta.com/en/prod/Content/Topics/integrations/adfs-okta-int.htm)|
|One Identity| 2fa AD FS の star|[2FA AD FS アダプターを starling にする](https://www.oneidentity.com/products/starling-two-factor-authentication/)|
|One Identity| Defender AD FS|[Defender AD FS アダプター](https://www.oneidentity.com/products/defender/)|
|Ping Identity|AD FS 用の Ping Id MFA アダプター|[AD FS 用の Ping Id MFA アダプター](https://documentation.pingidentity.com/pingid/pingidAdminGuide/index.shtml#pid_c_PingIDforADFSSSO.html)|
|RSA (EMC のセキュリティ部門)|RSA SecurID Authentication Agent for Microsoft Active Directory Federation Services|[RSA SecurID Authentication Agent for Microsoft Active Directory Federation Services](http://www.emc.com/security/rsa-securid/rsa-authentication-agents/microsoft-ad-fs.htm)|
|SafeNet, Inc.|SafeNet Authentication Service (SAS) Agent for AD FS|[SafeNet Authentication Service: AD FS Agent Configuration Guide (SafeNet Authentication Service: AD FS エージェント構成ガイド)](http://www.safenet-inc.com/resources/integration-guide/data-protection/Safenet_Authentication_Service/SafeNet_Authentication_Service__AD_FS_Agent_Configuration_Guide/?langtype=1033)|
|SecureMFA|SecureMFA OTP プロバイダー| [ADFS Multi-factor Authentication プロバイダー](https://www.securemfa.com/)|
|Swisscom|Mobile ID 認証サービスおよび署名サービス|[Mobile ID 認証サービス](http://swisscom.ch/mid)|
|Symantec|Symantec Validation and ID Protection Service (VIP)|[Symantec Validation and ID Protection Service (VIP)](http://www.symantec.com/vip-authentication-service)|
|Trusona|必須 (passwordless MFA) と Executive (重要 + Id 校正)| [Trusona Multi-factor Authentication](https://www.trusona.com/solution-overview/)|


## <a name="custom-authentication-method-for-ad-fs-in-windows-server-2012-r2"></a>Windows Server 2012 R2 での AD FS 用のカスタム認証方法
Windows Server 2012 R2 での AD FS 用に独自のカスタム認証方法を構築するための手順が提供されています。 詳細については、「 [Windows Server 2012 R2 での AD FS 用のカスタム認証方法の構築](https://go.microsoft.com/fwlink/?LinkID=511980)」を参照してください。

## <a name="see-also"></a>参照
[追加の多要素認証による個人情報アプリケーションのリスク管理](Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)
