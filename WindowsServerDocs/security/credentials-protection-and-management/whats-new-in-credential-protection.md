---
title: 資格情報の保護の新機能
description: Windows Server のセキュリティ
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 2351be82ad1d8b9af17715ce363836f57c71ea66
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386911"
---
# <a name="whats-new-in-credential-protection"></a>資格情報の保護の新機能

## <a name="credential-guard-for-signed-in-user"></a>サインインしているユーザーの Credential Guard

Windows 10、バージョン1507、Kerberos、NTLM 以降では、仮想化ベースのセキュリティを使用して、サインインしているユーザーのログオンセッションの Kerberos & NTLM シークレットを保護します。 

Windows 10 バージョン1511以降では、資格情報マネージャーは、仮想化ベースのセキュリティを使用して、ドメイン資格情報の種類の保存された資格情報を保護します。 サインインした資格情報と保存されたドメインの資格情報は、リモートデスクトップを使用してリモートホストに渡されません。 Credential Guard は、UEFI ロックなしで有効にすることができます。

Windows 10 バージョン1607以降では、分離ユーザーモードは、Credential Guard の展開用に個別にインストールされないように、Hyper-v に含まれています。

[Credential Guard の詳細についてはこちらをご覧](https://technet.microsoft.com/itpro/windows/keep-secure/credential-guard)ください。


## <a name="remote-credential-guard-for-signed-in-user"></a>サインインしているユーザーのリモート Credential Guard

Windows 10 バージョン1607以降、remote Credential Guard は、クライアントデバイスで Kerberos および NTLM シークレットを保護することによって、リモートデスクトップを使用するときにサインインしているユーザーの資格情報を保護します。 リモートホストがネットワークリソースをユーザーとして評価するためには、クライアントデバイスでシークレットを使用する必要があります。

Windows 10 バージョン1703以降、remote Credential Guard は、リモートデスクトップを使用するときに、指定されたユーザー資格情報を保護します。

[詳細については、「Remote credential guard](https://technet.microsoft.com/itpro/windows/keep-secure/remote-credential-guard)」を参照してください。

## <a name="domain-protections"></a>ドメインの保護

ドメインの保護には Active Directory ドメインが必要です。

### <a name="domain-joined-device-support-for-authentication-using-public-key"></a>ドメインに参加しているデバイスで、公開キーを使用した認証がサポートされる

Windows 10 バージョン1507および Windows Server 2016 以降では、ドメインに参加しているデバイスが、バインドされた公開キーを Windows Server 2016 ドメインコントローラー (DC) に登録できる場合、デバイスは Kerberos PKINIT を使用して公開キーで認証できます。Windows Server 2016 DC に対する認証。

Windows Server 2016 以降では、Kdc は Kerberos キー信頼を使用した認証をサポートしています。  

[ドメイン参加済みデバイスの公開キーのサポートの詳細については & Kerberos キーの信頼」を参照して](https://technet.microsoft.com/windows-server-docs/security/kerberos/whats-new-in-kerberos-authentication)ください。

### <a name="pkinit-freshness-extension-support"></a>PKINIT 鮮度拡張機能のサポート

Windows 10、バージョン1507、および Windows Server 2016 以降では、Kerberos クライアントは公開キーベースのサインオンに対して PKInit 鮮度拡張機能を試行します。 

Windows Server 2016 以降では、Kdc は PKInit 鮮度拡張機能をサポートできます。  既定では、Kdc は PKInit 鮮度拡張機能を提供しません。 

[PKINIT 鮮度拡張機能のサポートの詳細について](https://technet.microsoft.com/windows-server-docs/security/kerberos/whats-new-in-kerberos-authentication)は、こちらを参照してください。

### <a name="rolling-public-key-only-users-ntlm-secrets"></a>公開キーのみのユーザーの NTLM シークレットをロールする

Windows Server 2016 のドメイン機能レベル (DFL) 以降では、Dc は公開キーのみのユーザーの NTLM シークレットのロールをサポートできます。 この機能は、下位の DFLs では機能しません。

> [!WARNING] 
> ローリング NTLM シークレットが有効になっているドメインにドメインコントローラーを追加すると、DC が少なくとも11月8日に更新される前に、2016サービスによって DC がクラッシュするリスクがあります。 

構成:新しいドメインの場合、この機能は既定で有効になっています。 既存のドメインの場合は、Active Directory 管理センターで構成する必要があります。 

1. Active Directory 管理センターで、左側のウィンドウのドメインを右クリックし、 **[プロパティ]** を選択します。

    ![ドメインのプロパティ](../media/Credentials-Protection-And-Management/domain-properties.png)

2. **対話型ログオンに Microsoft Passport またはスマートカードを使用する必要があるユーザーについては、[サインオン中に期限切れの NTLM シークレットを有効に**する] を選択します。

    ![Autoroll の有効期限が切れる NTLM シークレット](../media/Credentials-Protection-And-Management/autoroll-ntlm.png)

3. **[OK]** をクリックします。 

### <a name="allowing-network-ntlm-when-user-is-restricted-to-specific-domain-joined-devices"></a>ユーザーが特定のドメインに参加しているデバイスに制限されている場合にネットワーク NTLM を許可する

Windows Server 2016 のドメイン機能レベル (DFL) 以降では、ドメインに参加している特定のデバイスにユーザーが制限されている場合、Dc はネットワーク NTLM の許可をサポートできます。 この機能は、下位の DFLs では使用できません。

構成:[認証ポリシー] で、[**ユーザーが選択したデバイスに制限されている場合、NTLM ネットワーク認証を許可**する] をクリックします。 

[認証ポリシーの詳細についてはこちらをご覧](https://technet.microsoft.com/windows-server-docs/security/credentials-protection-and-management/authentication-policies-and-authentication-policy-silos)ください。
