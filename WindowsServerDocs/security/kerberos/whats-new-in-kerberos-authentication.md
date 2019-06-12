---
title: Kerberos 認証の新機能新機能
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 7bd17803-6e42-4a3b-803f-e47c74725813
manager: alanth
author: justinha
ms.technology: security-authentication
ms.date: 11/09/2016
ms.openlocfilehash: 90107bd49268f232fd6d532c304c2fdd050bcbf5
ms.sourcegitcommit: c6acac3622e5d34714ca5c569805931681f98779
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/30/2019
ms.locfileid: "66391506"
---
# <a name="whats-new-in-kerberos-authentication"></a>What's New in Kerberos Authentication

>適用先:Windows Server 2016 および Windows 10

## <a name="kdc-support-for-public-key-trust-based-client-authentication"></a>公開キー信頼に基づいたクライアントの認証の KDC のサポート

Windows Server 2016 以降、Kdc はパブリック キー マッピングの方法をサポートします。 アカウントの公開キーがプロビジョニングされると、KDC は明示的にそのキーを使用して Kerberos PKInit をサポートします。 証明書の検証がないため、自己署名証明書がサポートされているし、認証メカニズム保証がサポートされていません。

キー信頼が UseSubjectAltName 設定に関係なく、アカウントに対して構成されている場合に適しています。

## <a name="kerberos-client-and-kdc-support-for-rfc-8070-pkinit-freshness-extension"></a>RFC 8070 PKInit 鮮度の拡張機能の Kerberos クライアントと KDC のサポートします。

以降、Windows 10、バージョン 1607 および Windows Server 2016 では、Kerberos クライアントと、 [RFC 8070 PKInit 鮮度拡張子](https://datatracker.ietf.org/doc/draft-ietf-kitten-pkinit-freshness/)公開キー ベースのサインオンします。 

Windows Server 2016 以降、Kdc は PKInit 鮮度の拡張機能をサポートできます。 既定では、Kdc では、PKInit 鮮度の拡張機能は提供されません。 有効にするには、ドメイン内のすべての Dc で PKInit 鮮度拡張子の KDC 管理用テンプレート ポリシー設定の新しい KDC のサポートを使用します。 構成すると、ドメインが Windows Server 2016 ドメインの機能レベル (DFL) に、次のオプションがサポートされます。

- **Disabled**:ありません、KDC は PKInit 鮮度の拡張機能を提供し、鮮度をチェックせず、有効な認証要求を受け入れます。 ユーザーには、新しいパブリック キー id の SID は受け取りません。
- **サポートされている**:PKInit 鮮度の拡張機能は、要求でサポートされます。 PKInit 鮮度の拡張機能を使用した認証が正常に Kerberos クライアントでは、新しいパブリック キー id の SID を受け取ります。
- **必須**:PKInit 鮮度の拡張機能は、認証が成功に必要です。 パブリック キーの資格情報を使用する場合、PKInit 鮮度の拡張機能をサポートしていない Kerberos クライアントは常に失敗します。

## <a name="domain-joined-device-support-for-authentication-using-public-key"></a>ドメインに参加しているデバイスで公開キーを使用する認証のサポート

以降では、Windows 10 バージョン 1507、Windows Server 2016 ではドメインに参加しているデバイスが Windows Server 2016 ドメイン コント ローラー (DC) にバインドされている公開キーを登録できない場合、デバイスで認証できる Kerberos 認証を使用して、公開キーWindows Server 2016 の DC です。 詳細については、次を参照してください[デバイスの公開キー認証をドメインに参加している。](Domain-joined-Device-Public-Key-Authentication.md)

## <a name="kerberos-clients-allow-ipv4-and-ipv6-address-hostnames-in-service-principal-names-spns"></a>Kerberos クライアントがサービス プリンシパル名 (Spn) で IPv4 と IPv6 アドレスのホスト名を許可します。

Windows 10 バージョン 1507 と Windows Server 2016 以降では、Kerberos クライアントが Spn で IPv4 と IPv6 のホスト名をサポートするために構成できます。 

レジストリ パス:

HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\Kerberos\Parameters

Spn の IP アドレスのホスト名のサポートを構成するには、TryIPSPN エントリを作成します。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後は、DWORD 値を 1 に変更します。 構成されていない場合は、IP アドレスのホスト名は行われません。

Active Directory で、SPN を登録すると、Kerberos と認証が成功しました。 

詳細については、ドキュメントをご覧ください[の IP アドレスを構成する Kerberos](configuring-kerberos-over-ip.md)します。

## <a name="kdc-support-for-key-trust-account-mapping"></a>KDC キー信頼アカウントのマッピングをサポートします。

Windows Server 2016 以降では、ドメイン コント ローラーは、キー信頼アカウント マッピングに加えて、SAN の動作で既存の AltSecID およびユーザー プリンシパル名 (UPN) にフォールバックをサポートがあります。 UseSubjectAltName に設定するとします。

- 0:明示的なマッピングが必要です。 必要になりますか。
    - (Windows Server 2016) で新しいキーを信頼
    - ExplicitAltSecID
- 1:暗黙的なマッピングを許可します (既定)。
    1. アカウントの構成キーを信頼する場合には使用のマッピング (Windows Server 2016 の新機能)。
    2. SAN 内に UPN がない場合は、マッピングの AltSecID が試行されます。
    3. SAN に UPN がある場合は、マッピングの UPN が試行されます。

## <a name="see-also"></a>関連項目

- [Kerberos 認証の概要](kerberos-authentication-overview.md)
