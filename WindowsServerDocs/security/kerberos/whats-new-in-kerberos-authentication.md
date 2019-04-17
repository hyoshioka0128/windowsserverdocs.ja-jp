---
title: "Kerberos 認証の新機能"
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 7bd17803-6e42-4a3b-803f-e47c74725813
manager: alanth
author: justinha
ms.technology: security-authentication
ms.date: 11/09/2016
ms.openlocfilehash: 7b046490c606cdf9e1436f503bf46a9cd4280ea9
ms.sourcegitcommit: 2782a80a916f8432c030af76e860a72f08481899
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2018
---
# <a name="whats-new-in-kerberos-authentication"></a>Kerberos 認証の新機能

>適用対象: Windows Server 2016 および Windows 10

## <a name="kdc-support-for-public-key-trust-based-client-authentication"></a>公開キーを信頼ベースのクライアント認証の KDC のサポート

Windows Server 2016 以降、Kdc は、公開キーのマッピングの方法をサポートします。 アカウントの公開キーがプロビジョニングされた場合、KDC はそのキーを使用して明示的に Kerberos をサポートします。 証明書の検証がないため、自己署名証明書がサポートされているし、認証メカニズム保証がサポートされていません。

UseSubjectAltName 設定に関係なく、アカウントの構成されている場合、キーの信頼が適しています。

## <a name="kerberos-client-and-kdc-support-for-rfc-8070-pkinit-freshness-extension"></a>RFC 8070 を鮮度拡張機能の Kerberos クライアントと KDC のサポートします。

Windows 10 バージョン 1607 および Windows Server 2016 以降では、Kerberos クライアントと、[RFC 8070 を鮮度拡張子](https://datatracker.ietf.org/doc/draft-ietf-kitten-pkinit-freshness/)公開キー ベースのサインオンします。 

Windows Server 2016 以降、Kdc を鮮度拡張機能をサポートできます。 既定では、Kdc を鮮度拡張機能は提供されません。 これを有効にするには、ドメイン内のすべての Dc 上を鮮度拡張子の KDC 管理用テンプレート ポリシー設定の新しい KDC のサポートを使用します。 構成すると、ドメインが Windows Server 2016 ドメインの機能レベル (DFL) に、次のオプションがサポートされます。

- **無効になっている**: [KDC を鮮度拡張機能を提供して確認鮮度をせずに有効な認証要求を受け入れることはありません。 ユーザーは、新しい公開キー ID SID を決して表示されます。
- **サポートされている**: で要求を鮮度拡張機能はサポートされています。 鮮度拡張子を持つ認証が成功する Kerberos クライアントでは、新しい公開キー ID SID を受け取ります。
- **必要な**: を鮮度拡張子は認証が成功したために必要です。 鮮度拡張機能をサポートしていない Kerberos クライアントは公開キーの資格情報を使用するときに常に失敗します。

## <a name="domain-joined-device-support-for-authentication-using-public-key"></a>公開キーを使用して認証のドメインに参加しているデバイスのサポート

以降で Windows 10 バージョン 1507 および Windows Server 2016 では、ドメインに参加しているデバイスが Windows Server 2016 ドメイン コントローラー (DC) でバインドされているその公開キーを登録できる場合、デバイス認証できる Windows Server 2016 の DC を Kerberos 認証を使用して公開キーを持つ。 詳細については、次を参照してください[デバイスの公開キー認証をドメインに参加している。](Domain-joined-Device-Public-Key-Authentication.md)

## <a name="kerberos-clients-allow-ipv4-and-ipv6-address-hostnames-in-service-principal-names-spns"></a>Kerberos クライアントは、サービス プリンシパル名 (SPN) で IPv4 と IPv6 アドレスのホスト名を許可します。

Windows 10 バージョン 1507 および Windows Server 2016 以降では、Kerberos クライアントは、SPN の IPv4 と IPv6 のホスト名をサポートするために構成できます。 

レジストリのパス:

HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\Kerberos\Parameters

SPN の IP アドレスのホスト名のサポートを構成するには、TryIPSPN エントリを作成します。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後、DWORD 値を 1 に変更します。 構成しなかった場合、IP アドレスのホスト名は行われません。

Active Directory の SPN が登録されている、kerberos 認証が成功しました。 

## <a name="kdc-support-for-key-trust-account-mapping"></a>KDC でキーの信頼アカウントへのマッピングをサポートします。

Windows Server 2016 以降では、ドメイン コントローラーは、SAN の動作にフォールバックする既存の AltSecID およびユーザー プリンシパル名 (UPN) とキーの信頼アカウントへのマッピングがサポートされています。 UseSubjectAltName に設定すると。

- 0: 明示的なマッピングが必要です。 必要になりますか。
    - (Windows Server 2016) で新しいキーを信頼
    - ExplicitAltSecID
- 1: 暗黙的なマッピングが (既定) を許可します。
    1. アカウントのキーの信頼を構成し、それが使用マッピングの (Windows Server 2016 の新機能) されます。
    2. SAN の UPN がない場合は、マッピングの AltSecID が試行されます。
    3. SAN に UPN がある場合は、マッピングの UPN が試行されました。

## <a name="see-also"></a>参照してください。

- [Kerberos 認証の概要](kerberos-authentication-overview.md)
