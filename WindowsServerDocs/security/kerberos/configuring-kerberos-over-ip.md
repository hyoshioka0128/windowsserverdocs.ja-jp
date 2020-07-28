---
title: IP アドレスの Kerberos を構成しています
description: IP ベースの Spn に対する Kerberos のサポート
author: daveba
ms.author: daveba
ms.openlocfilehash: 16feb7045508a854657834fcbb4ab850f9b8ac3b
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87181918"
---
# <a name="kerberos-clients-allow-ipv4-and-ipv6-address-hostnames-in-service-principal-names-spns"></a>Kerberos クライアントは、サービスプリンシパル名 (Spn) で IPv4 および IPv6 アドレスのホスト名を許可します。

>適用先:Windows Server (半期チャネル)、Windows Server 2016

Windows 10 バージョン1507および Windows Server 2016 以降では、Spn の IPv4 および IPv6 ホスト名をサポートするように Kerberos クライアントを構成できます。

既定では、ホスト名が IP アドレスの場合、Windows はホストの Kerberos 認証を試行しません。 NTLM などの有効な認証プロトコルにフォールバックされます。 ただし、アプリケーションは IP アドレスを使用するようにハードコードされている場合があります。これは、アプリケーションが NTLM にフォールバックし、Kerberos を使用しないことを意味します。 このため、環境の移行時に NTLM を無効にすると、互換性の問題が発生する可能性があります。

NTLM を無効にした場合の影響を軽減するために、管理者がサービスプリンシパル名で IP アドレスをホスト名として使用できるようにする新機能が導入されました。 この機能は、レジストリキー値を使用してクライアントで有効になっています。

```cmd
reg add "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\Kerberos\Parameters" /v TryIPSPN /t REG_DWORD /d 1 /f
```

Spn で IP アドレスのホスト名のサポートを構成するには、TryIPSPN エントリを作成します。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後、DWORD 値を1に変更します。 このレジストリ値は、Kerberos で保護されているリソースに IP アドレスでアクセスする必要がある各クライアントコンピューターで設定する必要があります。

## <a name="configuring-a-service-principal-name-as-ip-address"></a>IP アドレスとしてのサービスプリンシパル名の構成

サービスプリンシパル名は、Kerberos 認証時にネットワーク上のサービスを識別するために使用される一意の識別子です。 SPN は、サービス、ホスト名、およびオプションで、などの形式のポートで構成され `service/hostname[:port]` `host/fs.contoso.com` ます。 コンピューターが Active Directory に参加している場合、Windows は複数の Spn をコンピューターオブジェクトに登録します。

通常、ip アドレスは一時的なものであるため、ホスト名の代わりに IP アドレスを使用することはできません。 アドレスリースの有効期限が切れ、更新されると、競合と認証エラーが発生する可能性があります。 したがって、IP アドレスベースの SPN の登録は手動で行う必要があるため、DNS ベースのホスト名に切り替えることができない場合にのみ使用してください。

[Setspn.exe](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc731241(v=ws.11))ツールを使用することをお勧めします。 SPN は一度に Active Directory の1つのアカウントにしか登録できないことに注意してください。 DHCP を使用する場合は、IP アドレスに静的リースを使用することをお勧めします。

```
Setspn -s <service>/ip.address> <domain-user-account>
```

例:

```
Setspn -s host/192.168.1.1 server01
```
