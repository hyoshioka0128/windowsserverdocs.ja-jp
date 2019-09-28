---
title: Protected Users セキュリティ グループ
description: Windows Server のセキュリティ
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 0cbec876ebf8a3ce27bf0d6f099ade6a5d6bc032
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403774"
---
# <a name="protected-users-security-group"></a>Protected Users セキュリティ グループ

>適用先:Windows Server (半期チャネル)、Windows Server 2016

ここでは、IT プロフェッショナル向けに、Active Directory のセキュリティ グループである Protected Users と、そのしくみについて説明します。 このグループは、Windows Server 2012 R2 ドメインコントローラーで導入されました。

## <a name="BKMK_ProtectedUsers"></a>概要

このセキュリティグループは、企業内の資格情報の公開を管理する戦略の一環として設計されています。 このグループのメンバーのアカウントには、構成可能ではない保護が自動的に適用されます。 Protected Users グループのメンバーであるということは、既定で制限的であり、予防的にセキュリティで保護されることを示します。 アカウントに関してこのような保護を変更する唯一の方法は、このセキュリティ グループからアカウントを削除することです。

> [!WARNING]
> サービスとコンピューターのアカウントは、Protected Users グループのメンバーにはなりません。 パスワードまたは証明書が常にホストで使用可能であるため、このグループは不完全な保護を提供します。 認証は、保護されたユーザーグループに追加されたサービスまたはコンピューターのユーザー名またはパスワードが正しくないことを示すエラー @no__t で失敗します。

このドメイン関連のグローバルグループは、windows server 2012 R2 を実行しているプライマリドメインコントローラーを持つドメイン内のユーザーに対して、Windows Server 2012 R2 以降を実行 Windows 8.1 しているデバイスとホストコンピューターで、構成可能ではない保護をトリガーします。 これにより、ユーザーがこれらの保護を使用してコンピューターにサインインするときに、資格情報の既定のメモリフットプリントが大幅に削減されます。

