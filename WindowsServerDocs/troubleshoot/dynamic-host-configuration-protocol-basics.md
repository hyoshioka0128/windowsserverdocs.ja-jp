---
title: DHCP (動的ホスト構成プロトコル) の基本
description: ''
ms.prod: windows-server
manager: dcscontentpm
ms.technology: server-general
ms.date: 5/26/2020
ms.topic: troubleshoot
author: Deland-Han
ms.author: delhan
ms.reviewer: ''
ms.openlocfilehash: 5a3247fad961f4b2d1cf6e354c29706708c8e330
ms.sourcegitcommit: 145cf75f89f4e7460e737861b7407b5cee7c6645
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87409813"
---
# <a name="dhcp-dynamic-host-configuration-protocol-basics"></a>DHCP (動的ホスト構成プロトコル) の基本

動的ホスト構成プロトコル (DHCP) は RFC 1541 によって規定された標準プロトコルであり、rfc 2131 に置き換えられています。これにより、サーバーは、IP アドレスと構成情報を動的にクライアントに配布できるようになります。 通常、DHCP サーバーは、少なくとも次の基本情報をクライアントに提供します。

- IP アドレス

- [サブネット マスク]

- 既定の GatewayOther 情報は、ドメインネームサービス (DNS) サーバーアドレスや Windows インターネットネームサービス (WINS) サーバーのアドレスなど、指定することもできます。 システム管理者は、クライアントに解析されるオプションを使用して DHCP サーバーを構成します。

## <a name="more-information"></a>詳細情報

次の Microsoft 製品では、DHCP クライアント機能を提供しています。

- Windows NT Server バージョン3.5、3.51、および4.0

- Windows NT Workstation バージョン3.5、3.51、および4.0

- Windows 95

- MS-DOS 用 Microsoft ネットワーククライアントバージョン3.0

- Microsoft LAN Manager クライアントバージョン 2.2 c for MS-DOS

- Microsoft TCP/IP-32 for Windows for Windows for Windows バージョン3.11、3.11 a、および 3.11 b

Dhcp クライアントは、DHCP サーバーから受信できるさまざまなオプションをサポートしています。

次の Microsoft サーバーオペレーティングシステムでは、DHCP サーバーの機能を提供しています。

- Windows NT Server バージョン3.5

- Windows NT Server バージョン3.51

- Windows NT Server バージョン4.0

クライアントが DHCP 情報を受信するように構成された後に初めて初期化されると、サーバーとのメッセージ交換が開始されます。

次に示すのは、クライアントとサーバー間のメッセージ交換の概要テーブルであり、その後にプロセスのパケットレベルの説明が続きます。

```
Source Dest Source Dest Packet
 MAC addr MAC addr IP addr IP addr Description
 -----------------------------------------------------------------
 Client Broadcast 0.0.0.0 255.255.255.255 DHCP Discover
 DHCPsrvr Broadcast DHCPsrvr 255.255.255.255 DHCP Offer
 Client Broadcast 0.0.0.0 255.255.255.255 DHCP Request
 DHCPsrvr Broadcast DHCPsrvr 255.255.255.255 DHCP ACK
```

DHCP クライアントと DHCP サーバーの間の詳細なメッセージ交換は、次のとおりです。

### <a name="dhcpdiscover"></a>DHCPDISCOVER

クライアントは、DHCPDISCOVER パケットを送信します。 次に示すのは、DHCPDISCOVER パケットの IP および DHCP 部分を示すネットワークモニターキャプチャの抜粋です。 [IP] セクションで、送信先アドレスが255.255.255.255 で、発信元アドレスが0.0.0.0 であることを確認できます。 DHCP セクションは、パケットを検出パケットとして識別し、ネットワークカードの物理アドレスを使用して2か所でクライアントを識別します。 [CHADDR] フィールドと [DHCP: クライアント識別子] フィールドの値が同じであることに注意してください。

