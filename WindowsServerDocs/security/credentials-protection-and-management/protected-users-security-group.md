---
title: "Protected Users セキュリティ グループ"
description: "Windows Server のセキュリティ"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-credential-protection
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b0b5180-f65a-43ac-8ef3-66014116f296
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: bd6b53c0febdfb2d344136097a9654c981405568
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="protected-users-security-group"></a>Protected Users セキュリティ グループ

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

IT プロフェッショナル向けのこのトピックでは、Protected Users と、Active Directory セキュリティ グループの説明し、そのしくみについて説明します。 このグループは、Windows Server 2012 R2 のドメイン コントローラーで導入されました。

## <a name="BKMK_ProtectedUsers"></a>概要

このセキュリティ グループは、企業内で資格情報の公開を管理する戦略の一環として設計されています。 このグループのメンバーには、自分のアカウントに適用不可能の保護が自動的があります。 Protected Users グループのメンバーは、制限の厳しいしてが既定で事前にセキュリティで保護するものです。 これらのアカウントの保護を変更する唯一の方法では、セキュリティ グループからアカウントを削除します。

> [!WARNING]
> サービスおよびコンピューター用のアカウントでは、Protected Users グループのメンバーをする必要があることはありません。 このグループは、パスワードまたは証明書は、ホスト上で利用可能な常にあるために不完全な保護をいずれにせよ提供します。 エラー \"the ユーザー名に認証が失敗またはパスワードが incorrect\"のサービスまたは Protected Users グループに追加されているコンピューター。

このグループはドメインに関連する、グローバルでは、Windows Server 2012 R2 を実行しているプライマリ ドメイン コントローラーでデバイスおよび Windows Server 2012 R2 および Windows 8.1 を実行しているホスト コンピューター上で、後でドメイン内のユーザーが構成可能な保護をトリガーします。 これはユーザーのサインインでこのような保護コンピューターをするときに資格情報の既定のメモリ使用量が大幅に削減されます。

