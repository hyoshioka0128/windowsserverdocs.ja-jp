---
title: Protected Users セキュリティ グループ
description: Windows Server のセキュリティ
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862363"
---
# <a name="protected-users-security-group"></a>Protected Users セキュリティ グループ

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

ここでは、IT プロフェッショナル向けに、Active Directory のセキュリティ グループである Protected Users と、そのしくみについて説明します。 このグループは、ドメイン コント ローラーの Windows Server 2012 R2 で導入されました。

## <a name="BKMK_ProtectedUsers"></a>概要

このセキュリティ グループは、企業内で資格情報の公開を管理する戦略の一環として設計されています。 このグループのメンバーのアカウントには、構成可能ではない保護が自動的に適用されます。 Protected Users グループのメンバーであるということは、既定で制限的であり、予防的にセキュリティで保護されることを示します。 アカウントに関してこのような保護を変更する唯一の方法は、このセキュリティ グループからアカウントを削除することです。

> [!WARNING]
> サービスとコンピューターのアカウント Protected Users グループのメンバーにすることはありません。 このグループは、不完全な保護パスワードまたは証明書は、ホストで使用可能では常にためも提供します。 認証は、エラーで失敗\"ユーザー名またはパスワードが正しくありません\"の任意のサービスまたは Protected Users グループに追加されているコンピューター。

このドメインに関連する、グローバル グループは、Windows Server 2012 R2 を実行しているプライマリ ドメイン コント ローラーとデバイスと Windows Server 2012 R2 および Windows 8.1 を実行しているホスト コンピューター上または後でドメイン内のユーザーが構成可能な保護をトリガーします。 これはときにユーザーのサインインでは、このような保護コンピューターに資格情報の既定のメモリ使用量が大幅に減少します。