```

IP: ID = 0x0; Proto = UDP; Len: 328
 IP: Version = 4 (0x4)
 IP: Header Length = 20 (0x14)
 IP: Service Type = 0 (0x0)
 IP: Precedence = Routine
 IP: ...0.... = Normal Delay
 IP: ....0... = Normal Throughput
 IP: .....0.. = Normal Reliability
 IP: Total Length = 328 (0x148)
 IP: Identification = 0 (0x0)
 IP: Flags Summary = 0 (0x0)
 IP: .......0 = Last fragment in datagram
 IP: ......0. = May fragment datagram if necessary
 IP: Fragment Offset = 0 (0x0) bytes
 IP: Time to Live = 128 (0x80)
 IP: Protocol = UDP - User Datagram
 IP: Checksum = 0x39A6
 IP: Source Address = 0.0.0.0
 IP: Destination Address = 255.255.255.255
 IP: Data: Number of data bytes remaining = 308 (0x0134)

DHCP: Discover (xid=21274A1D)
 DHCP: Op Code (op) = 1 (0x1)
 DHCP: Hardware Type (htype) = 1 (0x1) 10Mb Ethernet
 DHCP: Hardware Address Length (hlen) = 6 (0x6)
 DHCP: Hops (hops) = 0 (0x0)
 DHCP: Transaction ID (xid) = 556223005 (0x21274A1D)
 DHCP: Seconds (secs) = 0 (0x0)
 DHCP: Flags (flags) = 0 (0x0)
 DHCP: 0............... = No Broadcast
 DHCP: Client IP Address (ciaddr) = 0.0.0.0
 DHCP: Your IP Address (yiaddr) = 0.0.0.0
 DHCP: Server IP Address (siaddr) = 0.0.0.0
 DHCP: Relay IP Address (giaddr) = 0.0.0.0
 DHCP: Client Ethernet Address (chaddr) = 08002B2ED85E
 DHCP: Server Host Name (sname) = <Blank>
 DHCP: Boot File Name (file) = <Blank>
 DHCP: Magic Cookie = [OK]
 DHCP: Option Field (options)
 DHCP: DHCP Message Type = DHCP Discover
 DHCP: Client-identifier = (Type: 1) 08 00 2b 2e d8 5e
 DHCP: Host Name = JUMBO-WS
 DHCP: Parameter Request List = (Length: 7) 01 0f 03 2c 2e 2f 06
 DHCP: End of this option field

```

### <a name="dhcpoffer"></a>DHCPOFFER

DHCP サーバーは、DHCPOFFER パケットを送信することによって応答します。 次のキャプチャの抜粋の IP セクションでは、ソースアドレスが DHCP サーバーの IP アドレスになり、送信先アドレスがブロードキャストアドレス255.255.255.255 になります。 DHCP セクションは、プランとしてパケットを識別します。 [YIADDR] フィールドには、サーバーがクライアントを提供している IP アドレスが設定されます。 CHADDR フィールドには、要求元のクライアントの物理アドレスがまだ含まれていることに注意してください。 また、DHCP オプションフィールドセクションには、サーバーによって IP アドレスと共に送信されるさまざまなオプションが示されています。 この場合、サーバーは、サブネットマスク、デフォルトゲートウェイ (ルーター)、リース時間、WINS サーバーアドレス (NetBIOS ネームサービス)、および NetBIOS ノードの種類を送信します。

```

IP: ID = 0x3C30; Proto = UDP; Len: 328
 IP: Version = 4 (0x4)
 IP: Header Length = 20 (0x14)
 IP: Service Type = 0 (0x0)
 IP: Precedence = Routine
 IP: ...0.... = Normal Delay
 IP: ....0... = Normal Throughput
 IP: .....0.. = Normal Reliability
 IP: Total Length = 328 (0x148)
 IP: Identification = 15408 (0x3C30)
 IP: Flags Summary = 0 (0x0)
 IP: .......0 = Last fragment in datagram
 IP: ......0. = May fragment datagram if necessary
 IP: Fragment Offset = 0 (0x0) bytes
 IP: Time to Live = 128 (0x80)
 IP: Protocol = UDP - User Datagram
 IP: Checksum = 0x2FA8
 IP: Source Address = 157.54.48.151
 IP: Destination Address = 255.255.255.255
 IP: Data: Number of data bytes remaining = 308 (0x0134)

DHCP: Offer (xid=21274A1D)
 DHCP: Op Code (op) = 2 (0x2)
 DHCP: Hardware Type (htype) = 1 (0x1) 10Mb Ethernet
 DHCP: Hardware Address Length (hlen) = 6 (0x6)
 DHCP: Hops (hops) = 0 (0x0)
 DHCP: Transaction ID (xid) = 556223005 (0x21274A1D)
 DHCP: Seconds (secs) = 0 (0x0)
 DHCP: Flags (flags) = 0 (0x0)
 DHCP: 0............... = No Broadcast
 DHCP: Client IP Address (ciaddr) = 0.0.0.0
 DHCP: Your IP Address (yiaddr) = 157.54.50.5
 DHCP: Server IP Address (siaddr) = 0.0.0.0
 DHCP: Relay IP Address (giaddr) = 0.0.0.0
 DHCP: Client Ethernet Address (chaddr) = 08002B2ED85E
 DHCP: Server Host Name (sname) = <Blank>
 DHCP: Boot File Name (file) = <Blank>
 DHCP: Magic Cookie = [OK]
 DHCP: Option Field (options)
 DHCP: DHCP Message Type = DHCP Offer
 DHCP: Subnet Mask = 255.255.240.0
 DHCP: Renewal Time Value (T1) = 8 Days, 0:00:00
 DHCP: Rebinding Time Value (T2) = 14 Days, 0:00:00
 DHCP: IP Address Lease Time = 16 Days, 0:00:00
 DHCP: Server Identifier = 157.54.48.151
 DHCP: Router = 157.54.48.1
 DHCP: NetBIOS Name Service = 157.54.16.154
 DHCP: NetBIOS Node Type = (Length: 1) 04
 DHCP: End of this option field

```

