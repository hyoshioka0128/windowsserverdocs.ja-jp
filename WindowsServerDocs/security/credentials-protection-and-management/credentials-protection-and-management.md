---
title: "資格情報の保護と管理"
description: "Windows Server のセキュリティ"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-credential-protection
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e457229c-0126-40fe-948c-101c943e1b57
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 16cc1f2260bf0552da6902dc3e97de65d29c7931
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="credentials-protection-and-management"></a>資格情報の保護と管理

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

IT プロフェッショナル向けのこのトピックでは、機能と Windows Server 2012 R2 と Windows 8.1 の資格情報の保護とドメイン認証コントロールを資格情報の盗用を減らすためにで導入された方法について説明します。

## <a name="BKMK_CredentialsProtectionManagement"></a>
### <a name="restricted-admin-mode-for-remote-desktop-connection"></a>リモート デスクトップ接続の制限付き管理モード
制限付き管理モードでは、対話形式で、サーバーに資格情報を送信することがなくリモート ホスト サーバーにログオンする方法を説明します。 これは、資格情報が、サーバーが侵害された場合、最初の接続プロセス中に回収されることを防ぎます。

で管理者の資格情報をこのモードを使用して、リモート デスクトップ クライアントは、資格情報を送信しなくてもこのモードをサポートするホストに対話的にログオンを試みます。 ホストは、それに接続するユーザー アカウントが管理者権限を持つ制限付き管理モードをサポートしていることを検証、接続が成功します。 それ以外の場合、接続の試行は失敗します。 制限付き管理モードでは、ポイント送信プレーン テキストまたはリモート コンピューターに資格情報の再利用可能なその他の形式ではなくしません。

### <a name="lsa-protection"></a>LSA の保護
ローカル セキュリティ機関 (LSA)、ローカル セキュリティ機関セキュリティ サービス (LSASS) プロセス内であるユーザー ローカルおよびリモート サインインを検証し、ローカル セキュリティ ポリシーを適用します。 Windows 8.1 オペレーティング システムでは、保護されていないプロセスによるコード インジェクションを防止するために LSA に追加の保護を提供します。 これは、LSA が格納し、管理するための資格情報の追加のセキュリティを提供します。 LSA の場合は、この保護されたプロセス設定は、Windows 8.1 で構成することができますは Windows RT 8.1 では既定でオンです、変更できません。

LSA の保護の構成については、次を参照してください。[追加 LSA の保護を構成する](configuring-additional-lsa-protection.md)します。

### <a name="protected-users-security-group"></a>Protected Users セキュリティ グループ
この新しいドメイン グローバル グループは、デバイスおよび Windows Server 2012 R2 および Windows 8.1 を実行しているホスト コンピューター上で新しいが構成可能な保護をトリガーします。 Protected Users グループは、ドメイン コントローラーと Windows Server 2012 R2 のドメイン内のドメインの追加の保護を使用できます。 これはユーザーがログオンしているとき、ネットワーク上のコンピューターに侵害されていないコンピューターから使用できる資格情報の種類が大幅に削減されます。

Protected Users グループのメンバーは、限られた認証の次のメソッドによって、さらに。

-   Protected Users グループのメンバーは、Kerberos プロトコルを使用してでのみに署名できます。 アカウントは、NTLM、ダイジェスト認証、または CredSSP を使用して認証できません。 Windows 8.1 を実行しているデバイスでパスワードがキャッシュされていない、ため、これらのセキュリティ サポート プロバイダー (Ssp) のいずれかを使用するデバイスは、アカウントが、保護されたユーザー グループのメンバーである、ドメインに対する認証に失敗します。

-   Kerberos プロトコルでは、事前認証プロセスで弱い DES または RC4 の暗号化の種類は使用しません。 つまり、少なくとも AES 暗号スイートをサポートするために、ドメインを構成する必要があります。

-   Kerberos の制約付きまたは制約のない委任できないか、ユーザー アカウントの委任します。 これは、ユーザーが Protected Users グループのメンバーである場合、他のシステムへの以前の接続が失敗することを意味します。

-   4 時間の既定の Kerberos Ticket Granting Ticket (Tgt) 有効期間設定は、認証ポリシーとサイロを Active Directory 管理センター (ADAC) のアクセスを使用して構成可能です。 つまり、4 時間が経過すると、ユーザー再度に認証する必要があります。

> [!WARNING]
> サービスおよびコンピューター用のアカウントでは、Protected Users グループのメンバーは使用できません。 パスワードまたは証明書は、ホスト上で利用可能な常にあるために、このグループにローカルでの保護が用意されていません。 Authentication will fail with the error "the user name or password is incorrect" for any service or computer that is added to the Protected Users group.

このグループの詳細については、次を参照してください。[Protected Users セキュリティ グループ](protected-users-security-group.md)します。

### <a name="authentication-policy-and-authentication-policy-silos"></a>認証ポリシーと認証ポリシー サイロ
フォレストに基づいた Active Directory ポリシーが導入されていると、Windows Server 2012 R2 のドメイン機能レベルを持つドメイン内のアカウントに適用できます。 これらの認証ポリシーは、ユーザーがログインに使用できるホストを制御できます。 Protect Users セキュリティ グループと連携して機能して、管理者は、アカウントに認証のアクセス制御条件を適用することができます。 これらの認証ポリシーは、ネットワークの範囲を制限する関連アカウントを分離します。

新しい Active Directory オブジェクト クラスで、認証ポリシーでは、Windows Server 2012 R2 ドメインの機能レベルを持つドメイン内のアカウント クラスに認証構成を適用することができます。 認証ポリシーを適用中に、Kerberos AS または TGS 交換します。 Active Directory アカウント クラスがあります。

-   ユーザー

-   コンピューター

-   管理されたサービス アカウント

-   グループの管理されたサービス アカウント

詳細については、次を参照してください。[認証ポリシーと認証ポリシー サイロ](authentication-policies-and-authentication-policy-silos.md)します。

詳細情報を構成するのには、アカウントを保護された、方法を参照してください[保護されるアカウントの構成方法](how-to-configure-protected-accounts.md)します。

## <a name="see-also"></a>参照してください。
For more information about the LSA and the LSASS, see the [Windows Logon and Authentication Technical Overview](https://technet.microsoft.com/library/dn169029(v=ws.10).aspx).



