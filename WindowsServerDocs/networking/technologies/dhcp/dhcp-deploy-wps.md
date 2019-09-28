---
title: Windows PowerShell を使用した DHCP の展開
description: このトピックを使用して、ネットワーク上の1つまたは複数のサブネットに接続されている IPv4 DHCP クライアントに対して自動 IP アドレスと DHCP オプションを提供する Windows Server 2016 インターネットプロトコル (IP) version 4 DHCP サーバーを展開できます。
ms.prod: windows-server
ms.technology: networking-dhcp
ms.topic: article
ms.assetid: 7110ad21-a33e-48d5-bb3c-129982913bc8
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 66e5845bdc8f473929bfd97a3999be82cd7730c8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405770"
---
# <a name="deploy-dhcp-using-windows-powershell"></a>Windows PowerShell を使用した DHCP の展開

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

このガイドでは、Windows PowerShell を使用して、インターネットプロトコル (IP) version 4 の動的ホスト構成プロトコル @no__t 0DHCP @ no__t サーバーを展開する方法について説明します。このサーバーは、IP アドレスと DHCP オプションを、ネットワーク上の1つまたは複数のサブネットに接続されています。

>[!NOTE]
>このドキュメントを TechNet ギャラリーから Word 形式でダウンロードするには、「 [Windows Server 2016 で Windows PowerShell を使用して DHCP を展開](https://gallery.technet.microsoft.com/Deploy-DHCP-Using-Windows-246dd293)する」を参照してください。

DHCP サーバーを使用して IP アドレスを割り当てると、ネットワーク上のすべてのコンピューターにあるすべてのネットワークアダプターに対して TCP/IP v4 設定を手動で構成する必要がないため、管理オーバーヘッドが節約されます。 DHCP では、コンピューターまたは他の DHCP クライアントがネットワークに接続されているときに TCP/IP v4 構成が自動的に実行されます。

DHCP サーバーは、スタンドアロンサーバーとして、または Active Directory ドメインの一部としてワークグループに展開できます。

このガイドは次のセクションで構成されます。

- [DHCP 展開の概要](#bkmk_overview)
- [テクノロジの概要](#bkmk_technologies)
- [DHCP の展開を計画する](#bkmk_plan)
- [テストラボでのこのガイドの使用](#bkmk_lab)
- [DHCP の展開](#bkmk_deploy)
- [サーバーの機能を確認する](#bkmk_verify)
- [DHCP 用の Windows PowerShell コマンド](#bkmk_dhcpwps)
- [このガイドの「Windows PowerShell コマンドの一覧」](#bkmk_list)

## <a name="bkmk_overview"></a>DHCP 展開の概要

次の図は、このガイドを使用して展開できるシナリオを示しています。 このシナリオでは、Active Directory ドメインに1つの DHCP サーバーが含まれています。 サーバーは、2つの異なるサブネット上の DHCP クライアントに IP アドレスを提供するように構成されています。 サブネットは、DHCP 転送が有効になっているルーターによって分離されます。

![DHCP ネットワークトポロジの概要](../../media/Core-Network-Guide/cng16_overview.jpg)

## <a name="bkmk_technologies"></a>テクノロジの概要

次のセクションでは、DHCP と TCP/IP の概要について簡単に説明します。

### <a name="dhcp-overview"></a>DHCP の概要

DHCP は、ホストの IP 構成の管理を簡略化するための IP 標準です。 DHCP 標準によって、ネットワーク上の DHCP 対応クライアントへの IP アドレスの動的割り当てやその他の関連する構成の詳細を管理するための方法として、DHCP サーバーを使用できるようになります。

DHCP では、静的 IP アドレスを使用してすべてのデバイスを手動で構成するのではなく、DHCP サーバーを使用して、ローカルネットワーク上のコンピューターまたは他のデバイス (プリンターなど) に IP アドレスを動的に割り当てることができます。

TCP/IP ネットワーク上のすべてのコンピューターには、一意の IP アドレスが必要です。IP アドレスおよびアドレスに関連付けられたサブネット マスクによって、ホスト コンピューターとホスト コンピューターが関連付けられたサブネットの両方が識別されるためです。 DHCP を使用することで、DHCP クライアントとして構成されているすべてのコンピューターが、ネットワークの場所およびサブネットに適した IP アドレスを受信できます。また、デフォルト ゲートウェイや DNS サーバーなどの DHCP オプションを使用することで、DHCP クライアントにネットワーク上で正しく機能するために必要な情報を自動的に提供できます。

TCP/IP ベースのネットワークの場合、DHCP を使用すると、コンピューターの構成に伴う管理作業の複雑さと量を減らすことができます。

### <a name="tcpip-overview"></a>TCP/IP の概要

既定では、すべてのバージョンの Windows Server および Windows クライアントオペレーティングシステムは、dhcp サーバーから IP アドレスとその他の情報 (DHCP オプションと呼ばれる) を自動的に取得するように構成された IP version 4 ネットワーク接続の TCP/IP 設定を使用します。 このため、コンピューターがサーバーコンピューターまたは手動で構成された静的 IP アドレスを必要とするその他のデバイスでない限り、TCP/IP 設定を手動で構成する必要はありません。 

たとえば、DHCP サーバーの IP アドレスと、を実行している DNS サーバーとドメインコントローラーの IP アドレス Active Directory Domain Services \(AD DS @ no__t-1 を手動で構成することをお勧めします。

Windows Server 2016 の TCP/IP は次のとおりです。

- 業界標準ネットワーク プロトコルに基づくネットワーク構築ソフトウェア。

- Windows ベースのコンピューターからローカル エリア ネットワーク (LAN) 環境とワイド エリア ネットワーク (WAN) 環境の両方への接続をサポートする、ルーティング可能なエンタープライズ ネットワーク プロトコル。

- Windows ベースのコンピューターを情報共有のために異種システムと接続するためのコア テクノロジおよびユーティリティ。

- Web およびファイル転送プロトコル (FTP) サーバーなどのグローバルインターネットサービスへのアクセスを実現するための基盤。

- 堅牢かつスケーラブルな、クロスプラットフォームのクライアント/サーバー フレームワーク。

TCP/IP には基本的な TCP/IP ユーティリティが用意されています。それによって、Windows ベースのコンピューターから、次のシステムを含む他の Microsoft システム、および Microsoft 以外のシステムに接続し、情報を共有できます。

- Windows Server 2016

- Windows 10

- Windows Server 2012 R2

- Windows 8.1

- Windows Server 2012

- Windows 8

- Windows Server 2008 R2

- Windows 7

- Windows Server 2008

- Windows Vista

- インターネット ホスト

- Apple Macintosh システム

- IBM メインフレーム

- UNIX および Linux システム

- オープン VMS システム

- ネットワーク対応のプリンター

- 有線イーサネットまたはワイヤレス802.11 テクノロジが有効になっているタブレットと携帯電話

## <a name="bkmk_plan"></a>DHCP の展開を計画する

DHCP サーバーの役割をインストールする前の主要な計画手順を次に示します。

### <a name="planning-dhcp-servers-and-dhcp-forwarding"></a>DHCP サーバーおよび DHCP 転送を計画する

DHCP メッセージはブロードキャスト メッセージであるため、ルーターは DHCP メッセージをサブネット間で転送しません。 複数のサブネットがあり、DHCP サービスを各サブネットに対して提供する場合、次のいずれかを行う必要があります。

- DHCP サーバーを各サブネットにインストールします。

- DHCP ブロードキャスト メッセージをサブネット間で転送するようにルーターを構成し、複数のスコープを DHCP サーバー上に構成します (各サブネットにつき 1 つのスコープ)。

ほとんどの場合、DHCP ブロードキャスト メッセージをサブネット間で転送するようにルーターを構成する方が、DHCP サーバーをネットワークの各物理セグメント上に展開するよりコスト効果が高くなります。

### <a name="planning-ip-address-ranges"></a>IP アドレスの範囲を計画する

各サブネットには、固有の IP アドレスの範囲を設定する必要があります。 これらの範囲は、DHCP サーバー上にスコープと共に表されます。

スコープとは、DHCP サービスを使用するサブネット上のコンピューターの IP アドレスを管理するためのグループです。 管理者は、まず各物理サブネットのスコープを作成します。次に、そのスコープを使用して、クライアントによって使用されるパラメーターを定義します。

スコープには、次のプロパティがあります。

- IP アドレスの範囲。DHCP サービス リースの提供時に、この範囲のアドレスが使用されるか除外されます。

- サブネット マスク。任意の IP アドレスのサブネット プレフィックスを決定します。

- スコープ名。スコープの作成時に割り当てられます。

- リース期間の値。動的に割り当てられた IP アドレスを受け取る DHCP クライアントに割り当てられます。

- DHCP クライアントに割り当てるために構成された DHCP スコープ オプション。DNS サーバー IP アドレス、ルーター (デフォルト ゲートウェイ) IP アドレスなどがあります。

- 予約は、DHCP クライアントが常に同じ IP アドレスを受信するようにするために任意で使用されます。

サーバーを展開する前に、各サブネットに使用するサブネットと IP アドレスの範囲をリストします。

### <a name="planning-subnet-masks"></a>サブネット マスクを計画する

IP アドレス内のネットワーク ID およびホスト ID は、サブネット マスクを使用して識別されます。 各サブネット マスクは、IP アドレスのネットワーク ID 部分を示すすべて 1 から成る連続するビット グループと、ホスト IP 部分を示すすべてゼロ (0) から成る連続するビット グループで構成された 32 ビットの数値で表されます。

たとえば、IP アドレス 131.107.16.200 と一緒に使用されるサブネット マスクは、通常次の 32 ビットの 2 進数になります。

```
11111111 11111111 00000000 00000000
```

このサブネットマスク番号は、16 1 ビットの後に16ビットの0ビットが続くもので、この IP アドレスのネットワーク ID とホスト ID のセクションの長さが16ビットの両方であることを示します。 通常、このサブネット マスクはピリオドで区切られた 10 進表記で "255.255.0.0" と表されます。

次の表に、インターネット アドレス クラスのサブネット マスクを表示します。

|アドレス クラス|サブネット マスクのビット|サブネット マスク|
|-----------------|------------------------|---------------|
|クラス A|11111111 00000000 00000000 00000000|255.0.0.0|
|クラス B|11111111 11111111 00000000 00000000|255.255.0.0|
|クラス C|11111111 11111111 11111111 00000000|255.255.255.0|

DHCP にスコープを作成し、そのスコープの IP アドレス範囲を入力すると、DHCP によってこれらの既定のサブネット マスクの値が提供されます。 既定のサブネット マスクの値は通常、各 IP ネットワーク セグメントがそれぞれ個別の物理ネットワークに対応するのであれば、ほとんどのネットワークで特別な要件なく受け入れられます。

一部のネットワークでは、カスタマイズしたサブネット マスクを使用して IP サブネットを実装する必要があります。 IP サブネットの設定では、IP アドレスの既定のホスト ID 部分を細分化し、元のクラスベースのネットワーク ID の構成部分であるサブネットを指定できます。

サブネット マスクの長さをカスタマイズすることで、実際のホスト ID のために使用するビット数を低減できます。

アドレス割り当てとルーティングの問題を防止するには、ネットワーク セグメント上のすべての TCP/IP コンピューターに同じサブネット マスクが使用されており、各コンピューターまたはデバイスに固有の IP アドレスが割り当てられていることを確認します。

### <a name="planning-exclusion-ranges"></a>除外範囲を計画する

DHCP サーバー上にスコープを作成する場合、DHCP サーバーが DHCP クライアント (コンピューターやその他のデバイスなど) にリースできるすべての IP アドレスを含む IP アドレス範囲を指定します。 一部のサーバーおよびその他のデバイスを、DHCP サーバーが使用している IP アドレス範囲と同じ IP アドレス範囲の静的 IP アドレスを使用して手動で構成する場合、ユーザーと DHCP サーバーが異なるデバイスに同じ IP アドレスを割り当てることによって、誤って IP アドレスが競合する可能性があります。

この問題を解決するために、DHCP スコープの除外範囲を作成できます。 除外範囲は、DHCP サーバーが使用できない範囲の IP アドレス範囲内にある、連続した範囲の IP アドレスです。 除外範囲を作成した場合、DHCP サーバーはその範囲にあるアドレスを割り当てません。そのため、ユーザーは IP アドレスを競合させることなく、その範囲のアドレスを手動で割り当てることができます。

各スコープの除外範囲を作成することによって、DHCP サーバーによる配布から IP アドレスを除外できます。 静的 IP アドレスを使用して構成されているすべてのデバイスに対し、除外を適用する必要があります。 他のサーバー、非 DHCP クライアント、ディスクレス ワークステーション、またはルーティングとリモート アクセスおよび PPP クライアントに手動で割り当てた IP アドレスは、すべて除外アドレスに含める必要があります。

除外範囲は、将来のネットワークの拡張に対応できるよう、余分なアドレスを含めて構成することをお勧めします。 次の表は、IP アドレス範囲が 10.0.0.1-10.0.0.254 でサブネットマスクが255.255.255.0 のスコープの除外範囲の例を示しています。

|構成項目|値の例|
|-----------------------|------------------|
|除外範囲の開始 IP アドレス|10.0.0.1|
|除外範囲の終了 IP アドレス|「10.0.0.25|

### <a name="planning-tcpip-static-configuration"></a>TCP/IP の静的構成を計画する

ルーター、DHCP サーバー、DNS サーバーなどの特定のデバイスは、静的 IP アドレスを使用して構成する必要があります。 さらに、プリンターなどの追加のデバイスで、IP アドレスを固定させる必要のあるデバイスがあります。 各サブネットについて、静的に構成するデバイスをリストアップし、DHCP サーバー上で使用する除外範囲を計画して、その DHCP サーバーが静的に構成されたデバイスの IP アドレスをリースしないようにする必要があります。 除外範囲は、スコープ内の制限された連続する IP アドレスであり、DHCP サービスの提供から除外されます。 除外範囲を設定することで、これらの範囲内のすべてのアドレスは、サーバーからネットワーク上の DHCP クライアントに提供されないことが保証されます。

たとえば、サブネットの IP アドレス範囲が192.168.0.1 から192.168.0.254 で、静的 IP アドレスを使用して構成するデバイスが10個ある場合、192.168.0 の除外範囲を作成できます。10個以上の IP アドレスを含む*x*スコープ:192.168.0.1 から192.168.0.15。

この例では、10 個の除外された IP アドレスを使用してサーバーやその他のデバイスを静的 IP アドレスで構成し、残りの 5 個の IP アドレスは、将来追加する可能性がある新しいデバイスの静的構成のために確保されています。 この除外範囲では、DHCP サーバーには 192.168.0.16 ～ 192.168.0.254 までのアドレス プールが残ります。

次の表は、AD DS と DNS の構成項目の追加例を示しています。

|構成項目|値の例|
|-----------------------|------------------|
|ネットワーク接続バインディング|Ethernet|
|DNS サーバー設定|DC1.corp.contoso.com|
|優先 DNS サーバーの IP アドレス|10.0.0.2|
|スコープ値<br /><br />1. スコープ名<br />2. 開始 IP アドレス<br />3.終了 IP アドレス<br />4。サブネット マスク<br />5。デフォルト ゲートウェイ (オプション)<br />6。リース期間|1. プライマリ サブネット<br />2. 10.0.0.1<br />3. 10.0.0.254<br />4. 255.255.255.0<br />5. 10.0.0.1<br />6. 8 日|
|IPv6 DHCP サーバーの操作モード|無効|

## <a name="bkmk_lab"></a>テストラボでのこのガイドの使用

このガイドを使用して、実稼働環境に展開する前に、テストラボに DHCP を展開することができます。 

>[!NOTE]
>テストラボに DHCP を展開しない場合は、「 [dhcp の展開](#bkmk_deploy)」セクションに進むことができます。

ラボの要件は、物理サーバーと仮想マシンのどちらを使用しているかによって異なります。 @no__t は、@ no__t-1 で、Active Directory ドメインを使用するか、スタンドアロンの DHCP サーバーを展開するかによって異なります。

このガイドを使用して、DHCP 展開をテストするために必要な最小限のリソースを決定するには、次の情報を参照してください。

### <a name="test-lab-requirements-with-vms"></a>Vm を使用したテストラボの要件

Vm を使用してテストラボに DHCP を展開するには、次のリソースが必要です。

ドメインの展開またはスタンドアロンの展開では、ハイパー @ no__t-0V ホストとして構成されている1つのサーバーが必要です。

**ドメインの展開**

この展開には、1台の物理サーバー、1つの仮想スイッチ、2つの仮想サーバー、1つの仮想クライアントが必要です。

物理サーバーの Hyper-v マネージャーで、次の項目を作成します。

1. 1つの**内部**仮想スイッチ。 **外部**仮想スイッチを作成しないでください。これは、hyper-v ホストが dhcp サーバーを含むサブネット上にある場合、テスト VM は dhcp サーバーから IP アドレスを受信するためです。 さらに、展開したテスト DHCP サーバーは、Hyper-v ホストがインストールされているサブネット上の他のコンピューターに IP アドレスを割り当てる場合があります。
1. Windows Server 2016 を実行している1台の VM が、作成した内部仮想スイッチに接続されている Active Directory Domain Services のドメインコントローラーとして構成されています。 このガイドに適合するために、このサーバーには静的に構成された IP アドレス10.0.0.2 が必要です。 AD DS の展開の詳細については、「Windows Server 2016[コアネットワークガイド](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide#BKMK_deployADDNS01)」の**DC1 の展開**に関するセクションを参照してください。
1. このガイドを使用して DHCP サーバーとして構成し、作成した内部仮想スイッチに接続されている、Windows Server 2016 を実行している1台の VM。 
1. 作成した内部仮想スイッチに接続されている Windows クライアントオペレーティングシステムを実行している1つの VM。 dhcp サーバーが dhcp クライアントに IP アドレスと DHCP オプションを動的に割り当てていることを確認するために使用します。

**スタンドアロン DHCP サーバーの展開**

この展開には、1台の物理サーバー、1つの仮想スイッチ、1台の仮想サーバー、1つの仮想クライアントが必要です。

物理サーバーの Hyper-v マネージャーで、次の項目を作成します。

1. 1つの**内部**仮想スイッチ。 **外部**仮想スイッチを作成しないでください。これは、hyper-v ホストが dhcp サーバーを含むサブネット上にある場合、テスト VM は dhcp サーバーから IP アドレスを受信するためです。 さらに、展開したテスト DHCP サーバーは、Hyper-v ホストがインストールされているサブネット上の他のコンピューターに IP アドレスを割り当てる場合があります。
2. このガイドを使用して DHCP サーバーとして構成し、作成した内部仮想スイッチに接続されている、Windows Server 2016 を実行している1台の VM。
3. 作成した内部仮想スイッチに接続されている Windows クライアントオペレーティングシステムを実行している1つの VM。 dhcp サーバーが dhcp クライアントに IP アドレスと DHCP オプションを動的に割り当てていることを確認するために使用します。

### <a name="test-lab-requirements-with-physical-servers"></a>物理サーバーを使用したテストラボの要件

物理サーバーを使用したテストラボに DHCP を展開するには、次のリソースが必要です。

**ドメインの展開**

この展開には、1つのハブまたはスイッチ、2台の物理サーバー、1つの物理クライアントが必要です。

1. イーサネットケーブルを使用して物理コンピューターを接続できる1つのイーサネットハブまたはスイッチ
2. Active Directory Domain Services が設定されたドメインコントローラーとして構成された Windows Server 2016 を実行している1台の物理コンピューター。 このガイドに適合するために、このサーバーには静的に構成された IP アドレス10.0.0.2 が必要です。 AD DS の展開の詳細については、「Windows Server 2016[コアネットワークガイド](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide#BKMK_deployADDNS01)」の**DC1 の展開**に関するセクションを参照してください。
3. このガイドを使用して DHCP サーバーとして構成する Windows Server 2016 を実行している1台の物理コンピューター。 
4. DHCP サーバーが DHCP クライアントに IP アドレスと DHCP オプションを動的に割り当てていることを確認するために使用する、Windows クライアントオペレーティングシステムを実行している1台の物理コンピューター。

>[!NOTE]
>このデプロイに十分なテストコンピューターがない場合は、AD DS と DHCP の両方に対して1つのテストコンピューターを使用できます。ただし、この構成は運用環境では推奨されません。

**スタンドアロン DHCP サーバーの展開**

この展開には、1つのハブまたはスイッチ、1台の物理サーバー、1つの物理クライアントが必要です。

1. イーサネットケーブルを使用して物理コンピューターを接続できる1つのイーサネットハブまたはスイッチ
2. このガイドを使用して DHCP サーバーとして構成する Windows Server 2016 を実行している1台の物理コンピューター。
3. DHCP サーバーが DHCP クライアントに IP アドレスと DHCP オプションを動的に割り当てていることを確認するために使用する、Windows クライアントオペレーティングシステムを実行している1台の物理コンピューター。


## <a name="bkmk_deploy"></a>DHCP の展開

このセクションでは、1台のサーバーに DHCP を展開するために使用できる Windows PowerShell コマンドの例を示します。 これらのコマンド例をサーバーで実行する前に、ネットワークと環境に合わせてコマンドを変更する必要があります。 

たとえば、コマンドを実行する前に、次の項目のコマンドの例の値を置き換える必要があります。

- コンピューター名
- 構成する各スコープの IP アドレス範囲 (サブネットごとに1つのスコープ)
- 構成する各 IP アドレス範囲のサブネットマスク
- スコープごとのスコープ名
- 各スコープの除外範囲
- DHCP オプションの値 (既定のゲートウェイ、ドメイン名、DNS または WINS サーバーなど)
- インターフェイス名

>[!IMPORTANT]
>コマンドを実行する前に、環境に合わせてすべてのコマンドを確認および変更します。

### <a name="where-to-install-dhcp---on-a-physical-computer-or-a-vm"></a>DHCP をインストールする場所 (物理コンピューターまたは VM)

DHCP サーバーの役割は、Hyper-v ホストにインストールされている物理コンピューターまたは仮想マシン \(VM @ no__t-1 にインストールできます。 DHCP を VM にインストールし、Hyper-v ホストが接続されている物理ネットワーク上のコンピューターに DHCP サーバーが IP アドレスの割り当てを行うようにする場合は、VM 仮想ネットワークアダプターを外部にある Hyper-v 仮想スイッチに接続する必要があります。 **/c0 >。**

詳細については、「[仮想ネットワークの作成](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/connect-to-network)」トピックの「 **hyper-v マネージャーを使用した仮想スイッチの作成**」セクションを参照してください。

### <a name="run-windows-powershell-as-an-administrator"></a>管理者として Windows PowerShell を実行する

管理者特権で Windows PowerShell を実行するには、次の手順に従います。

1. Windows Server 2016 を実行しているコンピューターで、**スタート** をクリックし、windows PowerShell アイコンを右クリックします。 メニューが表示されます。

2. メニューで **[詳細]** をクリックし、 **[管理者として実行]** をクリックします。 メッセージが表示されたら、コンピューターに対する管理者特権を持つアカウントの資格情報を入力します。 コンピューターにログオンしているユーザーアカウントが管理者レベルのアカウントである場合、資格情報のプロンプトは表示されません。

3. Windows PowerShell が管理者特権で開きます。

### <a name="rename-the-dhcp-server-and-configure-a-static-ip-address"></a>DHCP サーバーの名前を変更し、静的 IP アドレスを構成する

まだ行っていない場合は、次の Windows PowerShell コマンドを使用して DHCP サーバーの名前を変更し、サーバーの静的 IP アドレスを構成できます。

**静的 IP アドレスを構成する**

次のコマンドを使用して、DHCP サーバーに静的 IP アドレスを割り当てたり、正しい DNS サーバー IP アドレスを使用して DHCP サーバーの TCP/IP プロパティを構成したりすることができます。 また、この例のインターフェイス名と IP アドレスを、コンピューターの構成に使用する値に置き換える必要があります。

```
New-NetIPAddress -IPAddress 10.0.0.3 -InterfaceAlias "Ethernet" -DefaultGateway 10.0.0.1 -AddressFamily IPv4 -PrefixLength 24
Set-DnsClientServerAddress -InterfaceAlias "Ethernet" -ServerAddresses 10.0.0.2
```

これらのコマンドの詳細については、次のトピックを参照してください。

- [New-netipaddress](https://technet.microsoft.com/itpro/powershell/windows/tcpip/new-netipaddress)
- [設定-DnsClientServerAddress](https://technet.microsoft.com/itpro/powershell/windows/dns-client/set-dnsclientserveraddress)

**コンピューターの名前を変更する**

次のコマンドを使用して、コンピューターの名前を変更してから再起動することができます。

```
Rename-Computer -Name DHCP1
Restart-Computer
```

これらのコマンドの詳細については、次のトピックを参照してください。

- [コンピューター名の変更](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.management/rename-computer)
- [Restart-Computer](https://msdn.microsoft.com/powershell/reference/4.0/microsoft.powershell.management/restart-computer)

### <a name="join-the-computer-to-the-domain-optional"></a>コンピューターをドメインに参加させ \(Optional @ no__t-1

Active Directory ドメイン環境に DHCP サーバーをインストールする場合は、コンピューターをドメインに参加させる必要があります。 管理者特権で Windows PowerShell を開き、ドメイン NetBios 名**CORP**を環境に適した値に置き換えた後、次のコマンドを実行します。

```
Add-Computer CORP
```

メッセージが表示されたら、ドメインにコンピューターを参加させるアクセス許可を持つドメインユーザーアカウントの資格情報を入力します。 

```
Restart-Computer
```

コンピューターの追加コマンドの詳細については、次のトピックを参照してください。

- [コンピューターの追加](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.management/add-computer)

### <a name="install-dhcp"></a>DHCP のインストール

コンピューターが再起動したら、管理者特権で Windows PowerShell を開き、次のコマンドを実行して DHCP をインストールします。

```
Install-WindowsFeature DHCP -IncludeManagementTools
```

このコマンドの詳細については、次のトピックを参照してください。

- [Install-Add-windowsfeature](https://technet.microsoft.com/itpro/powershell/windows/server-manager/install-windowsfeature)

### <a name="create-dhcp-security-groups"></a>DHCP セキュリティグループを作成する

セキュリティグループを作成するには、Windows PowerShell でネットワークシェル \(netsh @ no__t コマンドを実行し、DHCP サービスを再起動して新しいグループがアクティブになるようにする必要があります。

Dhcp サーバーで次の netsh コマンドを実行すると、dhcp **Administrators**および dhcp **Users**セキュリティグループが、dhcp サーバー上の **[ローカルユーザーとグループ]** に作成されます。

```
netsh dhcp add securitygroups
```

次のコマンドは、ローカルコンピューター上の DHCP サービスを再起動します。

```
Restart-Service dhcpserver
```

これらのコマンドの詳細については、次のトピックを参照してください。

- [ネットワーク シェル (netsh)](../netsh/netsh.md)
- [サービスの再起動](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.management/restart-service)

### <a name="authorize-the-dhcp-server-in-active-directory-optional"></a>Active Directory で DHCP サーバーを承認する \(Optional @ no__t-1

ドメイン環境に DHCP をインストールする場合は、次の手順を実行して、DHCP サーバーがドメインで動作することを承認する必要があります。

>[!NOTE]
>Active Directory ドメインにインストールされている承認されていない DHCP サーバーは、正常に機能しないため、DHCP クライアントに IP アドレスをリースしません。 承認されていない DHCP サーバーの自動無効化は、承認されていない DHCP サーバーがネットワーク上のクライアントに誤った IP アドレスを割り当てないようにするセキュリティ機能です。

次のコマンドを使用して、Active Directory の承認された DHCP サーバーの一覧に DHCP サーバーを追加できます。 

>[!NOTE]
>ドメイン環境がない場合は、このコマンドを実行しないでください。

```
Add-DhcpServerInDC -DnsName DHCP1.corp.contoso.com -IPAddress 10.0.0.3
```

DHCP サーバーが Active Directory で承認されていることを確認するには、次のコマンドを使用します。

```
Get-DhcpServerInDC
```

Windows PowerShell に表示される結果の例を次に示します。

```
IPAddress   DnsName
---------   -------
10.0.0.3    DHCP1.corp.contoso.com
```

これらのコマンドの詳細については、次のトピックを参照してください。

- [追加-DhcpServerInDC](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/add-dhcpserverindc)
- [取得-DhcpServerInDC](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/get-dhcpserverindc)

### <a name="notify-server-manager-that-post-install-dhcp-configuration-is-complete-optional"></a>Post @ no__t-0install DHCP 構成が完了したことを通知サーバーマネージャー \(Optional @ no__t

Active Directory でのセキュリティグループの作成や DHCP サーバーの承認など、@ no__t のインストールタスクを完了した後で、サーバーマネージャーによってユーザーインターフェイスに警告が表示されることがあります。これは、post @ no__t のインストール手順を示す必要があります。DHCP ポストインストールの構成ウィザードを使用して完了します。

この Windows PowerShell コマンドを使用して次のレジストリキーを構成することによって、サーバーマネージャーに @ no__t-0unnecessary で不正確なメッセージが表示されないようにすることができます。

```
Set-ItemProperty –Path registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ServerManager\Roles\12 –Name ConfigurationState –Value 2
```

このコマンドの詳細については、次のトピックを参照してください。

- [Get-itemproperty](https://msdn.microsoft.com/powershell/reference/4.0/microsoft.powershell.management/set-itemproperty?f=255&MSPPError=-2147217396)

### <a name="set-server-level-dns-dynamic-update-configuration-settings-optional"></a>サーバーレベルの DNS 動的更新の構成設定 \(Optional @ no__t-1

Dhcp サーバーで DHCP クライアントコンピューターの DNS 動的更新を実行する場合は、次のコマンドを実行してこの設定を構成できます。 これは、スコープレベルの設定ではなく、サーバーレベルの設定であるため、サーバー上で構成するすべてのスコープに影響します。 この例のコマンドは、クライアントの有効期限が切れたときにクライアントの DNS リソースレコードを削除するように DHCP サーバーを構成します。

```
Set-DhcpServerv4DnsSetting -ComputerName "DHCP1.corp.contoso.com" -DynamicUpdates "Always" -DeleteDnsRRonLeaseExpiry $True
```

次のコマンドを使用して、DHCP サーバーが DNS サーバー上のクライアントレコードを登録または登録解除するために使用する資格情報を構成できます。 この例では、DHCP サーバーに資格情報を保存します。 最初のコマンドは、 **Get Credential**を使用して**PSCredential**オブジェクトを作成し、そのオブジェクトを **$Credential**変数に格納します。 コマンドを実行すると、ユーザー名とパスワードの入力を求められるため、DNS サーバー上のリソースレコードを更新するアクセス許可を持つアカウントの資格情報を入力してください。
 
```
$Credential = Get-Credential
Set-DhcpServerDnsCredential -Credential $Credential -ComputerName "DHCP1.corp.contoso.com"
``` 

これらのコマンドの詳細については、次のトピックを参照してください。

- [DhcpServerv4DnsSetting](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/set-dhcpserverv4dnssetting)
- [DhcpServerDnsCredential](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/set-dhcpserverdnscredential)

### <a name="configure-the-corpnet-scope"></a>企業ネットワークのスコープを構成する

DHCP のインストールが完了したら、次のコマンドを使用して、ネットワークスコープの構成とアクティブ化を行い、スコープの除外範囲を作成し、DHCP オプションの既定のゲートウェイ、DNS サーバーの IP アドレス、DNS ドメイン名を構成することができます。

```
Add-DhcpServerv4Scope -name "Corpnet" -StartRange 10.0.0.1 -EndRange 10.0.0.254 -SubnetMask 255.255.255.0 -State Active    
Add-DhcpServerv4ExclusionRange -ScopeID 10.0.0.0 -StartRange 10.0.0.1 -EndRange 10.0.0.15
Set-DhcpServerv4OptionValue -OptionID 3 -Value 10.0.0.1 -ScopeID 10.0.0.0 -ComputerName DHCP1.corp.contoso.com
Set-DhcpServerv4OptionValue -DnsDomain corp.contoso.com -DnsServer 10.0.0.2
```

これらのコマンドの詳細については、次のトピックを参照してください。

- [DhcpServerv4Scope](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/add-dhcpserverv4scope)
- [DhcpServerv4ExclusionRange](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/add-dhcpserverv4exclusionrange)
- [DhcpServerv4OptionValue](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/set-dhcpserverv4optionvalue)

### <a name="configure-the-corpnet2-scope-optional"></a>Corpnet2 スコープ \(Optional @ no__t-1 を構成します。

DHCP 転送が有効になっているルーターを使用して最初のサブネットに接続されている2番目のサブネットがある場合は、次のコマンドを使用して、この例の Corpnet2 という名前の2つ目のスコープを追加できます。 また、この例では、Corpnet2 サブネットのサブネット @ no__t-1 のルーター IP アドレス @no__t、既定のゲートウェイの除外範囲と IP アドレスを構成します。

```
Add-DhcpServerv4Scope -name "Corpnet2" -StartRange 10.0.1.1 -EndRange 10.0.1.254 -SubnetMask 255.255.255.0 -State Active
Add-DhcpServerv4ExclusionRange -ScopeID 10.0.1.0 -StartRange 10.0.1.1 -EndRange 10.0.1.15
Set-DhcpServerv4OptionValue -OptionID 3 -Value 10.0.1.1 -ScopeID 10.0.1.0 -ComputerName DHCP1.corp.contoso.com
```

この DHCP サーバーによって提供される追加のサブネットがある場合は、すべてのコマンドパラメーターに異なる値を使用してこれらのコマンドを繰り返し、各サブネットのスコープを追加することができます。

>[!IMPORTANT]
>Dhcp クライアントと DHCP サーバー間のすべてのルーターが、DHCP メッセージ転送用に構成されていることを確認します。 DHCP 転送を構成する方法については、ルーターのマニュアルを参照してください。

## <a name="bkmk_verify"></a>サーバーの機能を確認する

Dhcp サーバーが DHCP クライアントに IP アドレスを動的に割り当てていることを確認するために、別のコンピューターをサービスサブネットに接続できます。 イーサネットケーブルをネットワークアダプターに接続し、コンピューターの電源をオンにすると、DHCP サーバーから IP アドレスが要求されます。 **Ipconfig/all**コマンドを使用して結果を確認するか、Windows エクスプローラーなどを使用してブラウザーまたはファイル共有で Web リソースにアクセスしようとするなどの接続テストを実行して、正常に構成されたことを確認できます。プログラム.

クライアントが DHCP サーバーから IP アドレスを受信しない場合は、次のトラブルシューティング手順を実行します。

1. イーサネットケーブルがコンピューターとイーサネットスイッチ、ハブ、またはルーターの両方に接続されていることを確認します。
2. クライアントコンピューターを、ルーターによって DHCP サーバーから分離されたネットワークセグメントに接続している場合は、ルーターが DHCP メッセージを転送するように構成されていることを確認します。
3. Active Directory から承認された DHCP サーバーの一覧を取得するには、次のコマンドを実行して、DHCP サーバーが Active Directory で承認されていることを確認します。 [取得-DhcpServerInDC](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/get-dhcpserverindc)。
4. スコープがアクティブ化されていることを確認します。そのためには、DHCP コンソール \(Server Manager、**ツール**、 **DHCP**\)、サーバーツリーを展開してスコープを確認し、右 @ no__t を右クリックします。 選択したメニューに **[アクティブ]** 化 が含まれている場合は、 **[アクティブ化]** をクリックします。 \(If が既にアクティブ化されている場合、メニュー選択は**非アクティブ化**を読み取ります。 \)

## <a name="bkmk_dhcpwps"></a>DHCP 用の Windows PowerShell コマンド

次のリファレンスでは、Windows Server 2016 のすべての DHCP サーバー Windows PowerShell コマンドについて、コマンドの説明と構文を示します。 このトピックでは、コマンドの先頭にある動詞 ( **Get**や**Set**など) に基づいて、アルファベット順にコマンドを示します。

>[!NOTE]
>Windows server 2012 R2 では、Windows Server 2016 コマンドを使用できません。

- [DhcpServer モジュール](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/index)

次のリファレンスでは、Windows Server 2012 R2 のすべての DHCP サーバー Windows PowerShell コマンドについて、コマンドの説明と構文を示します。 このトピックでは、コマンドの先頭にある動詞 ( **Get**や**Set**など) に基づいて、アルファベット順にコマンドを示します。

>[!NOTE]
>Windows server 2012 R2 のコマンドは、Windows Server 2016 で使用できます。

- [Windows PowerShell の DHCP サーバーコマンドレット](https://technet.microsoft.com/library/jj590751.aspx)

## <a name="bkmk_list"></a>このガイドの「Windows PowerShell コマンドの一覧」

このガイドで使用されているコマンドとサンプル値の簡単な一覧を次に示します。

```
New-NetIPAddress -IPAddress 10.0.0.3 -InterfaceAlias "Ethernet" -DefaultGateway 10.0.0.1 -AddressFamily IPv4 -PrefixLength 24
Set-DnsClientServerAddress -InterfaceAlias "Ethernet" -ServerAddresses 10.0.0.2
Rename-Computer -Name DHCP1
Restart-Computer

Add-Computer CORP
Restart-Computer

Install-WindowsFeature DHCP -IncludeManagementTools
netsh dhcp add securitygroups
Restart-Service dhcpserver

Add-DhcpServerInDC -DnsName DHCP1.corp.contoso.com -IPAddress 10.0.0.3
Get-DhcpServerInDC

Set-ItemProperty –Path registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ServerManager\Roles\12 –Name ConfigurationState –Value 2

Set-DhcpServerv4DnsSetting -ComputerName "DHCP1.corp.contoso.com" -DynamicUpdates "Always" -DeleteDnsRRonLeaseExpiry $True

$Credential = Get-Credential
Set-DhcpServerDnsCredential -Credential $Credential -ComputerName "DHCP1.corp.contoso.com"

rem At prompt, supply credential in form DOMAIN\user, password

rem Configure scope Corpnet
Add-DhcpServerv4Scope -name "Corpnet" -StartRange 10.0.0.1 -EndRange 10.0.0.254 -SubnetMask 255.255.255.0 -State Active
Add-DhcpServerv4ExclusionRange -ScopeID 10.0.0.0 -StartRange 10.0.0.1 -EndRange 10.0.0.15
Set-DhcpServerv4OptionValue -OptionID 3 -Value 10.0.0.1 -ScopeID 10.0.0.0 -ComputerName DHCP1.corp.contoso.com
Set-DhcpServerv4OptionValue -DnsDomain corp.contoso.com -DnsServer 10.0.0.2

rem Configure scope Corpnet2
Add-DhcpServerv4Scope -name "Corpnet2" -StartRange 10.0.1.1 -EndRange 10.0.1.254 -SubnetMask 255.255.255.0 -State Active
Add-DhcpServerv4ExclusionRange -ScopeID 10.0.1.0 -StartRange 10.0.1.1 -EndRange 10.0.1.15
Set-DhcpServerv4OptionValue -OptionID 3 -Value 10.0.1.1 -ScopeID 10.0.1.0 -ComputerName DHCP1.corp.contoso.com
```