詳細については、次を参照してください。[Protected Users グループの動作方法](#BKMK_HowItWorks)このトピックの「します。



## <a name="BKMK_Requirements"></a>保護されたユーザー グループの要件
Protected Users グループのメンバーのデバイスの保護を提供するための要件は次のとおりです。

- Protected Users グローバル セキュリティ グループは、アカウント ドメイン内のすべてのドメイン コントローラーにレプリケートされます。

- Windows 8.1 および Windows Server 2012 R2 は、既定ではサポートが追加されました。 [マイクロソフト セキュリティ アドバイザリ 2871997](https://technet.microsoft.com/library/security/2871997) Windows 7、Windows Server 2008 R2 および Windows Server 2012 にサポートを追加します。

Protected Users グループのメンバーにドメイン コントローラーの保護を提供するための要件は次のとおりです。

- ユーザーは、ドメインには、Windows Server 2012 R2 または以上のドメイン機能レベルでなければなりません。

### <a name="adding-protected-user-global-security-group-to-down-level-domains"></a>ダウンレベルのドメインにユーザーの保護されたグローバル セキュリティ グループを追加します。

Windows Server 2012 R2 より前のオペレーティング システムを実行するドメイン コントローラーは、新しい Protected Users セキュリティ グループにメンバーを追加するをサポートできます。 これにより、ドメインをアップグレードする前に、デバイスの保護を活用できます。 

> [!Note]
> ドメイン コントローラーは、ドメインの保護をサポートしていません。 

によって保護されているユーザー グループを作成することができます[、プライマリ ドメイン コントローラー (PDC) エミュレーターの役割を転送する](https://technet.microsoft.com/library/cc816944(v=ws.10).aspx)Windows Server 2012 R2 を実行しているドメイン コントローラーにします。 そのグループのオブジェクトは、その他のドメイン コント ローラーにレプリケートされた後は、Windows Server の以前のバージョンを実行しているドメイン コント ローラーで PDC エミュレーターの役割をホストできます。

### <a name="BKMK_ADgroup"></a>保護されていないユーザー AD グループのプロパティ

次の表では、Protected Users グループのプロパティを指定します。

|属性|値|
|-------|-----|
|SID/RID|S-1-5-21 -<domain>-525|
|種類|ドメイン グローバル|
|既定のコンテナー|CN = Users, DC =<domain>、DC =|
|既定のメンバー|[なし]|
|既定のメンバー|[なし]|
|ADMINSDHOLDER で保護されているか。|違います|
|既定のコンテナーから移動することができるか。|うん|
|サービス管理者以外には、このグループの管理に委任することができるか。|違います|
|既定のユーザー権利|既定のユーザー権限を持っていません。|

## <a name="BKMK_HowItWorks"></a>Protected Users グループのしくみ
このセクションでは、Protected Users グループのしくみ場合について説明します。

-   Windows デバイスにログに記録

-   ユーザー アカウントのドメインが Windows Server 2012 R2 または以上のドメイン機能レベルです。

### <a name="device-protections-for-signed-in-protected-users"></a>内のデバイスの保護は、Protected Users に記録
ログイン ユーザーが Protected Users グループのメンバーである場合、次の保護が適用されます。

-   資格情報の委任 (CredSSP) は、ユーザーのプレーン テキストの資格情報が場合でもキャッシュではなく、**既定の資格情報の委任を許可する**グループ ポリシー設定を有効にします。

-   Windows 8.1 および Windows Server 2012 R2 以降、Windows ダイジェストはキャッシュしませんプレーン テキストの資格情報をユーザーの Windows ダイジェストが有効になっている場合でもします。

> [!Note]
> インストールした後[マイクロソフト セキュリティ アドバイザリ 2871997](https://technet.microsoft.com/library/security/2871997)レジストリ キーを構成するまで、資格情報をキャッシュする Windows ダイジェストが続行されます。 参照してください[マイクロソフト セキュリティ アドバイザリ: 資格情報の保護と管理を向上させるために更新プログラム: 2014 年 5 月 13 日](https://support.microsoft.com/en-us/help/2871997/microsoft-security-advisory-update-to-improve-credentials-protection-a)手順についてはします。

-   ユーザーのプレーン テキストの資格情報または NT の一方向の関数 (NTOWF)、NTLM はキャッシュされません。

-   Kerberos は、DES または RC4 のキーを作成されなくなります。 いないキャッシュ、ユーザーの資格情報をプレーン テキストまたは長期的なキー初期の TGT が取得した後です。

-   キャッシュされた検証機能では、サインイン時は作成されませんまたはロック解除、オフラインでのサインインはサポートされなくようにします。

ユーザー アカウントが Protected Users グループに追加されると、保護は、ユーザーがデバイスにサインインするときに開始されます。

### <a name="domain-controller-protections-for-protected-users"></a>Protected Users に対するドメイン コントローラーの保護
Windows Server 2012 R2 のドメインに対して認証される Protected Users グループのメンバーであるアカウントにすることはできません。

-   NTLM 認証を認証します。

-   Kerberos 事前認証で DES または RC4 の暗号化の種類を使用します。

-   制約なし/制約付き委任を使用して委任されます。

-   最初の 4 時間の有効期間を超える Kerberos Tgt を更新します。

Protected Users グループのすべてのアカウントの Tgt の有効期限を構成できない設定が確立されます。 Tgt 有効期間と更新をドメイン ポリシーに基づくドメイン コントローラーが通常は、設定**ユーザー チケットの最長有効期間**と**ユーザー チケットを更新できる最長有効期間**します。 Protected Users グループで、これらのドメイン ポリシー 600 分が設定されます。

詳細については、次を参照してください。[保護されるアカウントの構成方法](how-to-configure-protected-accounts.md)します。

## <a name="troubleshooting"></a>トラブルシューティング
次の 2 つの運用管理ログが Protected Users に関連するイベントのトラブルシューティングに役立つ使用できます。 これらの新しいログ イベント ビューアー内にあると、既定で無効になっているし、下にある**アプリケーションとサービス \microsoft\windows\microsoft\authentication**します。

|イベント ID とログ|説明|
|----------|--------|
|104<br /><br />**ProtectedUser クライアント**|理由: セキュリティ パッケージに、クライアントでは、資格情報は含まれません。<br /><br />アカウントが Protected Users セキュリティ グループのメンバーである場合、クライアント コンピューターに、エラーが記録されます。 このイベントは、セキュリティ パッケージが、サーバーを認証するために必要な資格情報をキャッシュしていないことを示します。<br /><br />パッケージ名、ユーザー名、ドメイン名、およびサーバーの名前が表示されます。|
|304<br /><br />**ProtectedUser クライアント**|理由: セキュリティ パッケージでは、Protected Users の資格情報は保存されません。<br /><br />セキュリティ パッケージが、ユーザーのサインイン資格情報をキャッシュしていないことを示すためにクライアントでは、情報イベントが記録されます。 Protected Users のサインオン資格情報を持つダイジェスト (WDigest)、資格情報の委任 (CredSSP)、および NTLM が失敗すると想定されます。 アプリケーションを求めれば、成功する資格情報の入力を求める、します。<br /><br />パッケージ名、ユーザー名、およびドメイン名が表示されます。|
|100<br /><br />**ProtectedUserFailures DomainController**|理由: NTLM のサインイン エラーは、Protected Users セキュリティ グループであるアカウントで発生します。<br /><br />アカウントが Protected Users セキュリティ グループのメンバーであるために NTLM 認証が失敗したことを示すために、ドメイン コントローラーでは、エラーが記録されます。<br /><br />デバイスの名前とアカウントの名前が表示されます。|
|104<br /><br />**ProtectedUserFailures DomainController**|理由: DES または RC4 の暗号化の種類は Kerberos 認証に使用され、Protected Users セキュリティ グループ内のユーザーのサインイン エラーが発生します。<br /><br />アカウントが Protected Users セキュリティ グループのメンバーである、DES および RC4 の暗号化の種類を使用できないために、Kerberos の事前認証が失敗しました。<br /><br />(AES は使用できます)|
|303<br /><br />**ProtectedUserSuccesses DomainController**|理由: Kerberos チケットの保証-チケット (TGT) は、保護されたユーザー グループのメンバーに対して発行が正常にされました。|



## <a name="additional-resources"></a>その他のリソース

-   [資格情報の保護と管理](credentials-protection-and-management.md)

-   [認証ポリシーと認証ポリシー サイロ](authentication-policies-and-authentication-policy-silos.md)

-   [保護されたアカウントを構成する方法](how-to-configure-protected-accounts.md)


