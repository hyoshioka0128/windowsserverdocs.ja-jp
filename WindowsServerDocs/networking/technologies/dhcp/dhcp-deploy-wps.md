---
title: Windows PowerShell を使用した DHCP の展開
description: このトピックを使用すると、ネットワーク上の 1 つまたは複数のサブネットに接続されている IPv4 DHCP クライアントに自動の IP アドレスと DHCP オプションを提供する Windows Server 2016 インターネット プロトコル (IP) version 4 の DHCP サーバーを展開します。
ms.prod: windows-server-threshold
ms.technology: networking-dhcp
ms.topic: article
ms.assetid: 7110ad21-a33e-48d5-bb3c-129982913bc8
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8a53f6293067fa0f7014e7794696cf75f7179545
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849093"
---
# <a name="deploy-dhcp-using-windows-powershell"></a>Windows PowerShell を使用した DHCP の展開

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このガイドが Windows PowerShell を使用して、インターネット プロトコル (IP) version 4 をデプロイする方法を説明動的ホスト構成プロトコル\(DHCP\)を自動的に割り当てる IP アドレスと DHCP サーバーの IPv4 dhcp オプションネットワーク上の 1 つまたは複数のサブネットに接続されているクライアント。

>[!NOTE]
>Word 形式では、このドキュメントは、TechNet ギャラリーからダウンロードするを参照してください。[デプロイ DHCP を使用して Windows PowerShell で Windows Server 2016](https://gallery.technet.microsoft.com/Deploy-DHCP-Using-Windows-246dd293)します。

アドレスは IP の割り当てに DHCP サーバーを使用して、ネットワーク上のすべてのコンピューターですべてのネットワーク アダプターの TCP/IP v4 の設定を手動で構成する必要はありませんのでに管理オーバーヘッドで保存します。 DHCP を使用、コンピューターの場合に、TCP/IP v4 の構成は自動的に実行または他の DHCP クライアントがネットワークに接続されています。

ワークグループで、DHCP サーバーは、スタンドアロン サーバーまたは Active Directory ドメインの一部としてデプロイできます。

このガイドは次のセクションで構成されます。

- [DHCP 展開の概要](#bkmk_overview)
- [テクノロジの概要](#bkmk_technologies)
- [DHCP の展開を計画します。](#bkmk_plan)
- [テスト ラボでのこのガイドの使用](#bkmk_lab)
- [DHCP を展開します。](#bkmk_deploy)
- [サーバー機能を確認します。](#bkmk_verify)
- [DHCP 用 Windows PowerShell コマンド](#bkmk_dhcpwps)
- [このガイドでの Windows PowerShell コマンドの一覧](#bkmk_list)

## <a name="bkmk_overview"></a>DHCP 展開の概要

次の図は、このガイドを使用してデプロイできるシナリオを示しています。 シナリオには、Active Directory ドメインには 1 つの DHCP サーバーが含まれます。 2 つの異なるサブネット上の DHCP クライアントに IP アドレスを提供する、サーバーが構成されます。 サブネットは、DHCP 転送が有効にしたルーターで区切られます。

![DHCP ネットワーク トポロジの概要](../../media/Core-Network-Guide/cng16_overview.jpg)

## <a name="bkmk_technologies"></a>テクノロジの概要

次のセクションでは、DHCP および TCP/IP の概要を説明します。

### <a name="dhcp-overview"></a>DHCP の概要

DHCP は、ホストの IP 構成の管理を簡略化するための IP 標準です。 DHCP 標準によって、ネットワーク上の DHCP 対応クライアントへの IP アドレスの動的割り当てやその他の関連する構成の詳細を管理するための方法として、DHCP サーバーを使用できるようになります。

DHCP を使用すると、DHCP サーバーを使用して、コンピューターまたは静的 IP アドレスを持つすべてのデバイスを手動で構成するのではなく、ローカル ネットワーク上のプリンターなどの他のデバイスに IP アドレスを動的に割り当てることができます。

TCP/IP ネットワーク上のすべてのコンピューターには、一意の IP アドレスが必要です。IP アドレスおよびアドレスに関連付けられたサブネット マスクによって、ホスト コンピューターとホスト コンピューターが関連付けられたサブネットの両方が識別されるためです。 DHCP を使用することで、DHCP クライアントとして構成されているすべてのコンピューターが、ネットワークの場所およびサブネットに適した IP アドレスを受信できます。また、デフォルト ゲートウェイや DNS サーバーなどの DHCP オプションを使用することで、DHCP クライアントにネットワーク上で正しく機能するために必要な情報を自動的に提供できます。

IP ベースのネットワークでは、DHCP によって、複雑さとコンピューターの構成に伴う管理作業の量が削減されます。

### <a name="tcpip-overview"></a>TCP/IP の概要

既定では、Windows Server および Windows クライアント オペレーティング システムのすべてのバージョンは、IP アドレスと DHCP サーバーから DHCP オプションと呼ばれるその他の情報を自動的に取得するように構成 IP バージョン 4 のネットワーク接続の TCP/IP 設定があります。 このため、コンピューターがサーバー コンピューターまたはその他のデバイスを手動で構成した静的 IP アドレスを必要としない限り、手動で TCP/IP 設定を構成する必要はありません。 

DHCP サーバーの IP アドレスと DNS サーバーおよび Active Directory Domain Services を実行しているドメイン コント ローラーの IP アドレスは構成手動で、たとえば、勧め\(AD DS\)します。

Windows Server 2016 での TCP/IP 次に示します。

-   業界標準ネットワーク プロトコルに基づくネットワーク構築ソフトウェア。

-   Windows ベースのコンピューターからローカル エリア ネットワーク (LAN) 環境とワイド エリア ネットワーク (WAN) 環境の両方への接続をサポートする、ルーティング可能なエンタープライズ ネットワーク プロトコル。

-   Windows ベースのコンピューターを情報共有のために異種システムと接続するためのコア テクノロジおよびユーティリティ。

-   Web およびファイル転送プロトコル (FTP) サーバーなどのグローバル インターネット サービスへのアクセスの基盤です。

-   堅牢かつスケーラブルな、クロスプラットフォームのクライアント/サーバー フレームワーク。

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

- ネットワーク対応プリンター

- タブレットと携帯電話をワイヤード (有線) イーサネットまたはワイヤレスの 802.11 テクノロジを有効になっていると

## <a name="bkmk_plan"></a>DHCP の展開を計画します。

DHCP サーバーの役割をインストールする前にキーの計画手順を次に示します。

### <a name="planning-dhcp-servers-and-dhcp-forwarding"></a>DHCP サーバーおよび DHCP 転送を計画する

DHCP メッセージはブロードキャスト メッセージであるため、ルーターは DHCP メッセージをサブネット間で転送しません。 複数のサブネットがあり、DHCP サービスを各サブネットに対して提供する場合、次のいずれかを行う必要があります。

-   DHCP サーバーを各サブネットにインストールします。

-   DHCP ブロードキャスト メッセージをサブネット間で転送するようにルーターを構成し、複数のスコープを DHCP サーバー上に構成します (各サブネットにつき 1 つのスコープ)。

ほとんどの場合、DHCP ブロードキャスト メッセージをサブネット間で転送するようにルーターを構成する方が、DHCP サーバーをネットワークの各物理セグメント上に展開するよりコスト効果が高くなります。

### <a name="planning-ip-address-ranges"></a>IP アドレスの範囲を計画する

各サブネットには、固有の IP アドレスの範囲を設定する必要があります。 これらの範囲は、DHCP サーバー上にスコープと共に表されます。

スコープとは、DHCP サービスを使用するサブネット上のコンピューターの IP アドレスを管理するためのグループです。 管理者は、まず各物理サブネットのスコープを作成します。次に、そのスコープを使用して、クライアントによって使用されるパラメーターを定義します。

スコープには、次のプロパティがあります。

-   IP アドレスの範囲。DHCP サービス リースの提供時に、この範囲のアドレスが使用されるか除外されます。

-   サブネット マスク。任意の IP アドレスのサブネット プレフィックスを決定します。

-   スコープ名。スコープの作成時に割り当てられます。

-   リース期間の値。動的に割り当てられた IP アドレスを受け取る DHCP クライアントに割り当てられます。

-   DHCP クライアントに割り当てるために構成された DHCP スコープ オプション。DNS サーバー IP アドレス、ルーター (デフォルト ゲートウェイ) IP アドレスなどがあります。

-   予約は、DHCP クライアントが常に同じ IP アドレスを受信するようにするために任意で使用されます。

サーバーを展開する前に、各サブネットに使用するサブネットと IP アドレスの範囲をリストします。

### <a name="planning-subnet-masks"></a>サブネット マスクを計画する

IP アドレス内のネットワーク ID およびホスト ID は、サブネット マスクを使用して識別されます。 各サブネット マスクは、IP アドレスのネットワーク ID 部分を示すすべて 1 から成る連続するビット グループと、ホスト IP 部分を示すすべてゼロ (0) から成る連続するビット グループで構成された 32 ビットの数値で表されます。

たとえば、IP アドレス 131.107.16.200 と一緒に使用されるサブネット マスクは、通常次の 32 ビットの 2 進数になります。

```
11111111 11111111 00000000 00000000
```

このサブネット マスクの番号は、ネットワーク ID とホスト ID セクションでは、この IP アドレスの両方の 16 ビット長であることを示す後に 16 0 ビット、16 の 1 のビットです。 通常、このサブネット マスクはピリオドで区切られた 10 進表記で "255.255.0.0" と表されます。

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

この問題を解決するために、DHCP スコープの除外範囲を作成できます。 除外範囲は、DHCP サーバーは使用できません、スコープの IP アドレスの範囲内の連続する範囲の IP アドレス。 除外範囲を作成した場合、DHCP サーバーはその範囲にあるアドレスを割り当てません。そのため、ユーザーは IP アドレスを競合させることなく、その範囲のアドレスを手動で割り当てることができます。

各スコープの除外範囲を作成して、DHCP サーバーによって分布から IP アドレスを除外できます。 静的 IP アドレスを使用して構成されているすべてのデバイスに対し、除外を適用する必要があります。 他のサーバー、非 DHCP クライアント、ディスクレス ワークステーション、またはルーティングとリモート アクセスおよび PPP クライアントに手動で割り当てた IP アドレスは、すべて除外アドレスに含める必要があります。

除外範囲は、将来のネットワークの拡張に対応できるよう、余分なアドレスを含めて構成することをお勧めします。 次の表は、10.0.0.1 ~ の IP アドレスの範囲を使用するスコープに対する除外範囲の例を示します 10.0.0.254 と 255.255.255.0 のサブネット マスク。

|構成項目|値の例|
|-----------------------|------------------|
|除外範囲の開始 IP アドレス|10.0.0.1|
|除外範囲の終了 IP アドレス|10.0.0.25|

### <a name="planning-tcpip-static-configuration"></a>TCP/IP の静的構成を計画する

ルーター、DHCP サーバー、DNS サーバーなどの特定のデバイスは、静的 IP アドレスを使用して構成する必要があります。 さらに、プリンターなどの追加のデバイスで、IP アドレスを固定させる必要のあるデバイスがあります。 各サブネットについて、静的に構成するデバイスをリストアップし、DHCP サーバー上で使用する除外範囲を計画して、その DHCP サーバーが静的に構成されたデバイスの IP アドレスをリースしないようにする必要があります。 除外範囲は、スコープ内の制限された連続する IP アドレスであり、DHCP サービスの提供から除外されます。 除外範囲を設定することで、これらの範囲内のすべてのアドレスは、サーバーからネットワーク上の DHCP クライアントに提供されないことが保証されます。

たとえば、サブネットの IP アドレスの範囲が 192.168.0.1 ~ 192.168.0.254 し、静的 IP アドレスを構成する 10 台のデバイスを使用している場合、192.168.0 の除外範囲を作成できます。*x* 10 個以上の IP アドレスが含まれるスコープ。192.168.0.1 192.168.0.15 ~。

この例では、10 個の除外された IP アドレスを使用してサーバーやその他のデバイスを静的 IP アドレスで構成し、残りの 5 個の IP アドレスは、将来追加する可能性がある新しいデバイスの静的構成のために確保されています。 この除外範囲では、DHCP サーバーには 192.168.0.16 ～ 192.168.0.254 までのアドレス プールが残ります。

AD DS および DNS の構成項目の追加の例は、次の表で提供されます。

|構成項目|値の例|
|-----------------------|------------------|
|ネットワーク接続バインディング|Ethernet|
|DNS サーバー設定|DC1.corp.contoso.com|
|優先 DNS サーバーの IP アドレス|10.0.0.2|
|スコープの値<br /><br />1. スコープ名<br />2. 開始 IP アドレス<br />3.終了 IP アドレス<br />4。サブネット マスク<br />5。デフォルト ゲートウェイ (オプション)<br />6。リース期間|1. プライマリ サブネット<br />2.  10.0.0.1<br />3.  10.0.0.254<br />4.  255.255.255.0<br />5.  10.0.0.1<br />6. 8 日|
|IPv6 DHCP サーバーの操作モード|無効|

## <a name="bkmk_lab"></a>テスト ラボでのこのガイドの使用

このガイドを使用して、運用環境で展開する前に、テスト ラボで DHCP を展開することができます。 

>[!NOTE]
>テスト ラボで DHCP を展開しない場合、セクションに進んで[デプロイ DHCP](#bkmk_deploy)します。

ラボの要件が物理サーバーまたは仮想マシンのどちらを使用しているかどうかによって異なります\(Vm\)、Active Directory ドメインの使用またはスタンドアロン DHCP サーバーを展開するかどうかとします。 

次の情報を使用すると、このガイドを使用して DHCP の展開をテストするのに必要がある最小限のリソースを決定します。

### <a name="test-lab-requirements-with-vms"></a>Vm でのテスト ラボの要件

Vm でのテスト ラボで DHCP を展開するには、次のリソース必要があります。

ドメインの展開やスタンドアロン展開には、Hyper として構成されている 1 つのサーバーが必要です。\-V ホスト。

**ドメインの展開**

この展開では、1 つの物理サーバー、1 つの仮想スイッチ、2 つの仮想サーバー、および 1 つの仮想クライアントが必要です。

物理サーバーで HYPER-V マネージャーでは、次の項目を作成します。

1. 1 つ**内部**仮想スイッチ。 作成しないでください、**外部**仮想スイッチは、ため場合、ハイパースレッディング\-V ホストは、DHCP サーバーを含むサブネット上で、テスト Vm は、DHCP サーバーから IP アドレスを受け取ります。 さらに、テスト DHCP サーバーを展開するは、サブネット上の他のコンピューターへの IP アドレスを割り当てることができます、Hyper\-V ホストがインストールされています。
1. 1 つの VM が作成した内部仮想スイッチに接続されている Active Directory Domain Services ドメイン コント ローラーとして構成されている Windows Server 2016 を実行します。 このガイドに一致すると、このサーバーは、静的に構成された IP アドレスは 10.0.0.2 とする必要があります。 AD DS の展開方法の詳細については、セクションをご覧ください。 **DC1 を展開する**では、Windows Server 2016[コア ネットワーク ガイド](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide#BKMK_deployADDNS01)します。
1. このガイドとを使用して、DHCP サーバーとして構成する Windows Server 2016 を実行している VM が仮想の内部に接続されている 1 つスイッチを作成します。 
1. 仮想の内部に接続されている Windows クライアント オペレーティング システムを実行している 1 つの VM は、作成したといる、DHCP サーバーが動的に割り当てる IP アドレスと DHCP オプション DHCP クライアントに確認に使用することを切り替えます。

**スタンドアロンの DHCP サーバー展開**

この展開では、1 つの物理サーバー、1 つの仮想スイッチ、1 つの virtual server、および 1 つの仮想クライアントが必要です。

物理サーバーで HYPER-V マネージャーでは、次の項目を作成します。

1. 1 つ**内部**仮想スイッチ。 作成しないでください、**外部**仮想スイッチは、ため場合、ハイパースレッディング\-V ホストは、DHCP サーバーを含むサブネット上で、テスト Vm は、DHCP サーバーから IP アドレスを受け取ります。 さらに、テスト DHCP サーバーを展開するは、サブネット上の他のコンピューターへの IP アドレスを割り当てることができます、Hyper\-V ホストがインストールされています。
1. このガイドとを使用して、DHCP サーバーとして構成する Windows Server 2016 を実行している VM が仮想の内部に接続されている 1 つスイッチを作成します。
1. 仮想の内部に接続されている Windows クライアント オペレーティング システムを実行している 1 つの VM は、作成したといる、DHCP サーバーが動的に割り当てる IP アドレスと DHCP オプション DHCP クライアントに確認に使用することを切り替えます。

### <a name="test-lab-requirements-with-physical-servers"></a>物理サーバーでのテスト ラボの要件

物理サーバーでのテスト ラボで DHCP を展開するには、次のリソース必要があります。

**ドメインの展開**

この展開では、1 つのハブまたはスイッチ、2 つの物理サーバーおよび 1 つの物理的なクライアントが必要です。

1. 1 つのイーサネット ハブまたはスイッチには、イーサネット ケーブルで物理コンピューターを接続できます。
1. 1 つの物理コンピューターが Active Directory Domain Services ドメイン コント ローラーとして構成されている Windows Server 2016 を実行します。 このガイドに一致すると、このサーバーは、静的に構成された IP アドレスは 10.0.0.2 とする必要があります。 AD DS の展開方法の詳細については、セクションをご覧ください。 **DC1 を展開する**では、Windows Server 2016[コア ネットワーク ガイド](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide#BKMK_deployADDNS01)します。
1. このガイドを使用して、DHCP サーバーとして構成する Windows Server 2016 を実行している 1 つの物理コンピューター。 
1. DHCP サーバーのことを確認するのに使用する Windows クライアント オペレーティング システムを実行して、1 つの物理コンピューターを動的に割り当てる IP アドレスと DHCP オプションを DHCP クライアントにします。

>[!NOTE]
>この展開のための十分なテスト マシンがない、運用環境のためこの構成は推奨されませんが、AD DS と DHCP の両方の 1 つのテスト コンピューターを使用できます。

**スタンドアロンの DHCP サーバー展開**

この展開では、1 つのハブまたはスイッチ、1 つの物理サーバー、および 1 つの物理的なクライアントが必要です。

1. 1 つのイーサネット ハブまたはスイッチには、イーサネット ケーブルで物理コンピューターを接続できます。
2. このガイドを使用して、DHCP サーバーとして構成する Windows Server 2016 を実行している 1 つの物理コンピューター。 
3. DHCP サーバーのことを確認するのに使用する Windows クライアント オペレーティング システムを実行して、1 つの物理コンピューターを動的に割り当てる IP アドレスと DHCP オプションを DHCP クライアントにします。


## <a name="bkmk_deploy"></a>DHCP を展開します。

このセクションでは、1 つのサーバーの DHCP の展開を使用できる Windows PowerShell コマンドの例を提供します。 サーバーでこれらの例のコマンドを実行する前に、ネットワークと環境に一致するようにコマンドを変更する必要があります。 

たとえば、コマンドを実行する前に、次の項目のコマンドの例の値を置き換える必要があります。

- コンピューター名
- (サブネットごとに 1 つのスコープ) を構成する各範囲の IP アドレスの範囲
- 構成する各 IP アドレス範囲のサブネット マスク
- 各スコープのスコープ名
- 各スコープの除外範囲
- デフォルト ゲートウェイ、ドメイン名、DNS または WINS サーバーなどの DHCP オプションの値
- インターフェイス名

>[!IMPORTANT]
>確認し、コマンドを実行する前に、環境内のすべてのコマンドを変更します。

### <a name="where-to-install-dhcp---on-a-physical-computer-or-a-vm"></a>物理コンピューターまたは VM で DHCP のインストール - 場所でしょうか。

DHCP サーバーの役割をインストールするには、物理コンピューターまたは仮想マシンで\(VM\) Hyper にインストールされている\-V ホスト。 である、HYPER-V仮想スイッチにVMの仮想ネットワークアダプターを接続する場合は、VMにDHCPをインストールして、DHCPサーバー、HYPER-Vホストが接続されている物理ネットワーク上のコンピューターにIPアドレスの割り当てを提供する、する必要があります**外部**します。

詳細については、セクションをご覧ください。 **、Hyper-v マネージャーで仮想スイッチの作成**、トピックの「[仮想ネットワークの作成](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/connect-to-network)です。

### <a name="run-windows-powershell-as-an-administrator"></a>Windows PowerShell を管理者として実行します。

次の手順を使用すると、管理者特権で Windows PowerShell を実行します。

1. を Windows Server 2016 を実行するコンピューターで次のようにクリックします。**開始**、Windows PowerShell アイコンを右クリックします。 メニューが表示されます。 

2. メニューで、次のようにクリックします。**詳細**、 をクリックし、**管理者として実行**します。 メッセージが表示されたら、コンピューターで管理者特権を持つアカウントの資格情報を入力します。 ログオンしているコンピューターにユーザー アカウントが管理者レベルのアカウントの場合、資格情報プロンプトは受け取りません。

3. Windows PowerShell を管理者特権で開きます。

### <a name="rename-the-dhcp-server-and-configure-a-static-ip-address"></a>DHCP サーバーの名前を変更し、静的 IP アドレスを構成します。

されていない場合は、DHCP サーバーの名前を変更して、サーバーの静的 IP アドレスを構成する次の Windows PowerShell コマンドを使用できます。

**静的 IP アドレスを構成します。**

正しい DNS サーバーの IP アドレスと DHCP サーバーの TCP/IP プロパティを構成して、DHCP サーバーに静的 IP アドレスを割り当てるには、次のコマンドを使用できます。 また、この例のインターフェイス名と IP アドレスを、コンピューターの構成に使用する値に置き換える必要があります。

 `New-NetIPAddress -IPAddress 10.0.0.3 -InterfaceAlias "Ethernet" -DefaultGateway 10.0.0.1 -AddressFamily IPv4 -PrefixLength 24`

 `Set-DnsClientServerAddress -InterfaceAlias "Ethernet" -ServerAddresses 10.0.0.2`

これらのコマンドの詳細については、次のトピックを参照してください。

- [New-NetIPAddress](https://technet.microsoft.com/itpro/powershell/windows/tcpip/new-netipaddress)
- [Set-DnsClientServerAddress](https://technet.microsoft.com/itpro/powershell/windows/dns-client/set-dnsclientserveraddress)

**コンピューターを名前します。**

次のコマンドを使用する名前を変更し、コンピューターを再起動します。

`Rename-Computer -Name DHCP1`

 `Restart-Computer`

これらのコマンドの詳細については、次のトピックを参照してください。

- [Rename-computer](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.management/rename-computer)
- [Restart-Computer](https://msdn.microsoft.com/powershell/reference/4.0/microsoft.powershell.management/restart-computer)

### <a name="join-the-computer-to-the-domain-optional"></a>コンピューターをドメインに参加させる\((省略可能)\)

Active Directory ドメイン環境で、DHCP サーバーをインストールする場合は、コンピューターをドメインに参加する必要があります。 管理者特権で Windows PowerShell を開き、ドメインの NetBios 名を交換した後、次のコマンドを実行**CORP**環境内の適切な値。

    Add-Computer CORP

メッセージが表示されたら、コンピューターをドメインに参加する権限を持つドメイン ユーザー アカウントの資格情報を入力します。 

    Restart-Computer

Add-computer コマンドの詳細については、次のトピックを参照してください。

- [コンピューターの追加](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.management/add-computer)

### <a name="install-dhcp"></a>DHCP をインストールします。

コンピューターの再起動後に管理者特権で Windows PowerShell を開いてし、次のコマンドを実行して DHCP をインストールします。

    Install-WindowsFeature DHCP -IncludeManagementTools

このコマンドの詳細については、次のトピックを参照してください。

- [Install-windowsfeature](https://technet.microsoft.com/itpro/powershell/windows/server-manager/install-windowsfeature)

### <a name="create-dhcp-security-groups"></a>DHCP セキュリティ グループを作成します。

セキュリティ グループを作成するには、ネットワーク シェルを実行する必要があります\(netsh\) Windows PowerShell でコマンドを新しいグループがアクティブになるように、DHCP サービスを再起動します。

DHCP サーバーで次の netsh コマンドを実行すると、 **DHCP Administrators**と**DHCP Users**でセキュリティ グループが作成されます**ローカル ユーザーとグループ**DHCP にサーバー。

    netsh dhcp add securitygroups

次のコマンドは、ローカル コンピューター上の DHCP サービスを再起動します。

    Restart-service dhcpserver

これらのコマンドの詳細については、次のトピックを参照してください。

- [ネットワーク シェル (Netsh)](../netsh/netsh.md)
- [サービスを再開](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.management/restart-service)

### <a name="authorize-the-dhcp-server-in-active-directory-optional"></a>Active Directory で DHCP サーバーの承認\((省略可能)\)

ドメイン環境で DHCP をインストールする場合は、ドメインで動作する DHCP サーバーを承認するために次の手順を実行する必要があります。

>[!NOTE]
>Active Directory ドメインにインストールされている承認されていない DHCP サーバーは、正常に機能できないし、DHCP クライアントに IP アドレスをリースしません。 未承認の DHCP サーバーの自動無効化は、未承認の DHCP サーバーがネットワーク上のクライアントに正しくない IP アドレスを割り当てることを防ぐセキュリティ機能です。

DHCP サーバーを Active Directory で承認された DHCP サーバーの一覧に追加するのには、次のコマンドを使用できます。 

>[!NOTE]
>ドメイン環境がいない場合では、このコマンドは実行されません。

 `Add-DhcpServerInDC -DnsName DHCP1.corp.contoso.com -IPAddress 10.0.0.3`

DHCP サーバーが Active Directory で許可されていることを確認するには、次のコマンドを使用できます。

    Get-DhcpServerInDC

Windows PowerShell に表示される結果の例を次に示します。

    
        IPAddress   DnsName
        ---------   -------
        10.0.0.3    DHCP1.corp.contoso.com
    

これらのコマンドの詳細については、次のトピックを参照してください。

- [Add-DhcpServerInDC](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/add-dhcpserverindc)
- [Get-DhcpServerInDC](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/get-dhcpserverindc)

### <a name="notify-server-manager-that-post-install-dhcp-configuration-is-complete-optional"></a>投稿のサーバー マネージャーに通知\-DHCP 構成のインストールが完了したら\((省略可能)\)

投稿を行った後\-セキュリティ グループを作成して、Active Directory、サーバー マネージャーで、DHCP サーバーの承認などのインストール タスクは、その投稿を示すユーザー インターフェイスで、アラートを表示も可能性があります\-DHCP ポスト インストールの構成ウィザードを使用してインストール手順を完了する必要があります。

これを今すぐ防ぐ\-されないようにこの Windows PowerShell コマンドを使用して、次のレジストリ キーを構成することでサーバー マネージャーでの不要なと不正確なメッセージ。

    Set-ItemProperty –Path registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ServerManager\Roles\12 –Name ConfigurationState –Value 2

このコマンドの詳細については、次のトピックを参照してください。

- [Set-ItemProperty](https://msdn.microsoft.com/powershell/reference/4.0/microsoft.powershell.management/set-itemproperty?f=255&MSPPError=-2147217396)

### <a name="set-server-level-dns-dynamic-update-configuration-settings-optional"></a>サーバー レベルの DNS 動的更新の構成設定を設定\((省略可能)\)

DHCP サーバーが DHCP クライアント コンピューターの DNS 動的更新を実行する場合は、この設定を構成するには、次のコマンドを実行することができます。 これは、サーバー レベルの設定をいないをスコープ レベルの設定、サーバーを構成するすべてのスコープには影響があるためにです。 このコマンドの例では、クライアントは、少なくとも期限が切れると、クライアントの DNS リソース レコードを削除する DHCP サーバーも構成します。

    Set-DhcpServerv4DnsSetting -ComputerName "DHCP1.corp.contoso.com" -DynamicUpdates "Always" -DeleteDnsRRonLeaseExpiry $True

次のコマンドを使用すると、DHCP サーバーを登録または DNS サーバー上のクライアント レコードを登録解除に使用する資格情報を構成します。 この例では、DHCP サーバーの資格情報を保存します。 最初のコマンドを使用して**Get-credential**を作成する、 **PSCredential**オブジェクト、および内のオブジェクトを格納し、 **$Credential**変数。 コマンドはユーザー名とパスワードを要求する、そのため、DNS サーバー上のリソース レコードを更新する権限を持つアカウントの資格情報を指定することを確認します。

    
    $Credential = Get-Credential
    Set-DhcpServerDnsCredential -Credential $Credential -ComputerName "DHCP1.corp.contoso.com"
    

これらのコマンドの詳細については、次のトピックを参照してください。

- [Set-DhcpServerv4DnsSetting](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/set-dhcpserverv4dnssetting)
- [Set-DhcpServerDnsCredential](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/set-dhcpserverdnscredential)

### <a name="configure-the-corpnet-scope"></a>企業ネットワークのスコープを構成します。

DHCP インストールが完了した後は、構成、企業ネットワークのスコープをアクティブ化し、スコープの除外範囲を作成、および DHCP オプションの既定のゲートウェイ、DNS サーバーの IP アドレス、および DNS ドメイン名を構成する次のコマンドを使用できます。

    
    Add-DhcpServerv4Scope -name "Corpnet" -StartRange 10.0.0.1 -EndRange 10.0.0.254 -SubnetMask 255.255.255.0 -State Active`
    
    Add-DhcpServerv4ExclusionRange -ScopeID 10.0.0.0 -StartRange 10.0.0.1 -EndRange 10.0.0.15`
    
    Set-DhcpServerv4OptionValue -OptionID 3 -Value 10.0.0.1 -ScopeID 10.0.0.0 -ComputerName DHCP1.corp.contoso.com`
    
    Set-DhcpServerv4OptionValue -DnsDomain corp.contoso.com -DnsServer 10.0.0.2
    

これらのコマンドの詳細については、次のトピックを参照してください。

- [Add-DhcpServerv4Scope](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/add-dhcpserverv4scope)
- [Add-DhcpServerv4ExclusionRange](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/add-dhcpserverv4exclusionrange)
- [Set-DhcpServerv4OptionValue](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/set-dhcpserverv4optionvalue)

### <a name="configure-the-corpnet2-scope-optional"></a>Corpnet2 スコープ構成\(オプション\)

DHCP 転送が有効になっているルーターを持つ最初のサブネットに接続されている 2 番目のサブネットがあれば、この例の Corpnet2 をという名前で 2 つ目のスコープを追加するのに、次のコマンドを使用できます。 この例は、除外範囲と既定のゲートウェイ IP アドレスにも構成\(ルーターの IP アドレス、サブネット上\)Corpnet2 サブネット。

 `Add-DhcpServerv4Scope -name "Corpnet2" -StartRange 10.0.1.1 -EndRange 10.0.1.254 -SubnetMask 255.255.255.0 -State Active`

 `Add-DhcpServerv4ExclusionRange -ScopeID 10.0.1.0 -StartRange 10.0.1.1 -EndRange 10.0.1.15`

 `Set-DhcpServerv4OptionValue -OptionID 3 -Value 10.0.1.1 -ScopeID 10.0.1.0 -ComputerName DHCP1.corp.contoso.com`

この DHCP サーバーによって処理され、追加のサブネットがあれば、各サブネットのスコープを追加するコマンドのパラメーターのすべての異なる値を使用して、これらのコマンドを繰り返すことができます。

>[!IMPORTANT]
>DHCP クライアントと DHCP サーバーの間のすべてのルーターが DHCP メッセージ転送用に構成されていることを確認します。 DHCP 転送を構成する方法については、ルーターのドキュメントを参照してください。

## <a name="bkmk_verify"></a>サーバー機能を確認します。

DHCP サーバーが DHCP クライアントに IP アドレスの動的な割り当てを提供していることを確認するには、サービスのサブネットに別のコンピューターを接続できます。 ネットワーク アダプターと、コンピューターの電源をオンにイーサネット ケーブルを接続した後は、IP アドレスを DHCP サーバーから要求します。 使用して正常に構成を確認することができます、 **ipconfig/all**コマンドし、結果の確認、または接続テストを実行するようしようとすると、Windows でのブラウザーまたはファイル共有での Web リソースにアクセスエクスプ ローラーまたは他のアプリケーション。

クライアントが DHCP サーバーから IP アドレスを受信しなかった場合は、次のトラブルシューティングの手順を実行します。

1. イーサネット ケーブルが両方のコンピューターと、イーサネット スイッチ、ハブ、またはルーターに接続されていることを確認します。
1. クライアント コンピューターをルーターで DHCP サーバーから分離されたネットワーク セグメントに接続する場合は、DHCP メッセージを転送するルーターが構成されていることを確認します。
1. Active Directory から承認された DHCP サーバーの一覧を取得するには、次のコマンドを実行して Active Directory、DHCP サーバーが許可されていることを確認します。 [Get DhcpServerInDC](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/get-dhcpserverindc)します。
1. DHCP コンソールを開くことで、スコープがアクティブ化されることを確認\(サーバー マネージャー、**ツール**、 **DHCP**\)が右のスコープを確認してサーバーツリーを展開し、\-各スコープをクリックします。 表示されるメニューには、選択範囲が含まれている場合**アクティブ化**、 をクリックして**Activate**します。 \(メニューの選択が読み取る場合は、スコープが既にアクティブ化、**非アクティブ化**します。\) 

## <a name="bkmk_dhcpwps"></a>DHCP 用 Windows PowerShell コマンド

次の参照はコマンドの説明と構文を Windows Server 2016 のすべての DHCP サーバーの Windows PowerShell コマンドを提供します。 トピックには、コマンドの先頭の動詞をなどに基づいてアルファベット順にコマンドが表示されます。**取得**または**設定**します。

>[!NOTE]
>Windows Server 2012 R2 で Windows Server 2016 のコマンドを使用することができません。

- [DhcpServer モジュール](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/index)

次の参照はコマンドの説明と構文を Windows Server 2012 R2 のすべての DHCP サーバーの Windows PowerShell コマンドを提供します。 トピックには、コマンドの先頭の動詞をなどに基づいてアルファベット順にコマンドが表示されます。**取得**または**設定**します。

>[!NOTE]
>Windows Server 2016 では、Windows Server 2012 R2 のコマンドを使用できます。

- [Windows PowerShell の DHCP サーバー コマンドレット](https://technet.microsoft.com/library/jj590751.aspx)

## <a name="bkmk_list"></a>このガイドでの Windows PowerShell コマンドの一覧

コマンドと、このガイドで使用される値の例の簡単な一覧を次に示します。

    
    New-NetIPAddress -IPAddress 10.0.0.3 -InterfaceAlias "Ethernet" -DefaultGateway 10.0.0.1 -AddressFamily IPv4 -PrefixLength 24
    Set-DnsClientServerAddress -InterfaceAlias "Ethernet" -ServerAddresses 10.0.0.2
    Rename-Computer -Name DHCP1
    Restart-Computer
    
    Add-Computer CORP
    Restart-Computer
    
    Install-WindowsFeature DHCP -IncludeManagementTools
    netsh dhcp add securitygroups
    Restart-service dhcpserver
    
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
    


