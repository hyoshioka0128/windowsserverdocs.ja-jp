---
ms.assetid: ddfbbda3-30ca-4537-af12-667efc6f63ff
title: AD FS の追加の認証方法の構成
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 10/04/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 88c4d976b9808d254dc1681ce9eee3ca556824ab
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189793"
---
# <a name="configure-additional-authentication-methods-for-ad-fs"></a>AD FS の追加の認証方法の構成

多要素認証 (MFA) を有効にするには、追加の認証方法を少なくとも 1 つ選択する必要があります。 Windows Server 2012 R2 で Active の Directory フェデレーション サービス (AD FS) で既定に追加の認証方法として証明書認証 (つまり、スマート カード ベースの認証) を選択できます。

> [!NOTE]
> 証明書の認証を選択した場合は、スマート カードの証明書が安全にプロビジョニングされており、PIN 要件が含まれていることを確認してください。

Microsoft Azure は同様の機能をクラウドで実現します。 [Microsoft Azure ID ソリューション](http://aka.ms/m2w274)の詳細をご覧ください。<br /><br />Microsoft Azure でのハイブリッド ID ソリューションの作成:<br /> - [Azure Multi-factor Authentication について説明します。](http://aka.ms/ey6o9r)<br /> - [クラウド認証を使用した単一フォレスト ハイブリッド環境の id を管理します。](http://aka.ms/g1jat8)<br /> - [機密性の高いアプリケーションの追加の多要素認証によるリスクを管理します。](http://aka.ms/kt1bbm)

## <a name="microsoft-and-third-party-additional-authentication-methods"></a>Microsoft とサード パーティによる追加の認証方法
構成し、Microsoft および Windows Server 2012 R2 で AD FS でのサード パーティの認証方法を有効にすることができます。 インストールされている、AD FS に登録されると、グローバルまたはあたり証明書利用者のパーティの認証ポリシーの一部として、MFA を適用できます。

以下の一覧は、Windows Server 2012 R2 の AD FS で現在利用できる、Microsoft とサード パーティ プロバイダーの MFA サービスをアルファベット順に示したものです。

|プロバイダー|サービス|詳細情報へのリンク|
|-|-|-| 
|aPersona|aPersona Microsoft ADFS sso アダプティブの多要素認証|[aPersona ASM ad FS アダプター](https://www.apersona.com/adfs)|
|Duo セキュリティ|AD FS の duo MFA アダプター|[AD FS の認証をコンビ](https://duo.com/docs/adfs)|
|Gemalto|Gemalto アイデンティティ & セキュリティ サービス|[http://www.gemalto.com/identity](http://www.gemalto.com/identity)|
|inWebo Technologies|inWebo エンタープライズ認証サービス|[inWebo Enterprise Authentication](http://www.inwebo.com)|
|Login People|AD FS 2012 R2 用 Login People MFA API コネクタ (パブリック ベータ版)|[https://www.loginpeople.com](https://www.loginpeople.com)|
|Microsoft|Microsoft Azure MFA|[チュートリアル ガイド: 追加の多要素認証による個人情報アプリケーションのリスク管理](https://technet.microsoft.com/library/dn280946.aspx) (手順 3 を参照)|
Mideye | ADFS の mideye 認証プロバイダー | [Microsoft Active Directory フェデレーション サービスで mideye 2 要素認証](https://www.mideye.com/support/administrators/documentation/integration/microsoft-adfs/)|
|Okta | Active Directory フェデレーション サービスの Okta MFA | [Okta の MFA の Active Directory フェデレーション サービス (ADFS)](https://help.okta.com/en/prod/Content/Topics/integrations/adfs-okta-int.htm)|
|One Identity| Starling 2 fa AD FS|[Starling 2 fa AD FS アダプター](https://www.oneidentity.com/products/starling-two-factor-authentication/)|
|One Identity| Defender の AD FS|[Defender の AD FS アダプター](https://www.oneidentity.com/products/defender/)|
|Ping Identity|AD FS の PingID MFA アダプター|[AD FS の PingID MFA アダプター](https://documentation.pingidentity.com/pingid/pingidAdminGuide/index.shtml#pid_c_PingIDforADFSSSO.html)|
|RSA (EMC のセキュリティ部門)|RSA SecurID Authentication Agent for Microsoft Active Directory Federation Services|[Microsoft Active Directory フェデレーション サービス用には、RSA SecurID 認証エージェント](http://www.emc.com/security/rsa-securid/rsa-authentication-agents/microsoft-ad-fs.htm)|
|SafeNet, Inc.|SafeNet Authentication Service (SAS) Agent for AD FS|[SafeNet Authentication Service:AD FS エージェント構成ガイド](http://www.safenet-inc.com/resources/integration-guide/data-protection/Safenet_Authentication_Service/SafeNet_Authentication_Service__AD_FS_Agent_Configuration_Guide/?langtype=1033)|
|SecureMFA|SecureMFA OTP プロバイダー| [ADFS Multi-factor Authentication プロバイダー](https://www.securemfa.com/)|
|Swisscom|Mobile ID 認証サービスおよび署名サービス|[Mobile ID 認証サービス](http://swisscom.ch/mid)|
|Symantec|Symantec Validation and ID Protection Service (VIP)|[Symantec の検証と ID 保護サービス (VIP)](http://www.symantec.com/vip-authentication-service)|
|Trusona|Essential (パスワードなしの MFA) とエグゼクティブ (Essential + Identity 文章校正)| [Trusona 多要素認証](https://www.trusona.com/solution-overview/)|


## <a name="custom-authentication-method-for-ad-fs-in-windows-server-2012-r2"></a>Windows Server 2012 R2 での AD FS 用のカスタム認証方法
Windows Server 2012 R2 での AD FS 用に独自のカスタム認証方法を構築するための手順が提供されています。 詳細については、「 [Windows Server 2012 R2 での AD FS 用のカスタム認証方法の構築](https://go.microsoft.com/fwlink/?LinkID=511980)」を参照してください。

## <a name="see-also"></a>関連項目
[機密性の高いアプリケーションの追加の多要素認証によるリスクを管理します。](Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)