詳細については、次を参照してください。 [Protected Users グループの動作方法](#BKMK_HowItWorks)このトピックの「します。



## <a name="BKMK_Requirements"></a>保護されたユーザー グループの要件
Protected Users グループのメンバーのデバイスの保護を提供するための要件は次のとおりです。

- Protected Users グローバル セキュリティ グループは、アカウント ドメインのすべてのドメイン コントローラーにレプリケートされている。

- Windows 8.1 および Windows Server 2012 R2 は、既定でサポートを追加します。 [マイクロソフト セキュリティ アドバイザリ 2871997](https://technet.microsoft.com/library/security/2871997)には、Windows 7、Windows Server 2008 R2 および Windows Server 2012 のサポートを追加します。

Protected Users グループのメンバーにドメイン コントローラーの保護機能を提供するには、次の要件があります。

- ユーザーは、Windows Server 2012 R2 または以上のドメイン機能レベル ドメインでなければなりません。

### <a name="adding-protected-user-global-security-group-to-down-level-domains"></a>ダウンレベルのドメインにユーザーの保護されているグローバル セキュリティ グループを追加します。

Windows Server 2012 R2 より前のオペレーティング システムを実行するドメイン コント ローラーには、新しいユーザーの保護されているセキュリティ グループにメンバーを追加するをサポートできます。 これにより、ユーザーがドメインをアップグレードする前に、デバイスの保護を活用できます。 

> [!Note]
> ドメイン コント ローラーは、ドメインの保護をサポートしていません。 

Protected Users グループを作成できます[プライマリ ドメイン コント ローラー (PDC) エミュレーターの役割を転送する](https://technet.microsoft.com/library/cc816944(v=ws.10).aspx)Windows Server 2012 R2 を実行するドメイン コント ローラーにします。 そのグループのオブジェクトが他のドメイン コントローラーにレプリケートされた後に、以前のバージョンの Windows Server が実行されているドメイン コントローラーで PDC エミュレーターの役割をホストできます。

### <a name="BKMK_ADgroup"></a>保護されたユーザーの AD グループのプロパティ

次の表は、Protected Users グループのプロパティの一覧です。

|属性|Value|
|-------|-----|
|既知の SID/RID|S-1-5-21-<domain>-525|
|種類|ドメイン グローバル|
|既定のコンテナー|CN=Users、DC=<domain>、DC=|
|既定メンバー|なし|
|～の既定のメンバー|なし|
|ADMINSDHOLDER で保護されているか|X|
|既定のコンテナーから移動することができるか|〇|
|このグループの管理をサービス管理者以外に委任することができるか|X|
|既定のユーザー権利|既定のユーザー権利はありません|

## <a name="BKMK_HowItWorks"></a>Protected Users グループのしくみ
ここでは、次の場合に Protected Users グループがどのように機能するかについて説明します。

-   Windows デバイスのサインイン

-   ユーザー アカウントのドメインが Windows Server 2012 R2 または以上のドメイン機能レベルです。

### <a name="device-protections-for-signed-in-protected-users"></a>Protected Users サインイン内のデバイスの保護
サインインしているユーザーが Protected Users グループのメンバーである次の保護が適用されます。

-   資格情報の委任 (CredSSP) は場合であっても、ユーザーのプレーン テキストの資格情報キャッシュではなく、**既定の資格情報の委任を許可する**グループ ポリシー設定を有効にします。

-   Windows 8.1 および Windows Server 2012 R2 以降、Windows ダイジェストでキャッシュされませんが、ユーザーのプレーン テキストの資格情報 Windows ダイジェストが有効な場合でもです。

> [!Note]
> インストールした後[Microsoft セキュリティ アドバイザリ 2871997](https://technet.microsoft.com/library/security/2871997)レジストリ キーが構成されるまで資格情報をキャッシュする Windows ダイジェストが続行されます。 参照してください[マイクロソフト セキュリティ アドバイザリ。資格情報の保護と管理を向上させるために更新します。2014 年 5 月 13 日](https://support.microsoft.com/en-us/help/2871997/microsoft-security-advisory-update-to-improve-credentials-protection-a)手順についてはします。

-   NTLM は、ユーザーのプレーン テキストの資格情報または NT の一方向の関数 (NTOWF) にはキャッシュしません。

-   Kerberos では、DES または RC4 キーは作成されなくなります。 キャッシュしません、ユーザーの資格情報をプレーン テキストまたはキーの長期的な初期の TGT を取得した後。

-   キャッシュされた検証機能では、サインイン時に作成されませんまたはロック解除、ため、オフラインの記号ではサポートされていません。

ユーザー アカウントが Protected Users グループに追加されると、保護は、ユーザーがデバイスにサインインするときに開始されます。

### <a name="domain-controller-protections-for-protected-users"></a>Protected Users に対するドメイン コント ローラーの保護
Windows Server 2012 R2 のドメインに対して認証される Protected Users グループのメンバーであるアカウントにできます。

-   NTLM 認証を使用して認証する。

-   Kerberos の事前認証で DES または RC4 の暗号化の種類を使用する。

-   制約なしの委任または制約付き委任を使用して委任する。

-   Kerberos TGT の最初の 4 時間の有効期間を延長する。

Protected Users グループのアカウントごとに、TGT の期限切れに対する構成可能ではない設定が指定されます。 通常、ドメイン コントローラーは、ドメイン ポリシー、**[チケットの最長有効期間]**、および **[ユーザー チケットを更新できる最長有効期間]** に基づいて TGT の有効期間と更新を設定します。 Protected Users グループの場合、このようなドメイン ポリシーに 600 分が設定されます。

詳細については、「[保護されるアカウントの構成方法](how-to-configure-protected-accounts.md)」をご覧ください。

## <a name="troubleshooting"></a>トラブルシューティング
2 つの運用管理ログを使用して、Protected Users に関連するイベントを解決することができます。 これらの新しいログはイベント ビューアーに表示され、既定では無効です。ログは **Applications and Services Logs\Microsoft\Windows\Microsoft\Authentication**に保存されます。

|イベント ID とログ|説明|
|----------|--------|
|104<br /><br />**ProtectedUser-Client**|理由: クライアントのセキュリティ パッケージに資格情報が含まれていません。<br /><br />アカウントが Protected Users セキュリティ グループのメンバーである場合、エラーはクライアント コンピューターのログに記録されます。 このイベントは、サーバーに対して認証するために必要な資格情報をセキュリティ パッケージがキャッシュしていないことを示します。<br /><br />パッケージ名、ユーザー名、ドメイン名、およびサーバー名を表示します。|
|304<br /><br />**ProtectedUser-Client**|理由: セキュリティ パッケージでは、保護されているユーザーの資格情報は保存されません。<br /><br />情報イベントは、セキュリティ パッケージが、ユーザーのサインイン資格情報をキャッシュしていないことを示すためにクライアントに記録されます。 ダイジェスト (WDigest)、資格情報の委任 (CredSSP)、および NTLM は、Protected Users のサインオン資格情報を取得できないと想定されます。 アプリケーションは、資格情報の入力を求めれば、成功することができます。<br /><br />パッケージ名、ユーザー名、およびドメイン名を表示します。|
|100<br /><br />**ProtectedUserFailures-DomainController**|理由: NTLM のサインインの失敗は、Protected Users セキュリティ グループに属するアカウントの場合に発生します。<br /><br />アカウントは Protected Users セキュリティ グループのメンバーだったために NTLM の認証が失敗したことを示すエラーが、ドメイン コントローラーのログに記録されます。<br /><br />アカウント名とデバイス名を表示します。|
|104<br /><br />**ProtectedUserFailures-DomainController**|理由: DES または RC4 の暗号化の種類は Kerberos 認証に使用されており、Protected Users セキュリティ グループに属するユーザーのサインイン エラーが発生します。<br /><br />アカウントが Protected Users セキュリティ グループのメンバーである場合、DES および RC4 の暗号化の種類を使用できないため、Kerberos の事前認証は失敗しました。<br /><br />(AES は使用できます)|
|303<br /><br />**ProtectedUserSuccesses-DomainController**|理由: Kerberos ticket-granting-ticket (TGT) は、Protected Users グループのメンバーに対して正常に発行されました。|



## <a name="additional-resources"></a>その他の資料

-   [資格情報の保護と管理](credentials-protection-and-management.md)

-   [認証ポリシーと認証ポリシー サイロ](authentication-policies-and-authentication-policy-silos.md)

-   [保護されたアカウントを構成する方法](how-to-configure-protected-accounts.md)


