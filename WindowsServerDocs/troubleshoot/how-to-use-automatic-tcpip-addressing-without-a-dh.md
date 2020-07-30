---
title: DHCP サーバーなしで TCP/IP 自動アドレス指定を使用する方法
description: DHCP サーバーなしで TCP/IP の自動アドレス指定を使用する方法について説明します。
ms.prod: windows-server
manager: dcscontentpm
ms.technology: server-general
ms.date: 5/26/2020
ms.topic: troubleshoot
author: Deland-Han
ms.author: delhan
ms.reviewer: robsmi
ms.openlocfilehash: fcd85c29975709053009ec4a2684df88b4bafd69
ms.sourcegitcommit: 145cf75f89f4e7460e737861b7407b5cee7c6645
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87409803"
---
# <a name="how-to-use-automatic-tcpip-addressing-without-a-dhcp-server"></a>DHCP サーバーなしで TCP/IP 自動アドレス指定を使用する方法

この記事では、動的ホスト構成プロトコル (DHCP) サーバーがネットワーク上に存在しない状態で、自動伝送制御プロトコル/インターネットプロトコル (TCP/IP) アドレス指定を使用する方法について説明します。 この記事の「適用対象」セクションに記載されているオペレーティングシステムのバージョンには、自動プライベート IP アドレス指定 (APIPA) と呼ばれる機能があります。 この機能を使用すると、DHCP サーバーが使用できない場合、またはネットワーク上に存在しない場合に、Windows コンピューターがそれ自体をインターネットプロトコル (IP) アドレスとして割り当てることができます。 この機能により、TCP/IP を実行する小規模なローカルエリアネットワーク (LAN) の構成とサポートが困難になります。

## <a name="more-information"></a>詳細情報