詳細については、このトピックの「 [Protected Users グループのしくみ](#BKMK_HowItWorks)」を参照してください。



## <a name="BKMK_Requirements"></a>Protected Users グループの要件
Protected Users グループのメンバーにデバイスの保護を提供するための要件は次のとおりです。

- Protected Users グローバル セキュリティ グループは、アカウント ドメインのすべてのドメイン コントローラーにレプリケートされている。

- Windows 8.1 と Windows Server 2012 R2 では、既定でサポートが追加されています。 [Microsoft セキュリティアドバイザリ 2871997](https://technet.microsoft.com/library/security/2871997)では、windows 7、windows Server 2008 R2、および windows server 2012 のサポートが追加されています。

Protected Users グループのメンバーにドメイン コントローラーの保護機能を提供するには、次の要件があります。

- ユーザーは、Windows Server 2012 R2 以上のドメイン機能レベルのドメインに存在する必要があります。

### <a name="adding-protected-user-global-security-group-to-down-level-domains"></a>下位ドメインに保護されたユーザーのグローバルセキュリティグループを追加しています

Windows Server 2012 R2 より前のオペレーティングシステムを実行するドメインコントローラーでは、新しい保護されたユーザーセキュリティグループへのメンバーの追加をサポートできます。 これにより、ユーザーは、ドメインをアップグレードする前にデバイスの保護を利用できるようになります。 

> [!Note]
> ドメインコントローラーは、ドメインの保護をサポートしていません。 

Protected Users グループを作成するには、Windows Server 2012 R2 を実行するドメインコントローラーに[プライマリドメインコントローラー (PDC) エミュレーターの役割を転送](https://technet.microsoft.com/library/cc816944(v=ws.10).aspx)します。 そのグループのオブジェクトが他のドメイン コントローラーにレプリケートされた後に、以前のバージョンの Windows Server が実行されているドメイン コントローラーで PDC エミュレーターの役割をホストできます。

### <a name="BKMK_ADgroup"></a>Protected Users グループの AD プロパティ

次の表は、Protected Users グループのプロパティの一覧です。

|属性|値|
|-------|-----|
|既知の SID/RID|S-1-5-21-<domain>-525|
|種類|ドメイン グローバル|
|既定のコンテナー|CN=Users、DC=<domain>、DC=|
|既定メンバー|なし|
|～の既定のメンバー|なし|
|ADMINSDHOLDER で保護されているか|いいえ|
|既定のコンテナーから移動することができるか|はい|
|このグループの管理をサービス管理者以外に委任することができるか|いいえ|
|既定のユーザー権利|既定のユーザー権利はありません|

## <a name="BKMK_HowItWorks"></a>Protected Users グループのしくみ
ここでは、次の場合に Protected Users グループがどのように機能するかについて説明します。

-   Windows デバイスで署名済み

-   ユーザーアカウントドメインが Windows Server 2012 R2 以上のドメイン機能レベルにある

### <a name="device-protections-for-signed-in-protected-users"></a>署名済みの保護されたユーザーに対するデバイスの保護
サインインしているユーザーが Protected Users グループのメンバーである場合は、次の保護が適用されます。

-   [**既定の資格情報の委任を許可**する] グループポリシー設定が有効になっている場合でも、資格情報の委任 (CredSSP) では、ユーザーのプレーンテキストの資格情報はキャッシュされません。

-   Windows 8.1 と Windows Server 2012 R2 以降では、windows digest が有効になっている場合でも、ユーザーのプレーンテキストの資格情報はキャッシュされません。

> [!Note]
> [Microsoft セキュリティアドバイザリ 2871997](https://technet.microsoft.com/library/security/2871997)をインストールした後、レジストリキーが構成されるまで、Windows ダイジェストは引き続き資格情報をキャッシュします。 「@No__t-0Microsoft セキュリティアドバイザリ:資格情報の保護と管理を向上させるための更新:手順については、2014年5月13日 @ no__t-0。

-   NTLM では、ユーザーのプレーンテキストの資格情報または NT の一方向の機能 (NTOWF) はキャッシュされません。

-   Kerberos では、DES キーまたは RC4 キーは作成されなくなりました。 また、最初の TGT を取得した後で、ユーザーのプレーンテキストの資格情報や長期キーをキャッシュすることもありません。

-   キャッシュされた検証は、サインイン時またはロック解除時に作成されないため、オフラインサインインはサポートされなくなりました。

ユーザーアカウントが Protected Users グループに追加されると、ユーザーがデバイスにサインインしたときに保護が開始されます。

### <a name="domain-controller-protections-for-protected-users"></a>保護されたユーザーに対するドメインコントローラーの保護
Windows Server 2012 R2 ドメインに対して認証される Protected Users グループのメンバーであるアカウントは、次のことを行うことができません。

-   NTLM 認証を使用して認証する。

-   Kerberos の事前認証で DES または RC4 の暗号化の種類を使用する。

-   制約なしの委任または制約付き委任を使用して委任する。

-   Kerberos TGT の最初の 4 時間の有効期間を延長する。

Protected Users グループのアカウントごとに、TGT の期限切れに対する構成可能ではない設定が指定されます。 通常、ドメイン コントローラーは、ドメイン ポリシー、 **[チケットの最長有効期間]** 、および **[ユーザー チケットを更新できる最長有効期間]** に基づいて TGT の有効期間と更新を設定します。 Protected Users グループの場合、このようなドメイン ポリシーに 600 分が設定されます。

詳細については、「[保護されるアカウントの構成方法](how-to-configure-protected-accounts.md)」をご覧ください。

## <a name="troubleshooting"></a>トラブルシューティング
2 つの運用管理ログを使用して、Protected Users に関連するイベントを解決することができます。 これらの新しいログはイベント ビューアーに表示され、既定では無効です。ログは **Applications and Services Logs\Microsoft\Windows\Microsoft\Authentication**に保存されます。

|イベント ID とログ|説明|
|----------|--------|
|104<br /><br />**ProtectedUser-Client**|理由: クライアントのセキュリティ パッケージに資格情報が含まれていません。<br /><br />アカウントが Protected Users セキュリティ グループのメンバーである場合、エラーはクライアント コンピューターのログに記録されます。 このイベントは、サーバーに対して認証するために必要な資格情報をセキュリティ パッケージがキャッシュしていないことを示します。<br /><br />パッケージ名、ユーザー名、ドメイン名、およびサーバー名を表示します。|
|304<br /><br />**ProtectedUser-Client**|理由: セキュリティパッケージには、保護されたユーザーの資格情報は保存されません。<br /><br />情報イベントは、セキュリティパッケージがユーザーのサインイン資格情報をキャッシュしていないことを示すために、クライアントに記録されます。 ダイジェスト (WDigest)、資格情報の委任 (CredSSP)、および NTLM は、Protected Users のサインオン資格情報を取得できないと想定されます。 アプリケーションは、資格情報の入力を求めれば、成功することができます。<br /><br />パッケージ名、ユーザー名、およびドメイン名を表示します。|
|100<br /><br />**ProtectedUserFailures-DomainController**|理由: NTLM のサインインの失敗は、Protected Users セキュリティ グループに属するアカウントの場合に発生します。<br /><br />アカウントは Protected Users セキュリティ グループのメンバーだったために NTLM の認証が失敗したことを示すエラーが、ドメイン コントローラーのログに記録されます。<br /><br />アカウント名とデバイス名を表示します。|
|104<br /><br />**ProtectedUserFailures-DomainController**|理由: DES または RC4 の暗号化の種類は Kerberos 認証に使用されており、Protected Users セキュリティ グループに属するユーザーのサインイン エラーが発生します。<br /><br />アカウントが Protected Users セキュリティ グループのメンバーである場合、DES および RC4 の暗号化の種類を使用できないため、Kerberos の事前認証は失敗しました。<br /><br />(AES は使用できます)|
|303<br /><br />**ProtectedUserSuccesses-DomainController**|理由: Kerberos ticket-granting-ticket (TGT) は、Protected Users グループのメンバーに対して正常に発行されました。|



## <a name="additional-resources"></a>その他の技術情報

-   [資格情報の保護と管理](credentials-protection-and-management.md)

-   [認証ポリシーと認証ポリシー サイロ](authentication-policies-and-authentication-policy-silos.md)

-   [保護されるアカウントの構成方法](how-to-configure-protected-accounts.md)


