---
ms.assetid: ddfbbda3-30ca-4537-af12-667efc6f63ff
title: AD FS の追加の認証方法の構成
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/26/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: adb587412d65506c35705c5eaa8dbea8c660d117
ms.sourcegitcommit: 9f955be34c641b58ae8b3000768caa46ad535d43
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2019
ms.locfileid: "68590359"
---
# <a name="configure-additional-authentication-methods-for-ad-fs"></a>AD FS の追加の認証方法の構成

多要素認証 (MFA) を有効にするには、追加の認証方法を少なくとも 1 つ選択する必要があります。 既定では、Windows Server 2012 R2 の Active Directory フェデレーションサービス (AD FS) (AD FS) で、追加の認証方法として証明書認証 (スマートカードベースの認証) を選択できます。

> [!NOTE]
> 証明書の認証を選択した場合は、スマート カードの証明書が安全にプロビジョニングされており、PIN 要件が含まれていることを確認してください。

Microsoft Azure は、クラウドで同様の機能を提供します。 [Microsoft Azure ID ソリューション](http://aka.ms/m2w274)の詳細をご覧ください。<br /><br />Microsoft Azure でのハイブリッド ID ソリューションの作成:<br /> - [Azure Multi-factor Authentication について説明します。](http://aka.ms/ey6o9r)<br /> - [クラウド認証を使用して、単一フォレストのハイブリッド環境の id を管理します。](http://aka.ms/g1jat8)<br /> - [追加の Multi-factor Authentication による機密アプリケーションのリスク管理。](http://aka.ms/kt1bbm)

## <a name="microsoft-and-third-party-additional-authentication-methods"></a>Microsoft とサード パーティによる追加の認証方法
Windows Server 2012 R2 の AD FS で、Microsoft とサードパーティの認証方法を構成して有効にすることもできます。 AD FS にインストールして登録すると、グローバルまたは証明書利用者ごとの認証ポリシーの一部として MFA を適用できます。

以下の一覧は、Windows Server 2012 R2 の AD FS で現在利用できる、Microsoft とサード パーティ プロバイダーの MFA サービスをアルファベット順に示したものです。

|プロバイダー|サービス|詳細情報へのリンク|
|-|-|-| 
|aPersona|Microsoft ADFS SSO の aPersona Adaptive Multi-factor Authentication|[aPersona ASM ADFS アダプター](https://www.apersona.com/adfs)|
|Duo のセキュリティ|AD FS 用の Duo MFA アダプター|[AD FS のための Duo 認証](https://duo.com/docs/adfs)|
|Futurae|AD FS 用の Futurae Authentication Suite|[Futurae 強力な認証](https://futurae.com)|
|Gemalto|Gemalto アイデンティティ & セキュリティ サービス|[http://www.gemalto.com/identity](http://www.gemalto.com/identity)|
|inWebo Technologies|inWebo エンタープライズ認証サービス|[inWebo エンタープライズ認証](http://www.inwebo.com)|
|Login People|AD FS 2012 R2 用 Login People MFA API コネクタ (パブリック ベータ版)|[https://www.loginpeople.com](https://www.loginpeople.com)|
|Microsoft|Microsoft Azure MFA|[チュートリアル ガイド: 追加の多要素認証による個人情報アプリケーションのリスク管理](https://technet.microsoft.com/library/dn280946.aspx) (手順 3 を参照)|
Mideye | ADFS の mideye 認証プロバイダー | [Microsoft Active Directory フェデレーションサービスを使用した2要素認証](https://www.mideye.com/support/administrators/documentation/integration/microsoft-adfs/)|
|Okta | Active Directory フェデレーションサービス (AD FS) 用の okta MFA | [Active Directory フェデレーションサービス (AD FS) 用の okta MFA (ADFS)](https://help.okta.com/en/prod/Content/Topics/integrations/adfs-okta-int.htm)|
|1つの Id| 2fa AD FS の star|[2FA AD FS アダプターを starling にする](https://www.oneidentity.com/products/starling-two-factor-authentication/)|
|1つの Id| Defender AD FS|[Defender AD FS アダプター](https://www.oneidentity.com/products/defender/)|
|Ping Id|AD FS 用の Ping Id MFA アダプター|[AD FS 用の Ping Id MFA アダプター](https://documentation.pingidentity.com/pingid/pingidAdminGuide/index.shtml#pid_c_PingIDforADFSSSO.html)|
|RSA (EMC のセキュリティ部門)|RSA SecurID Authentication Agent for Microsoft Active Directory Federation Services|[Microsoft Active Directory フェデレーションサービス (AD FS) 用 RSA SecurID 認証エージェント](http://www.emc.com/security/rsa-securid/rsa-authentication-agents/microsoft-ad-fs.htm)|
|SafeNet, Inc.|SafeNet Authentication Service (SAS) Agent for AD FS|[SafeNet 認証サービス:AD FS エージェント構成ガイド](http://www.safenet-inc.com/resources/integration-guide/data-protection/Safenet_Authentication_Service/SafeNet_Authentication_Service__AD_FS_Agent_Configuration_Guide/?langtype=1033)|
|SecureMFA|SecureMFA OTP プロバイダー| [ADFS Multi-factor Authentication プロバイダー](https://www.securemfa.com/)|
|Swisscom|Mobile ID 認証サービスおよび署名サービス|[モバイル ID 認証サービス](http://swisscom.ch/mid)|
|Symantec|Symantec Validation and ID Protection Service (VIP)|[Symantec 検証と ID 保護サービス (VIP)](http://www.symantec.com/vip-authentication-service)|
|Trusona|必須 (passwordless MFA) と Executive (重要 + Id 校正)| [Trusona Multi-factor Authentication](https://www.trusona.com/solution-overview/)|


## <a name="custom-authentication-method-for-ad-fs-in-windows-server-2012-r2"></a>Windows Server 2012 R2 での AD FS 用のカスタム認証方法
Windows Server 2012 R2 での AD FS 用に独自のカスタム認証方法を構築するための手順が提供されています。 詳細については、「 [Windows Server 2012 R2 での AD FS 用のカスタム認証方法の構築](https://go.microsoft.com/fwlink/?LinkID=511980)」を参照してください。

## <a name="see-also"></a>関連項目
[追加の多要素認証による個人情報アプリケーションのリスク管理](Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)


