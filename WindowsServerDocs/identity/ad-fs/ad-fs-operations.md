---
ms.assetid: eefcc989-8763-45ee-8a64-3a97b4397160
title: AD FS の運用
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 2db9cd83ed08673835a38e443e90c5eb092f43ac
ms.sourcegitcommit: b649047f161cb605df084f18b573f796a584753b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/17/2020
ms.locfileid: "76162483"
---
# <a name="ad-fs-operations"></a>AD FS の運用



このドキュメントには、AD FS のすべてのドキュメント操作の一覧が含まれています。 

## <a name="service-configuration"></a>サービス構成
- [AD FS と WAP 2016 で SSL 証明書を更新する](../ad-fs/operations/Manage-SSL-Certificates-AD-FS-WAP-2016.md)
- [AD FS の迅速な復元ツール](../ad-fs/operations/AD-FS-Rapid-Restore-Tool.md)
- [AD FS で証明書認証の代替ホスト名バインドを構成する](../ad-fs/operations/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication.md)
- [属性ストアを追加する](../ad-fs/operations/Add-an-Attribute-Store.md)
- [AD FS 2019 で HTTP セキュリティ応答ヘッダーをカスタマイズする](../ad-fs/operations/customize-http-security-headers-ad-fs.md)
- [管理者以外のユーザーへの AD FS Powershell コマンドレットのアクセスの委任](../ad-fs/operations/delegate-ad-fs-pshell-access.md)
- [SQL とアドレスの待機時間の微調整](../ad-fs/operations/adfs-sql-latency.md)
- [AlwaysOn 可用性グループ](../ad-fs/operations/ad-fs-always-on.md) 


## <a name="authentication-configuration"></a>認証の構成
### <a name="strong-authentication-mfa--password-less"></a>強力な認証 (MFA) & パスワードレス
- [AD FS (2019 以降) で、外部認証プロバイダーをプライマリとして構成する](../ad-fs/operations/Additional-Authentication-Methods-AD-FS.md)
- [AD FS (2016 以降) と Azure MFA を構成する](../ad-fs/operations/Configure-AD-FS-2016-and-Azure-MFA.md)
- [AD FS の追加の認証方法を構成する](../ad-fs/operations/Configure-Additional-Authentication-Methods-for-AD-FS.md)

### <a name="lockout-protection"></a>ロックアウトの保護
- [AD FS エクストラネット ソフト ロックアウト保護を構成する](../ad-fs/operations/Configure-AD-FS-Extranet-Soft-Lockout-Protection.md)
- [AD FS エクストラネット スマート ロックアウト保護を構成する](../ad-fs/operations/Configure-AD-FS-Extranet-Smart-Lockout-Protection.md)
- [AD FS エクストラネット禁止 IP を構成する](../ad-fs/operations/Configure-AD-FS-Banned-IP.md)

### <a name="policy-configuration"></a>ポリシーの構成
- [認証ポリシーを構成する](../ad-fs/operations/Configure-Authentication-Policies.md)
- [代替ログイン ID を構成する](../ad-fs/operations/Configuring-Alternate-Login-ID.md)
- [AD FS ポリシーで動作するように Azure AD プロンプトのログイン動作を構成する](../ad-fs/operations/AD-FS-Prompt-Login.md)

### <a name="kerberos--certificate-authentication"></a>Kerberos & 証明書認証
- [AD FS で AD DS 要求 & kerberos 複合認証を有効にする](../ad-fs/operations/AD-FS-Compound-Authentication-and-AD-DS-claims.md)
- [ユーザー証明書の認証用に AD FS を構成する](../ad-fs/operations/Configure-User-Certificate-Authentication.md)
- [AD FS で証明書認証の代替ホスト名バインドを構成する](../ad-fs/operations/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication.md)


### <a name="device"></a>デバイス
- [AD FS のデバイス認証コントロール](../ad-fs/operations/device-authentication-controls-in-AD-FS.md) 


## <a name="authorization-configuration"></a>承認の構成
- [AD FS で Access Control ポリシーを構成する](../ad-fs/operations/Access-Control-Policies-in-AD-FS.md)
- [オンプレミスのデバイス ベースの条件付きアクセスを構成する](../ad-fs/operations/Configure-Device-based-Conditional-Access-on-Premises.md)

## <a name="rpt--cpt-configuration"></a>RPT & CPT 構成
- [LDAP ディレクトリに保存されたユーザーを認証するように AD FS を構成する](../ad-fs/operations/Configure-AD-FS-to-authenticate-users-stored-in-LDAP-directories.md)
- [要求規則を構成する](../ad-fs/operations/Configure-Claim-Rules.md) 
- [要求プロバイダー信頼を作成する](../ad-fs/operations/Create-a-Claims-Provider-Trust.md) 
- [要求対応ではない証明書利用者信頼を作成する](../ad-fs/operations/Create-a-Non-Claims-Aware-Relying-Party-Trust.md)
- [証明書利用者の信頼を作成する](../ad-fs/operations/Create-a-Relying-Party-Trust.md)
- [集計されたフェデレーションプロバイダーを使用するように AD FS を構成する (例: Common)](../ad-fs/operations/Improved-interoperability-with-SAML-2.0.md)

## <a name="sign-in-experience-configuration"></a>サインインエクスペリエンスの構成
- [AD FS 2016 のシングルサインオン設定を構成する](../ad-fs/operations/AD-FS-2016-Single-Sign-On-Settings.md)
- [改ページ調整されたサインインの構成 AD FS](../ad-fs/operations/AD-FS-paginated-sign-in.md)
- [AD FS ユーザーサインインのカスタマイズを構成する](../ad-fs/operations/AD-FS-user-sign-in-customization.md)
- [パスワードの有効期限クレームを送信するように AD FS を構成する](../ad-fs/operations/Configure-AD-FS-to-Send-Password-Expiry-Claims.md)
- [WIA をサポートしないデバイス用にイントラネット フォーム ベースの認証を構成する](../ad-fs/operations/Configure-intranet-forms-based-authentication-for-devices-that-do-not-support-WIA.md)

## <a name="other"></a>Other
- [任意のデバイスからの職場への参加による業務用アプリケーション間の SSO とシームレスな 2 要素認証](../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)
- [追加の多要素認証による個人情報アプリケーションのリスク管理](../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)
- [条件付きアクセス制御によってリスクを管理する](../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md)
- [AD FS ラボ環境を設定する](../ad-fs/operations/Set-up-an-AD-FS-lab-environment.md)
- [チュートリアルガイド: 追加の Multi-Factor Authentication による機密アプリケーションのリスク管理](../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)
- [チュートリアルガイド: 条件付き Access Control によるリスク管理](../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md)
- [チュートリアル: Windows デバイスでの Workplace Join](../ad-fs/operations/Walkthrough--Workplace-Join-with-a-Windows-Device.md)
- [チュートリアル: iOS デバイスでの Workplace Join](../ad-fs/operations/Walkthrough--Workplace-Join-with-an-iOS-Device.md)

  