### <a name="dhcprequest"></a>DHCPREQUEST

クライアントは、DHCPREQUEST を送信することによって DHCPOFFER に応答します。 次のキャプチャの IP セクションでは、クライアントの送信元アドレスが0.0.0.0 で、パケットの宛先が引き続き255.255.255.255 である。 クライアントは、提供されたアドレスを使用して起動してもよいという確認をサーバーから受信していないため、0.0.0.0 を保持します。 複数の DHCP サーバーが応答していて、クライアントに対して行われたオファーの予約を保持している可能性があるため、移行先は引き続きブロードキャストされます。 これにより、他の DHCP サーバーは、提供されたアドレスを解放して使用可能なプールに戻すことができることを認識できます。 DHCP セクションは、要求としてパケットを識別し、DHCP: 要求されたアドレスフィールドを使用して提供されたアドレスを確認します。 [DHCP: サーバー識別子] フィールドには、リースを提供している DHCP サーバーの IP アドレスが表示されます。

```

IP: ID = 0x100; Proto = UDP; Len: 328
 IP: Version = 4 (0x4)
 IP: Header Length = 20 (0x14)
 IP: Service Type = 0 (0x0)
 IP: Precedence = Routine
 IP: ...0.... = Normal Delay
 IP: ....0... = Normal Throughput
 IP: .....0.. = Normal Reliability
 IP: Total Length = 328 (0x148)
 IP: Identification = 256 (0x100)
 IP: Flags Summary = 0 (0x0)
 IP: .......0 = Last fragment in datagram
 IP: ......0. = May fragment datagram if necessary
 IP: Fragment Offset = 0 (0x0) bytes
 IP: Time to Live = 128 (0x80)
 IP: Protocol = UDP - User Datagram
 IP: Checksum = 0x38A6
 IP: Source Address = 0.0.0.0
 IP: Destination Address = 255.255.255.255
 IP: Data: Number of data bytes remaining = 308 (0x0134)

DHCP: Request (xid=21274A1D)
 DHCP: Op Code (op) = 1 (0x1)
 DHCP: Hardware Type (htype) = 1 (0x1) 10Mb Ethernet
 DHCP: Hardware Address Length (hlen) = 6 (0x6)
 DHCP: Hops (hops) = 0 (0x0)
 DHCP: Transaction ID (xid) = 556223005 (0x21274A1D)
 DHCP: Seconds (secs) = 0 (0x0)
 DHCP: Flags (flags) = 0 (0x0)
 DHCP: 0............... = No Broadcast
 DHCP: Client IP Address (ciaddr) = 0.0.0.0
 DHCP: Your IP Address (yiaddr) = 0.0.0.0
 DHCP: Server IP Address (siaddr) = 0.0.0.0
 DHCP: Relay IP Address (giaddr) = 0.0.0.0
 DHCP: Client Ethernet Address (chaddr) = 08002B2ED85E
 DHCP: Server Host Name (sname) = <Blank>
 DHCP: Boot File Name (file) = <Blank>
 DHCP: Magic Cookie = [OK]
 DHCP: Option Field (options)
 DHCP: DHCP Message Type = DHCP Request
 DHCP: Client-identifier = (Type: 1) 08 00 2b 2e d8 5e
 DHCP: Requested Address = 157.54.50.5
 DHCP: Server Identifier = 157.54.48.151
 DHCP: Host Name = JUMBO-WS
 DHCP: Parameter Request List = (Length: 7) 01 0f 03 2c 2e 2f 06
 DHCP: End of this option field

```