> [!IMPORTANT]
> 慎重にこのセクションの手順に従います。 レジストリを正しく変更しないと、重大な問題が発生する可能性があります。 変更する前に、問題が発生した場合に[復元するためにレジストリをバックアップ](https://support.microsoft.com/help/322756)します。

Dhcp を使用するように構成されている Windows ベースのコンピューターは、DHCP サーバーが使用できない場合は、インターネットプロトコル (IP) アドレスを自動的に割り当てることができます。 たとえば、DHCP サーバーを使用しないネットワークや、DHCP サーバーがメンテナンスのために一時的に停止しているネットワーク上で発生する可能性があります。

インターネット割り当て番号機関 (IANA) には、自動プライベート IP アドレス指定のための169.254.255.255 が予約されています。 その結果、APIPA は、ルーティング可能なアドレスと競合しないことが保証されたアドレスを提供します。

ネットワークアダプターに IP アドレスが割り当てられると、そのコンピューターは、TCP/IP を使用して、同じ LAN に接続されていて、APIPA 用に構成されている他のコンピューターと通信したり、IP アドレスを手動で 169.254. x. y に設定したりすることができます (ここで、x.y はクライアントの一意の識別子)。 コンピューターは、他のサブネット上のコンピューター、または自動プライベート IP アドレス指定を使用しないコンピューターと通信できないことに注意してください。 自動プライベート IP アドレス指定は、既定で有効になっています。

次のいずれかの場合に無効にすることができます。

- ネットワークでルーターを使用している。

- NAT またはプロキシサーバーを使用せずに、ネットワークがインターネットに接続されています。

Dhcp 関連のメッセージを無効にしていない限り、dhcp のアドレス指定と自動プライベート IP アドレス指定の間で変更を行うと、通知が表示されます。 DHCP メッセージングが誤って無効になっている場合は、次のレジストリキーの PopupFlag 値を00から01に変更することで、DHCP メッセージを再び有効にすることができます。`HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\VxD\DHCP`

変更を有効にするには、コンピューターを再起動する必要があることに注意してください。 また、Windows Millennium Edition、Windows 98、または Windows 98 Second Edition の Winipcfg ツールを使用して、コンピューターで APIPA が使用されているかどうかを確認することもできます。

[スタート]、[実行] の順にクリックし、「winipcfg」 (引用符なし) を入力して、[OK] をクリックします。 [詳細情報] をクリックします。 [IP 自動構成アドレス] ボックスに、169.254. x. x の範囲内の IP アドレスが含まれている場合は、自動プライベート IP アドレス指定が有効になります。 [IP アドレス] ボックスが存在する場合、自動プライベート IP アドレス指定は現在有効になっていません。
Windows 2000、Windows XP、または Windows Server 2003 では、コマンドプロンプトで IPconfig コマンドを使用して、コンピューターで APIPA が使用されているかどうかを確認できます。

[スタート]、[ファイル名を指定して実行] の順にクリックし、「cmd」と入力し (引用符は不要)、[OK] をクリックして MS-DOS コマンドラインウィンドウを開きます。 「Ipconfig/all」と入力し (引用符は除く)、ENTER キーを押します。 [自動構成を有効にする] 行に "Yes" と表示され、[自動構成の IP アドレス] が 169.254. x. y である場合 (x.y はクライアントの一意の識別子)、コンピューターでは APIPA が使用されています。 "自動構成を有効にする" 行に "いいえ" と表示されている場合、コンピューターは現在 APIPA を使用していません。
次のいずれかの方法を使用して、自動プライベート IP アドレス指定を無効にすることができます。

TCP/IP 情報を手動で構成して、DHCP を完全に無効にすることができます。 レジストリを編集することで、自動プライベート IP アドレス指定 (DHCP ではない) を無効にすることができます。 これを行うには、値0x0 を持つ "IPAutoconfigurationEnabled" DWORD レジストリエントリを、Windows Millennium Edition、Windows98、または Windows 98 Second Edition の次のレジストリキーに追加します。`HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\VxD\DHCP`

Windows 2000、Windows XP、および Windows Server 2003 の場合、APIPA を無効にするには、次のレジストリキーに値0x0 を持つ "IPAutoconfigurationEnabled" DWORD レジストリエントリを追加します。`HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Tcpip\Parameters\Interfaces\<Adapter GUID>`
> [!NOTE]
> **アダプターの GUID**サブキーは、コンピューターの LAN アダプターのグローバル一意識別子 (guid) です。

IPAutoconfigurationEnabled DWORD エントリに値1を指定すると、APIPA が有効になります。これは、レジストリからこの値を省略した場合の既定の状態です。

## <a name="examples-of-where-apipa-may-be-useful"></a>APIPA が役に立つ可能性のある例

### <a name="example-1-no-previous-ip-address-and-no-dhcp-server"></a>例 1: 以前の IP アドレスと DHCP サーバーがない

(DHCP 用に構成された) Windows ベースのコンピューターが初期化されると、3つ以上の "検出" メッセージをブロードキャストします。 複数の検出メッセージがブロードキャストされた後に DHCP サーバーが応答しない場合、Windows コンピューターはそれ自体をクラス B (APIPA) アドレスに割り当てます。 Windows コンピューターでは、コンピューターのユーザーにエラーメッセージが表示されます (過去に DHCP サーバーから IP アドレスが割り当てられていないことを示しています)。 Windows コンピューターは、DHCP サーバーとの通信を確立するために、3分ごとに検出メッセージを送信します。

### <a name="example-2-previous-ip-address-and-no-dhcp-server"></a>例 2: 以前の IP アドレスと DHCP サーバーがない

コンピューターが DHCP サーバーを確認し、存在しない場合は、既定のゲートウェイに接続しようとします。 既定のゲートウェイが応答する場合、Windows コンピューターは以前にリースされた IP アドレスを保持します。 ただし、コンピューターが既定のゲートウェイから応答を受信しない場合、または何も割り当てられていない場合は、自動プライベート IP アドレス指定機能を使用して自身に IP アドレスを割り当てます。 ユーザーに対してエラーメッセージが表示され、3分ごとにメッセージが送信されます。 DHCP サーバーがオンラインになると、DHCP サーバーとの通信が再確立されたことを示すメッセージが生成されます。

### <a name="example-3-lease-expires-and-no-dhcp-server"></a>例 3: リースの有効期限が切れ、DHCP サーバーがない

Windows ベースのコンピューターは、IP アドレスのリースを再確立しようとします。 Windows コンピューターが DCHP サーバーを検出しない場合は、エラーメッセージを生成した後に IP アドレスを割り当てます。 その後、コンピューターは4つの検出メッセージをブロードキャストし、5分ごとに DHCP サーバーがオンラインになるまで、手順全体を繰り返します。 次に、DHCP サーバーとの通信が再確立されたことを示すメッセージが生成されます。
