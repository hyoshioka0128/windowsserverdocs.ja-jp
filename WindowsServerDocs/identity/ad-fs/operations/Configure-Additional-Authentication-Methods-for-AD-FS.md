---
ms.assetid: ddfbbda3-30ca-4537-af12-667efc6f63ff
title: "AD FS の追加の認証方法を構成します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 65baa6f94e1efa1fa337eab477b18f947cf0bb2d
ms.sourcegitcommit: 36d7b1dfd7da8e9f303d007a628e76149de000f2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2018
---
# <a name="configure-additional-authentication-methods-for-ad-fs"></a>AD FS の追加の認証方法を構成します。

>適用対象: Windows Server 2016、Windows Server 2012 R2

多要素認証 (MFA) を有効にするためには、少なくとも 1 つの追加の認証方法を選択してください。 Active Directory フェデレーション サービス (AD FS) で Windows Server 2012 R2 では、既定に追加の認証方法として証明書の認証 (つまり、スマート カード ベースの認証) を選択できます。

> [!NOTE]
> 証明書の認証を選択する場合は、スマート カード証明書が安全にプロビジョニングされていて、暗証番号 (pin) の要件があることを確認します。

Microsoft Azure がクラウドに同様の機能を提供することをご存知でしたか。 詳細については[Microsoft Azure ID ソリューション](http://aka.ms/m2w274)します。<br /><br />Microsoft Azure でハイブリッド ID ソリューションを作成します。<br /> - [Azure の Multi-factor Authentication について説明します。](http://aka.ms/ey6o9r)<br /> - [クラウド認証を使用した単一フォレスト ハイブリッド環境の ID を管理します。](http://aka.ms/g1jat8)<br /> - [追加の多要素認証による個人情報アプリケーションのリスクを管理します。](http://aka.ms/kt1bbm)|

## <a name="microsoft-and-third-party-additional-authentication-methods"></a>Microsoft とサード パーティ製の追加の認証方法
構成し、[Microsoft と Windows Server 2012 R2 の AD FS サード パーティの認証方法を有効にすることもできます。 いったんインストールして、AD FSに登録して、グローバルまたはごとの利用者の認証ポリシーの一部としてMFAを強制できます。

以下は Microsoft とサード パーティ プロバイダーと MFA ソリューションのアルファベット順の一覧現在利用可能な Windows Server 2012 R2 で AD FS 用です。

||||
|-|-|-|
|**プロバイダー**|**提供します。**|**リンクの詳細**|
|Gemalto|Gemalto アイデンティティ & セキュリティ サービス|[http://www.gemalto.com/identity](http://www.gemalto.com/identity)|
|inWebo テクノロジ|inWebo エンタープライズ認証サービス|[inWebo エンタープライズ認証](http://www.inwebo.com)|
|ログイン ユーザー|AD FS 2012 R2 (パブリック ベータ版) のログイン People MFA API コネクタ|[https://www.loginpeople.com](https://www.loginpeople.com)|
|Microsoft corp|Microsoft Azure MFA|[チュートリアル ガイド: 追加の多要素認証による個人情報アプリケーションのリスクを管理する](https://technet.microsoft.com/library/dn280946.aspx)(手順 3 を参照してください)|
|RSA、EMC のセキュリティ部門|Microsoft Active Directory フェデレーション サービスの RSA SecurID 認証エージェント|[Microsoft Active Directory フェデレーション サービスの RSA SecurID 認証エージェント](http://www.emc.com/security/rsa-securid/rsa-authentication-agents/microsoft-ad-fs.htm)|
|SafeNet, inc.|AD FS の SafeNet Authentication サービス (SAS) エージェント|[SafeNet Authentication Service: AD FS エージェント構成ガイド](http://www.safenet-inc.com/resources/integration-guide/data-protection/Safenet_Authentication_Service/SafeNet_Authentication_Service__AD_FS_Agent_Configuration_Guide/?langtype=1033)|
|Swisscom 社|Mobile ID 認証サービスおよび署名サービス|[Mobile ID 認証サービス](http://swisscom.ch/mid)|
|Symantec|Symantec の検証と ID Protection Service (VIP)|[Symantec の検証と ID Protection Service (VIP)](http://www.symantec.com/vip-authentication-service)|

## <a name="custom-authentication-method-for-ad-fs-in-windows-server-2012-r2"></a>Windows Server 2012 R2 で AD FS のカスタム認証方法
Windows Server 2012 R2 の AD FS で独自のカスタム認証方法を構築するための手順が提供されています。 詳細については、次を参照してください。[Windows Server 2012 R2 の AD FS でのカスタム認証方法の構築](https://go.microsoft.com/fwlink/?LinkID=511980)します。

## <a name="see-also"></a>参照してください。
[追加の多要素認証による個人情報アプリケーションのリスクを管理します。](Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)