### <a name="dhcpack"></a>DHCPACK

DHCP サーバーは、DHCPREQUEST に応答し、その結果、初期化サイクルを完了します。 送信元アドレスが DHCP サーバーの IP アドレスであり、送信先アドレスが引き続き255.255.255.255 である。 YIADDR フィールドにはクライアントのアドレスが含まれ、CHADDR および DHCP: クライアント識別子フィールドは、要求元のクライアントのネットワークカードの物理アドレスです。 DHCP オプションセクションは、パケットを ACK として識別します。

```

IP: ID = 0x3D30; Proto = UDP; Len: 328
 IP: Version = 4 (0x4)
 IP: Header Length = 20 (0x14)
 IP: Service Type = 0 (0x0)
 IP: Precedence = Routine
 IP: ...0.... = Normal Delay
 IP: ....0... = Normal Throughput
 IP: .....0.. = Normal Reliability
 IP: Total Length = 328 (0x148)
 IP: Identification = 15664 (0x3D30)
 IP: Flags Summary = 0 (0x0)
 IP: .......0 = Last fragment in datagram
 IP: ......0. = May fragment datagram if necessary
 IP: Fragment Offset = 0 (0x0) bytes
 IP: Time to Live = 128 (0x80)
 IP: Protocol = UDP - User Datagram
 IP: Checksum = 0x2EA8
 IP: Source Address = 157.54.48.151
 IP: Destination Address = 255.255.255.255
 IP: Data: Number of data bytes remaining = 308 (0x0134)

DHCP: ACK (xid=21274A1D)
 DHCP: Op Code (op) = 2 (0x2)
 DHCP: Hardware Type (htype) = 1 (0x1) 10Mb Ethernet
 DHCP: Hardware Address Length (hlen) = 6 (0x6)
 DHCP: Hops (hops) = 0 (0x0)
 DHCP: Transaction ID (xid) = 556223005 (0x21274A1D)
 DHCP: Seconds (secs) = 0 (0x0)
 DHCP: Flags (flags) = 0 (0x0)
 DHCP: 0............... = No Broadcast
 DHCP: Client IP Address (ciaddr) = 0.0.0.0
 DHCP: Your IP Address (yiaddr) = 157.54.50.5
 DHCP: Server IP Address (siaddr) = 0.0.0.0
 DHCP: Relay IP Address (giaddr) = 0.0.0.0
 DHCP: Client Ethernet Address (chaddr) = 08002B2ED85E
 DHCP: Server Host Name (sname) = <Blank>
 DHCP: Boot File Name (file) = <Blank>
 DHCP: Magic Cookie = [OK]
 DHCP: Option Field (options)
 DHCP: DHCP Message Type = DHCP ACK
 DHCP: Renewal Time Value (T1) = 8 Days, 0:00:00
 DHCP: Rebinding Time Value (T2) = 14 Days, 0:00:00
 DHCP: IP Address Lease Time = 16 Days, 0:00:00
 DHCP: Server Identifier = 157.54.48.151
 DHCP: Subnet Mask = 255.255.240.0
 DHCP: Router = 157.54.48.1
 DHCP: NetBIOS Name Service = 157.54.16.154
 DHCP: NetBIOS Node Type = (Length: 1) 04
 DHCP: End of this option field

```

クライアントに DHCP 割り当て済み IP アドレスが既にあり、再起動された場合、クライアントは、特別な DHCPREQUEST パケットで以前にリースされた IP アドレスを明示的に要求します。 送信元アドレスは0.0.0.0、宛先はブロードキャストアドレス255.255.255.255 です。 Microsoft クライアントは、DHCP オプションフィールド [DHCP: 要求されたアドレス] を事前に割り当てられたアドレスに設定します。 厳密に RFC に準拠しているクライアントは、要求されたアドレスを使用して CIADDR フィールドにデータを設定します。 Microsoft DHCP サーバーはいずれかを受け入れます。

