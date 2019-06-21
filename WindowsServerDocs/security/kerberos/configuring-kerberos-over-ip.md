---
title: IP アドレス用の Kerberos の構成
description: Spn の IP ベースの Kerberos サポート
ms.openlocfilehash: aa2685fcff2fdf231e5e5884d25885585f0bd6c9
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67279965"
---
# <a name="kerberos-clients-allow-ipv4-and-ipv6-address-hostnames-in-service-principal-names-spns"></a>Kerberos クライアントがサービス プリンシパル名 (Spn) で IPv4 と IPv6 アドレスのホスト名を許可します。

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

Windows 10 バージョン 1507 と Windows Server 2016 以降では、Kerberos クライアントが Spn で IPv4 と IPv6 のホスト名をサポートするために構成できます。

既定では、ホスト名が IP アドレスの場合、Windows は、ホストでの Kerberos 認証をしません。 これがフォールバックして NTLM のような場合は、その他の有効な認証プロトコルです。 ただし、アプリケーションは、アプリケーションはハードコーディングされた IP アドレスを使用するは NTLM にフォールバックされ、Kerberos を使用しない場合があります。 NTLM が無効にする環境の移動と、互換性問題が発生することができます。

NTLM の新機能を無効にする影響を軽減するには、導入された管理者はサービス プリンシパル名のホスト名として IP アドレスを使用します。 この機能は、レジストリ キーの値を使用してクライアントで有効にします。

```cmd
reg add "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\Kerberos\Parameters" /v TryIPSPN /t REG_DWORD /d 1 /f
```

Spn の IP アドレスのホスト名のサポートを構成するには、TryIPSPN エントリを作成します。 既定では、このエントリはレジストリに存在しません。 エントリを作成した後は、DWORD 値を 1 に変更します。 このレジストリ値は、IP アドレスで Kerberos で保護されたリソースにアクセスする必要がある各クライアント コンピューターに設定する必要があります。

## <a name="configuring-a-service-principal-name-as-ip-address"></a>サービス プリンシパル名を IP アドレスとして構成します。

サービス プリンシパル名は、ネットワーク上のサービスを識別するために、Kerberos 認証時に使用される一意の識別子です。 SPN が、サービス、ホスト名、および必要に応じて、ポートの形式で成る`service/hostname[:port]`など`host/fs.contoso.com`します。 コンピューターが Active Directory に参加しているときに、Windows はコンピューター オブジェクトに複数の Spn を登録します。

IP アドレスは、多くの場合、一時的なため、IP アドレスは通常のホスト名の代わりに使用されません。 これには、アドレスのリースは有効期限が切れるし、更新の競合および認証の失敗につながることができます。 IP アドレス ベースの SPN を登録するため、手動のプロセスし、DNS ベースのホスト名に切り替えることはできませんがある場合にのみ使用する必要があります。

推奨方法が使用するには、 [Setspn.exe](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc731241(v=ws.11))ツール。 SPN できますのみ登録することを Active Directory で単一のアカウント、一度にため DHCP を使用する場合、IP アドレスが静的なリースがあることをお勧めに注意してください。

```
Setspn -s <service>/ip.address> <domain-user-account>  
```

以下に例を示します。

```
Setspn -s host/192.168.1.1 server01
```
