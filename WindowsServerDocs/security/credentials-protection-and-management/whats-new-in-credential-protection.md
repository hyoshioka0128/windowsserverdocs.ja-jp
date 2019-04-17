---
title: "資格情報の保護の新機能"
description: "Windows Server のセキュリティ"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-credential-protection
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b0b5180-f65a-43ac-8ef3-66014116f297
author: gitmichiko
ms.author: michikos
manager: dongill
ms.date: 03/06/2017
ms.openlocfilehash: 0556c606b987a69eae663b0196467f532d5a307a
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="whats-new-in-credential-protection"></a>資格情報の保護の新機能

## <a name="credential-guard-for-signed-in-user"></a>サインインしたユーザーの資格情報 Guard

Windows 10 バージョン 1507 以降 Kerberos と NTLM を使用して仮想化ベースのセキュリティにサインインしたユーザーのログオン セッションの Kerberos と NTLM のシークレットを保護します。 

以降では、Windows 10 バージョン 1511 では、資格情報マネージャーは、ドメイン資格情報の種類の保存された資格情報を保護するのに仮想化ベースのセキュリティを使用します。 サインオン資格情報と保存されているドメインの資格情報は、リモート デスクトップを使用してリモート ホストに渡されません。 UEFI ロックなしは、credential Guard を有効にすることができます。

以降では、Windows 10 バージョン 1607 では、分離ユーザー モードは Hyper-V に含まれて、不要になったがインストールされているとは別に Credential Guard の展開のためです。

[詳細については、Credential Guard](https://technet.microsoft.com/en-us/itpro/windows/keep-secure/credential-guard)します。


## <a name="remote-credential-guard-for-signed-in-user"></a>サインインしたユーザーのリモートの Credential Guard

以降では、Windows 10 バージョン 1607 では、Remote Credential Guard によって保護にサインインしたユーザーの資格情報がクライアント デバイスで Kerberos と NTLM のシークレットを保護することにより、リモート デスクトップを使用する場合。 ユーザーとネットワーク リソースを評価するために、リモート ホストの認証要求は、機密情報を使用するクライアント デバイスが必要です。

リモート デスクトップを使用する場合、指定されたユーザーの資格情報の保護を Remote Credential Guard 以降では、Windows 10 バージョン 1703 では、します。

[詳細については、リモートの credential guard](https://technet.microsoft.com/en-us/itpro/windows/keep-secure/remote-credential-guard)します。

## <a name="domain-protections"></a>ドメインの保護

ドメインの保護では、Active Directory ドメインが必要です。

### <a name="domain-joined-device-support-for-authentication-using-public-key"></a>公開キーを使用して認証のドメインに参加しているデバイスのサポート

以降で Windows 10 バージョン 1507 および Windows Server 2016 では、ドメインに参加しているデバイスが Windows Server 2016 ドメイン コントローラー (DC) でバインドされているその公開キーを登録できる場合、デバイス認証できる Windows Server 2016 の DC に Kerberos を認証を使用して公開キーを持つ。

Windows Server 2016 以降、Kdc は Kerberos キーの信頼を使用して認証をサポートします。  

[ドメインに参加しているデバイスとキーの信頼の Kerberos の公開キーのサポートの詳細について](https://technet.microsoft.com/en-us/windows-server-docs/security/kerberos/whats-new-in-kerberos-authentication)します。

### <a name="pkinit-freshness-extension-support"></a>鮮度拡張機能のサポート

Windows 10 バージョン 1507 および Windows Server 2016 以降では、Kerberos クライアントはパブリック キー ベース サインオンの鮮度拡張子としてを試行します。 

Windows Server 2016 以降、Kdc を鮮度拡張機能をサポートできます。  既定では、Kdc を鮮度拡張機能は提供されません。 

[鮮度拡張機能のサポートの詳細について](https://technet.microsoft.com/en-us/windows-server-docs/security/kerberos/whats-new-in-kerberos-authentication)します。

### <a name="rolling-public-key-only-users-ntlm-secrets"></a>公開キーのみのユーザーの NTLM のシークレットのロールバック

ローリング NTLM の機密情報の公開キーのみユーザーの Windows Server 2016 ドメインの機能レベル (DFL) 以降では、Dc をサポートできます。 この機能は、なシャーシファンが低い DFLs でします。

> [!WARNING] 
> DC で更新された少なくとも 2016 年 11 月 8 日サービスの実行前に有効になっている NTLM シークレットの DC のクラッシュするリスクをローリングとドメインにドメイン コントローラーを追加します。 

構成: 新しいドメインは、この機能は既定で有効です。 既存のドメインの Active Directory 管理センターで構成する必要があります。 

1. Active Directory 管理センターで、左側のウィンドウにある、ドメインを右クリックして、**プロパティ**します。

    ![ドメインのプロパティ](../media/Credentials-Protection-And-Management/domain-properties.png)
    
2. 選択**対話型ログオンの Microsoft Passport またはスマート カードを使用するために必要であるユーザーのでは、サインアップ時の NTLM シークレットの有効期限が切れるのロールを有効にする**します。

    ![NTLM シークレットの有効期限が切れる Autoroll](../media/Credentials-Protection-And-Management/autoroll-ntlm.png)

3. をクリックして**OK**します。 

### <a name="allowing-network-ntlm-when-user-is-restricted-to-specific-domain-joined-devices"></a>ユーザーが特定のドメインに参加しているデバイスに制限されているときに、ネットワーク NTLM を許可します。

以降では、Windows Server 2016 ドメインの機能レベル (DFL)、Dc は、ユーザーがドメインに参加しているデバイスの特定に制限されているときにすることがネットワーク NTLM をサポートできます。 この機能では、低い DFLs で使用できません。

構成: で、認証ポリシー] をクリックして**NTLM を許可するネットワーク認証に制限されます。ユーザーとデバイスを選択した**します。 

[認証ポリシーの詳細について](https://technet.microsoft.com/en-us/windows-server-docs/security/credentials-protection-and-management/authentication-policies-and-authentication-policy-silos)します。
