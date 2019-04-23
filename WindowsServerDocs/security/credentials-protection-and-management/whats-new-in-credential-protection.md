---
title: 新機能については資格情報の保護
description: Windows Server のセキュリティ
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
ms.openlocfilehash: ec41e85949cb61c8130d8765b4786eefe39ebd0b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855593"
---
# <a name="whats-new-in-credential-protection"></a>新機能については資格情報の保護

## <a name="credential-guard-for-signed-in-user"></a>サインイン ユーザーの Credential Guard

以降、Windows 10 バージョン 1507、Kerberos と NTLM を使用して仮想化ベースのセキュリティ サインイン ユーザーのログオン セッションの Kerberos と NTLM のシークレットを保護します。 

Windows 10 バージョン 1511 以降資格情報マネージャーは、ドメイン資格情報の種類の保存された資格情報を保護するのに仮想化ベースのセキュリティを使用します。 サインイン資格情報と保存されているドメインの資格情報はリモート デスクトップを使用してリモート ホストに渡されません。 UEFI ロックなしは、Credential Guard を有効にすることができます。

以降で Windows 10 version 1607 では、分離ユーザー モードは、HYPER-V に含まれていますが不要になったがインストールされているとは別に Credential Guard の展開のため。

[詳細については、Credential Guard は](https://technet.microsoft.com/itpro/windows/keep-secure/credential-guard)します。


## <a name="remote-credential-guard-for-signed-in-user"></a>サインイン ユーザーの Credential Guard をリモート

クライアント デバイスで Kerberos と NTLM のシークレットを保護することにより、リモート デスクトップを使用する場合、サインイン ユーザーの資格情報の保護を Credential Guard をリモート以降では、Windows 10 バージョン 1607 を所有します。 ユーザーとネットワーク リソースを評価するため、リモート ホストの認証要求にシークレットを使用するクライアント デバイスが必要です。

リモート デスクトップを使用する場合、指定されたユーザーの資格情報の保護を Credential Guard をリモート Windows 10 バージョン 1703 以降します。

[詳細については、リモートの credential guard は](https://technet.microsoft.com/itpro/windows/keep-secure/remote-credential-guard)します。

## <a name="domain-protections"></a>ドメインの保護

ドメインの保護には、Active Directory ドメインが必要です。

### <a name="domain-joined-device-support-for-authentication-using-public-key"></a>ドメインに参加しているデバイスで公開キーを使用する認証のサポート

以降では、Windows 10 バージョン 1507、Windows Server 2016 ではドメインに参加しているデバイスが Windows Server 2016 ドメイン コント ローラー (DC) にバインドされている公開キーを登録できない場合、デバイスで認証できる Kerberos PKINIT を使用して、公開キーWindows Server 2016 の DC を認証します。

Windows Server 2016 以降、Kdc はキー信頼の Kerberos を使用して認証をサポートします。  

[詳細については、Kerberos キー信頼 (&)、ドメイン参加済みデバイスのパブリック キーのサポートは](https://technet.microsoft.com/windows-server-docs/security/kerberos/whats-new-in-kerberos-authentication)します。

### <a name="pkinit-freshness-extension-support"></a>PKINIT 鮮度拡張機能のサポート

Kerberos クライアントは、Windows 10 バージョン 1507、Windows Server 2016 以降のパブリック キーに基づいてサインオン PKInit 鮮度の拡張機能を試みます。 

Windows Server 2016 以降、Kdc は PKInit 鮮度の拡張機能をサポートできます。  既定では、Kdc は PKInit 鮮度の拡張機能が提供されません。 

[PKINIT 鮮度の拡張機能のサポートの詳細について](https://technet.microsoft.com/windows-server-docs/security/kerberos/whats-new-in-kerberos-authentication)します。

### <a name="rolling-public-key-only-users-ntlm-secrets"></a>公開キーのみのユーザーの NTLM の機密情報のローリング

公開キーのみユーザーの NTLM の機密情報のローリング以降 Windows Server 2016 ドメインの機能レベル (DFL) では、Dc をサポートできます。 この機能は、低い DFLs でなシャーシファンです。

> [!WARNING] 
> NTLM の機密情報が、DC で更新されました、少なくとも 2016 年 11 月 8 日の実行にサービスを提供する前に有効になっている DC のクラッシュのリスクをローリングとドメインにドメイン コント ローラーを追加します。 

構成:新しいドメインの場合は、この機能は既定で有効にします。 既存のドメインの Active Directory 管理センターで構成する必要があります。 

1. Active Directory 管理センターから、左側のウィンドウでドメインを右クリックして**プロパティ**します。

    ![ドメインのプロパティ](../media/Credentials-Protection-And-Management/domain-properties.png)
    
2. 選択**対話型ログオンに Microsoft Passport またはスマート カードを使用する必要のあるユーザーをサインアップ時に NTLM シークレットが期限切れ間近の導入にする**します。

    ![NTLM シークレットの有効期限が切れる Autoroll](../media/Credentials-Protection-And-Management/autoroll-ntlm.png)

3. **[OK]** をクリックします。 

### <a name="allowing-network-ntlm-when-user-is-restricted-to-specific-domain-joined-devices"></a>ユーザーが特定のドメインに参加しているデバイスに制限されていると、ネットワーク NTLM を許可します。

以降の Windows Server 2016 ドメインの機能レベル (DFL) Dc は、ユーザーがドメインに参加しているデバイスの特定の場所に制限されている場合、許可するネットワーク NTLM をサポートできます。 この機能は、低い DFLs でご利用いただけません。

構成:認証ポリシーでは、次のようにクリックします。**に制限されます。 ときにネットワーク認証が NTLM を許可するには、デバイスが選択されている**します。 

[詳細については、認証ポリシーは](https://technet.microsoft.com/windows-server-docs/security/credentials-protection-and-management/authentication-policies-and-authentication-policy-silos)します。