```

IP: ID = 0x0; Proto = UDP; Len: 328
 IP: Version = 4 (0x4)
 IP: Header Length = 20 (0x14)
 IP: Service Type = 0 (0x0)
 IP: Precedence = Routine
 IP: ...0.... = Normal Delay
 IP: ....0... = Normal Throughput
 IP: .....0.. = Normal Reliability
 IP: Total Length = 328 (0x148)
 IP: Identification = 0 (0x0)
 IP: Flags Summary = 0 (0x0)
 IP: .......0 = Last fragment in datagram
 IP: ......0. = May fragment datagram if necessary
 IP: Fragment Offset = 0 (0x0) bytes
 IP: Time to Live = 128 (0x80)
 IP: Protocol = UDP - User Datagram
 IP: Checksum = 0x39A6
 IP: Source Address = 0.0.0.0
 IP: Destination Address = 255.255.255.255
 IP: Data: Number of data bytes remaining = 308 (0x0134)

DHCP: Request (xid=2757554E)
 DHCP: Op Code (op) = 1 (0x1)
 DHCP: Hardware Type (htype) = 1 (0x1) 10Mb Ethernet
 DHCP: Hardware Address Length (hlen) = 6 (0x6)
 DHCP: Hops (hops) = 0 (0x0)
 DHCP: Transaction ID (xid) = 660034894 (0x2757554E)
 DHCP: Seconds (secs) = 0 (0x0)
 DHCP: Flags (flags) = 0 (0x0)
 DHCP: 0............... = No Broadcast
 DHCP: Client IP Address (ciaddr) = 0.0.0.0
 DHCP: Your IP Address (yiaddr) = 0.0.0.0
 DHCP: Server IP Address (siaddr) = 0.0.0.0
 DHCP: Relay IP Address (giaddr) = 0.0.0.0
 DHCP: Client Ethernet Address (chaddr) = 08002B2ED85E
 DHCP: Server Host Name (sname) = <Blank>
 DHCP: Boot File Name (file) = <Blank>
 DHCP: Magic Cookie = [OK]
 DHCP: Option Field (options)
 DHCP: DHCP Message Type = DHCP Request
 DHCP: Client-identifier = (Type: 1) 08 00 2b 2e d8 5e
 DHCP: Requested Address = 157.54.50.5
 DHCP: Host Name = JUMBO-WS
 DHCP: Parameter Request List = (Length: 7) 01 0f 03 2c 2e 2f 06
 DHCP: End of this option field

```

この時点で、サーバーが応答していないか、応答しない可能性があります。 Windows NT DHCP サーバーの動作は、使用されているオペレーティングシステムのバージョンや、superscoping などのその他の要因によって異なります。 クライアントが引き続きアドレスを使用できることがサーバーによって判断された場合、サーバーはサイレント状態のままになるか、DHCPREQUEST を確認します。 サーバーは、クライアントがアドレスを持つことができないと判断した場合は、NACK を送信します。

```

IP: ID = 0x3F1A; Proto = UDP; Len: 328
 IP: Version = 4 (0x4)
 IP: Header Length = 20 (0x14)
 IP: Service Type = 0 (0x0)
 IP: Precedence = Routine
 IP: ...0.... = Normal Delay
 IP: ....0... = Normal Throughput
 IP: .....0.. = Normal Reliability
 IP: Total Length = 328 (0x148)
 IP: Identification = 16154 (0x3F1A)
 IP: Flags Summary = 0 (0x0)
 IP: .......0 = Last fragment in datagram
 IP: ......0. = May fragment datagram if necessary
 IP: Fragment Offset = 0 (0x0) bytes
 IP: Time to Live = 128 (0x80)
 IP: Protocol = UDP - User Datagram
 IP: Checksum = 0x2CBE
 IP: Source Address = 157.54.48.151
 IP: Destination Address = 255.255.255.255
 IP: Data: Number of data bytes remaining = 308 (0x0134)

DHCP: NACK (xid=74A005CE)
 DHCP: Op Code (op) = 2 (0x2)
 DHCP: Hardware Type (htype) = 1 (0x1) 10Mb Ethernet
 DHCP: Hardware Address Length (hlen) = 6 (0x6)
 DHCP: Hops (hops) = 0 (0x0)
 DHCP: Transaction ID (xid) = 1956644302 (0x74A005CE)
 DHCP: Seconds (secs) = 0 (0x0)
 DHCP: Flags (flags) = 0 (0x0)
 DHCP: 0............... = No Broadcast
 DHCP: Client IP Address (ciaddr) = 0.0.0.0
 DHCP: Your IP Address (yiaddr) = 0.0.0.0
 DHCP: Server IP Address (siaddr) = 0.0.0.0
 DHCP: Relay IP Address (giaddr) = 0.0.0.0
 DHCP: Client Ethernet Address (chaddr) = 08002B2ED85E
 DHCP: Server Host Name (sname) = <Blank>
 DHCP: Boot File Name (file) = <Blank>
 DHCP: Magic Cookie = [OK]
 DHCP: Option Field (options)
 DHCP: DHCP Message Type = DHCP NACK
 DHCP: Server Identifier = 157.54.48.151
 DHCP: End of this option field

```

