---
title: What's New in Kerberos Authentication
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 7bd17803-6e42-4a3b-803f-e47c74725813
manager: alanth
author: justinha
ms.technology: security-authentication
ms.date: 11/09/2016
ms.openlocfilehash: a0916abf1076b5f791a856f0c85f54ad17f6d64c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403477"
---
# <a name="whats-new-in-kerberos-authentication"></a>What's New in Kerberos Authentication

>適用先:Windows Server 2016 と Windows 10

## <a name="kdc-support-for-public-key-trust-based-client-authentication"></a>KDC による公開キーの信頼ベースのクライアント認証のサポート

Windows Server 2016 以降では、Kdc は公開キーマッピングの方法をサポートしています。 公開キーがアカウントに対してプロビジョニングされている場合、KDC はそのキーを使用して明示的に Kerberos PKInit をサポートします。 証明書の検証は行われないため、自己署名証明書はサポートされており、認証メカニズムの保証はサポートされていません。

キーの信頼は、UseSubjectAltName の設定に関係なく、アカウントに対して構成する場合に推奨されます。

## <a name="kerberos-client-and-kdc-support-for-rfc-8070-pkinit-freshness-extension"></a>Kerberos クライアントと KDC での RFC 8070 の PKInit 鮮度拡張機能のサポート

Windows 10、バージョン1607、および Windows Server 2016 以降では、Kerberos クライアントは、公開キーベースのサインオンに対して[RFC 8070 の PKInit 鮮度拡張機能](https://datatracker.ietf.org/doc/draft-ietf-kitten-pkinit-freshness/)を試行します。 

Windows Server 2016 以降では、Kdc は PKInit 鮮度拡張機能をサポートできます。 既定では、Kdc は PKInit 鮮度拡張機能を提供しません。 有効にするには、ドメイン内のすべての Dc に対して、[PKInit 鮮度拡張機能の kdc] 管理用テンプレートポリシー設定の新しい KDC サポートを使用します。 構成した場合、ドメインが Windows Server 2016 ドメインの機能レベル (DFL) の場合、次のオプションがサポートされます。

- **Disabled**:KDC は、PKInit 鮮度拡張機能を提供しません。また、有効な認証要求を受け入れるかどうかをチェックしません。 ユーザーは、新しい公開キー id SID を受け取ることはありません。
- **サポートされている**:要求では、PKInit 鮮度拡張機能がサポートされています。 PKInit 鮮度拡張機能を使用して正常に認証された Kerberos クライアントは、新しい公開キー id SID を受け取ります。
- **必須**:認証を成功させるには、PKInit 鮮度拡張機能が必要です。 PKInit 鮮度拡張機能をサポートしていない Kerberos クライアントは、公開キーの資格情報を使用すると、常に失敗します。

## <a name="domain-joined-device-support-for-authentication-using-public-key"></a>ドメインに参加しているデバイスで、公開キーを使用した認証がサポートされる

Windows 10 バージョン1507および Windows Server 2016 以降では、ドメインに参加しているデバイスが、バインドされた公開キーを Windows Server 2016 ドメインコントローラー (DC) に登録できる場合、デバイスは Kerberos 認証を使用して公開キーで認証を行うことができます。Windows Server 2016 DC。 詳細については、「ドメインに参加している[デバイスの公開キーの認証](Domain-joined-Device-Public-Key-Authentication.md)」を参照してください。

## <a name="kerberos-clients-allow-ipv4-and-ipv6-address-hostnames-in-service-principal-names-spns"></a>Kerberos クライアントは、サービスプリンシパル名 (Spn) で IPv4 および IPv6 アドレスのホスト名を許可します。

Windows 10 バージョン1507および Windows Server 2016 以降では、Spn の IPv4 および IPv6 ホスト名をサポートするように Kerberos クライアントを構成できます。 

レジストリパス:

HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\Kerberos\Parameters

Spn で IP アドレスのホスト名のサポートを構成するには、TryIPSPN エントリを作成します。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後、DWORD 値を1に変更します。 構成されていない場合、IP アドレスのホスト名は試行されません。

SPN が Active Directory に登録されている場合、認証は Kerberos で成功します。 

詳細については、 [IP アドレスの Kerberos の構成](configuring-kerberos-over-ip.md)に関するドキュメントを参照してください。

## <a name="kdc-support-for-key-trust-account-mapping"></a>KDC でのキー信頼アカウントマッピングのサポート

Windows Server 2016 以降では、ドメインコントローラーは、キー信頼アカウントマッピングをサポートしています。また、SAN 動作の既存の AltSecID とユーザープリンシパル名 (UPN) へのフォールバックもサポートされています。 UseSubjectAltName がに設定されている場合:

- 0明示的なマッピングが必要です。 次のいずれかが必要です。
    - キー信頼 (Windows Server 2016 での新)
    - ExplicitAltSecID
- 1:暗黙的なマッピングは許可されています (既定)。
    1. キー信頼がアカウントに対して構成されている場合は、マッピングに使用されます (Windows Server 2016 で新規)。
    2. SAN に UPN がない場合は、マッピングのために AltSecID が試行されます。
    3. SAN に UPN がある場合は、マッピングのために UPN が試行されます。

## <a name="see-also"></a>関連項目

- [Kerberos 認証の概要](kerberos-authentication-overview.md)