その後、クライアントは検出プロセスを開始しますが、DHCPDISCOVER パケットは引き続き同じアドレスのリースを試みます。 多くの場合、tth クライアントは同じアドレスを取得しますが、そうでない可能性があります。

```

IP: ID = 0x100; Proto = UDP; Len: 328
 IP: Version = 4 (0x4)
 IP: Header Length = 20 (0x14)
 IP: Service Type = 0 (0x0)
 IP: Precedence = Routine
 IP: ...0.... = Normal Delay
 IP: ....0... = Normal Throughput
 IP: .....0.. = Normal Reliability
 IP: Total Length = 328 (0x148)
 IP: Identification = 256 (0x100)
 IP: Flags Summary = 0 (0x0)
 IP: .......0 = Last fragment in datagram
 IP: ......0. = May fragment datagram if necessary
 IP: Fragment Offset = 0 (0x0) bytes
 IP: Time to Live = 128 (0x80)
 IP: Protocol = UDP - User Datagram
 IP: Checksum = 0x38A6
 IP: Source Address = 0.0.0.0
 IP: Destination Address = 255.255.255.255
 IP: Data: Number of data bytes remaining = 308 (0x0134)

DHCP: Discover (xid=3ED14752)
 DHCP: Op Code (op) = 1 (0x1)
 DHCP: Hardware Type (htype) = 1 (0x1) 10Mb Ethernet
 DHCP: Hardware Address Length (hlen) = 6 (0x6)
 DHCP: Hops (hops) = 0 (0x0)
 DHCP: Transaction ID (xid) = 1053902674 (0x3ED14752)
 DHCP: Seconds (secs) = 0 (0x0)
 DHCP: Flags (flags) = 0 (0x0)
 DHCP: 0............... = No Broadcast
 DHCP: Client IP Address (ciaddr) = 0.0.0.0
 DHCP: Your IP Address (yiaddr) = 0.0.0.0
 DHCP: Server IP Address (siaddr) = 0.0.0.0
 DHCP: Relay IP Address (giaddr) = 0.0.0.0
 DHCP: Client Ethernet Address (chaddr) = 08002B2ED85E
 DHCP: Server Host Name (sname) = <Blank>
 DHCP: Boot File Name (file) = <Blank>
 DHCP: Magic Cookie = [OK]
 DHCP: Option Field (options)
 DHCP: DHCP Message Type = DHCP Discover
 DHCP: Client-identifier = (Type: 1) 08 00 2b 2e d8 5e
 DHCP: Requested Address = 157.54.51.5
 DHCP: Host Name = JUMBO-WS
 DHCP: Parameter Request List = (Length: 7) 01 0f 03 2c 2e 2f 06
 DHCP: End of this option field

```

DHCP サーバーからクライアントによって取得された DHCP 情報には、リース時間が関連付けられます。 リース時間は、クライアントが DHCP によって割り当てられた情報を使用できる期間を定義します。 リースが特定のマイルストーンに到達すると、クライアントはその DHCP 情報の更新を試みます。

Windows または Windows のワークグループクライアントの IP 情報を表示するには、IPCONFIG ユーティリティを使用します。 クライアントが Windows 95 の場合は、WINIPCFG を使用します。

## <a name="references"></a>参考資料

DHCP の詳細については、「RFC1541 and RFC2131」を参照してください。 Rfc は多くのサイトでインターネット経由で取得できます。たとえば、 [http://www.rfc-editor.org/](http://www.rfc-editor.org/) と[http://www.tech-nic.qc.ca/](http://www.tech-nic.qc.ca/)
