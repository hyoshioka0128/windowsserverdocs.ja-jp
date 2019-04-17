---
title: Windows PowerShell を使用した DHCP を展開します。
description: このトピックの「を使用して、ネットワーク上の 1 つまたは複数のサブネットに接続されている IPv4 DHCP クライアント自動の IP アドレスと DHCP オプションを提供する Windows Server 2016 インターネット プロトコル (IP) バージョン 4 の DHCP サーバーを展開することができます。
ms.prod: windows-server-threshold
ms.technology: networking-dhcp
ms.topic: article
ms.assetid: 7110ad21-a33e-48d5-bb3c-129982913bc8
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2be3c02f32229c9b9ee411f5e97305776f9825d8
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="deploy-dhcp-using-windows-powershell"></a>Windows PowerShell を使用した DHCP を展開します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このガイドでは、ネットワーク上の 1 つまたは複数のサブネットに接続されている IPv4 DHCP クライアントに IP アドレスと DHCP オプションを自動的に割り当てるインターネット プロトコル (IP) バージョン 4 の動的ホスト構成プロトコル \(DHCP\) サーバーを展開する Windows PowerShell を使用する方法について説明します。

>[!NOTE]
>Word 形式では、このドキュメントは、TechNet ギャラリーからダウンロードするを参照してください。[展開 DHCP を使用して Windows PowerShell で Windows Server 2016](https://gallery.technet.microsoft.com/Deploy-DHCP-Using-Windows-246dd293)します。

アドレスは IP の割り当てに DHCP サーバーを使用して、ネットワーク上のすべてのコンピューターですべてのネットワーク アダプターの TCP/IP v4 設定を手動で構成する必要はないために管理オーバーヘッドで保存します。 DHCP、TCP/IP v4 構成は自動的にコンピューターの場合に実行またはその他の DHCP クライアントがネットワークに接続されています。

スタンドアロン サーバー、または Active Directory ドメインの一部として、ワークグループ内、DHCP サーバーを展開することができます。

このガイドには、次のセクションが含まれています。

- [DHCP の展開の概要](#bkmk_overview)
- [テクノロジの概要](#bkmk_technologies)
- [DHCP の展開を計画します。](#bkmk_plan)
- [テスト ラボでこのガイドを使用します。](#bkmk_lab)
- [DHCP を展開します。](#bkmk_deploy)
- [サーバー機能を確認します。](#bkmk_verify)
- [DHCP 用 Windows PowerShell コマンド](#bkmk_dhcpwps)
- [このガイドで Windows PowerShell コマンドの一覧](#bkmk_list)

## <a name="bkmk_overview"></a>DHCP の展開の概要

次の図は、このガイドを使用して展開できるシナリオを示しています。 シナリオには、Active Directory ドメインに 1 つの DHCP サーバーが含まれています。 サーバーは、2 つの異なるサブネット上の DHCP クライアントに IP アドレスを提供するように構成します。 サブネットは、DHCP 転送が有効にしたルーターで区切られます。

![DHCP ネットワーク トポロジの概要](../../media/Core-Network-Guide/cng16_overview.jpg)

## <a name="bkmk_technologies"></a>テクノロジの概要

次のセクションでは、DHCP と TCP/IP の概要を提供します。

### <a name="dhcp-overview"></a>DHCP の概要

DHCP は、ホストの IP 構成の管理を合理化するための IP 標準です。 DHCP 標準は、ネットワーク上の DHCP 対応クライアントの IP アドレスの動的な割り当てとその他の関連する構成詳細を管理する手段として DHCP サーバーの使用を示します。

DHCP を使用すると、DHCP サーバーを使用して、コンピューターや、静的 IP アドレスを持つすべてのデバイスを手動で構成するのではなく、ローカル ネットワーク上のプリンターなど、他のデバイスに IP アドレスを動的に割り当てることができます。

TCP/IP ネットワーク上のすべてのコンピューターは、IP アドレスおよび関連付けられたサブネット マスクは、ホスト コンピューターと、コンピューターが接続されているサブネットの両方を識別するため、一意の IP アドレスにすることが必要です。 DHCP を使用すると、DHCP クライアントとして構成されているすべてのコンピューターが、ネットワークの場所およびサブネットに適切な IP アドレスを受信することを確認できますデフォルト ゲートウェイや DNS サーバーなどの DHCP オプションを使用して提供して、できる自動的に DHCP クライアント、ネットワーク上で正しく機能する必要があるという情報でします。

IP ベース ネットワークでは、DHCP によって複雑さとコンピューターの構成にかかわる管理作業の量が削減されます。

### <a name="tcpip-overview"></a>TCP/IP の概要

既定では、Windows Server および Windows クライアント オペレーティング システムのすべてのバージョンは IP バージョン 4 のネットワーク接続を自動的に IP アドレスと DHCP サーバーから DHCP オプションと呼ばれる、その他の情報を取得する構成の TCP/IP 設定があります。 このため、コンピューターがサーバーのコンピューターまたはその他のデバイスを手動で構成して、静的 IP アドレスを必要とする場合を除き、TCP/IP 設定を手動で構成する必要はありません。 

たとえば、ある手動で構成する、DHCP サーバーの IP アドレスと DNS サーバーと Active Directory Domain Services \(AD DS\) を実行しているドメイン コントローラーの IP アドレスをお勧めします。

Windows Server 2016 での TCP/IP は次のよう

-   ネットワークの業界標準のネットワーク プロトコルに基づくソフトウェア。

-   ローカル エリア ネットワーク (LAN) とワイド エリア ネットワーク (WAN) 環境の両方に Windows ベースのコンピューターの接続をサポートしているルーティング可能なエンタープライズ ネットワーク プロトコルです。

-   コア テクノロジおよび情報を共有するために異種システムで Windows ベースのコンピューターを接続するためのユーティリティです。

-   Web およびファイル転送プロトコル (FTP) サーバーなどのグローバル インターネット サービスにアクセスするための基盤です。

-   堅牢かつスケーラブルなクロスプラット フォーム、クライアント/サーバー フレームワーク。

TCP/IP には、Windows ベースのコンピュータに接続し、他の Microsoft を含む、Microsoft 以外のシステムと情報を共有できるようにする基本的な TCP/IP ユーティリティが用意されています。

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

- タブレット、携帯電話をワイヤード (有線) イーサネットと無線の 802.11 テクノロジを有効になっています。

## <a name="bkmk_plan"></a>DHCP の展開を計画します。

DHCP サーバーの役割をインストールする前に重要な計画手順を次に示します。

### <a name="planning-dhcp-servers-and-dhcp-forwarding"></a>DHCP サーバーおよび DHCP 転送を計画します。

DHCP メッセージはブロードキャスト メッセージであるために、ルーターでサブネット間では転送されません。 複数のサブネットがある各サブネットの DHCP サービスを提供する場合、次のいずれかを行う必要があります。

-   各サブネット上の DHCP サーバーをインストールします。

-   DHCP ブロードキャスト メッセージをサブネット間で転送し、サブネットごとに 1 つのスコープ、DHCP サーバーで複数のスコープを構成するようにルーターを構成します。

ほとんどの場合、DHCP ブロードキャスト メッセージを転送するようにルーターを構成するは、ネットワークの各物理セグメント上の DHCP サーバーを展開するよりコスト効率です。

### <a name="planning-ip-address-ranges"></a>IP アドレス範囲を計画します。

各サブネットには、独自の一意の IP アドレス範囲が必要です。 これらの範囲は、スコープと DHCP サーバーで表されます。

スコープは、DHCP サービスを使用するサブネット上のコンピューターの IP アドレスの管理グループです。 管理者は、まず各物理サブネットのスコープを作成し、スコープを使用して、クライアントで使用されるパラメータを定義します。

スコープには、次のプロパティ。

-   DHCP サービス リースの提供に使用されるアドレス、または除外する範囲の IP アドレス。

-   サブネット マスク: 特定の IP アドレスのサブネット プレフィックスを決定します。

-   作成時に割り当てられているスコープ名。

-   リース期間の値を動的に割り当てられた IP アドレスを受信する DHCP クライアントに割り当てられています。

-   DNS サーバーの IP アドレス、ルーターまたはデフォルト ゲートウェイの IP アドレスなどの DHCP クライアントに割り当て用に構成された DHCP スコープ オプション。

-   予約は必要に応じて、DHCP クライアントが常に同じ IP アドレスを受信することを確認するために使用します。

サーバーを展開する前に、サブネット、および各サブネットに使用する IP アドレスの範囲の一覧を表示します。

### <a name="planning-subnet-masks"></a>サブネット マスクを計画します。

ネットワーク Id および IP アドレス内のホスト Id は、サブネット マスクを使用して識別されます。 各サブネット マスクは 32 ビットの数値のすべての連続するビット グループを使用するネットワークを識別するには、(1) ID とすべてゼロ (0)、IP アドレスのホスト ID 部分を識別します。

たとえば、IP アドレス 131.107.16.200 で通常使用するサブネット マスクは、次の 32 ビット 2 進数を示します。

```
11111111 11111111 00000000 00000000
```

このサブネット マスクの数値は、ネットワーク ID とホスト ID セクションでは、この IP アドレスのどちらも 16 ビット長であることを示す 16 0 ビット、続けて 16 の 1 のビットです。 通常、このサブネット マスクは 255.255.0.0 としてはドット区切り 10 進表記で表示されます。

次の表は、インターネット アドレス クラスのサブネット マスクを表示します。

|アドレス クラス|サブネット マスクのビット|サブネット マスク|
|-----------------|------------------------|---------------|
|クラス A|11111111 00000000 00000000 00000000|255.0.0.0|
|クラス B|11111111 11111111 00000000 00000000|255.255.0.0|
|クラス C|11111111 11111111 11111111 00000000|255.255.255.0|

Dhcp スコープを作成する、スコープの IP アドレスの範囲を入力して、DHCP では、これらの既定のサブネット マスクの値が提供されます。 通常、既定のサブネット マスクの値は、特別な要件なくほとんどのネットワークと各 IP ネットワーク セグメントが 1 つの物理ネットワークに対応する場所で受け入れられます。

場合によっては、カスタマイズしたサブネット マスクを使用して IP サブネットを実装することができます。 IP サブネット、サブネットで、元のクラスベースのネットワーク ID の区分を指定する IP アドレスの既定のホスト ID 部分に分割することができます。

サブネット マスクの長さをカスタマイズして、実際のホスト ID に使用されるビット数を減らすことができます。

アドレス指定とルーティングの問題を防ぐためには、ネットワーク セグメント上のすべての TCP/IP コンピューターが同じサブネット マスクを使用して、コンピューターまたはデバイスごとに一意の IP アドレスがあることを確認してください。

### <a name="planning-exclusion-ranges"></a>除外範囲を計画します。

DHCP サーバーのスコープを作成するときに、すべての DHCP サーバーのコンピューターやその他のデバイスなどの DHCP クライアントにリースが許可されている IP アドレスが含まれる IP アドレスの範囲を指定します。 移動し、一部のサーバーを手動で構成し、DHCP サーバーを使用している同じ IP アドレスの範囲から IP アドレスを静的なその他のデバイス、誤って IP アドレスの競合を作成することができます、して、DHCP サーバーがある両方同じ IP アドレスを割り当てるさまざまなデバイスにします。

この問題を解決するには、DHCP スコープの除外範囲を作成できます。 除外範囲は、DHCP サーバーは使用できません、スコープの IP アドレスの範囲内の連続した範囲の IP アドレスです。 除外範囲を作成する場合、DHCP サーバーにすると、競合する IP アドレスを作成することがなく、これらのアドレスを手動で割り当てることが、その範囲内のアドレスは割り当てられません。

各スコープに対して除外範囲を作成することで、DHCP サーバーによって配布から IP アドレスを除外できます。 静的 IP アドレスが構成されているすべてのデバイスの除外を使用する必要があります。 除外されたアドレスでは、その他のサーバー、非 DHCP クライアント、ディスクレス ワークステーション、またはルーティングとリモート アクセスおよび PPP クライアントを手動で割り当てられているすべての IP アドレスを含める必要があります。

ネットワークの将来の成長に対応する余分なアドレスを持つ、除外範囲を構成することをお勧めします。 次の表は、10.0.0.1 ~ の IP アドレスの範囲を使用するスコープに対する除外範囲の例を示します 10.0.0.254 と 255.255.255.0 のサブネット マスク。

|構成項目|値の例|
|-----------------------|------------------|
|除外範囲の IP アドレスの開始|10.0.0.1|
|除外範囲終了 IP アドレス|10.0.0.25|

### <a name="planning-tcpip-static-configuration"></a>TCP/IP の静的構成を計画します。

静的 IP アドレスを持つ、ルーター、DHCP サーバー、および DNS サーバーなどの特定のデバイスを構成する必要があります。 さらに、追加のデバイス、常に確認するには、プリンターなど、同じ IP アドレスを持っているがあります。 各サブネットの静的を構成するデバイスの一覧し、DHCP サーバーが静的に構成されたデバイスの IP アドレスをリースしていないことを確認する DHCP サーバーで使用する場合、除外範囲を計画します。 除外範囲は、DHCP サービスの提供から除外されて、スコープ内の IP アドレスの限られたシーケンスです。 除外範囲は、ネットワーク上の DHCP クライアントにこれらの範囲内のアドレスがサーバーによって提供しないことを保証します。

たとえば、サブネットの IP アドレスの範囲が 192.168.0.1 ~ 192.168.0.254 し、静的 IP アドレスを構成する 10 台のデバイスを使用している場合、192. 168.0 除外範囲を作成できます。*x* 10 個以上の IP アドレスを含むスコープ: 192.168.0.1 ~ 192.168.0.15 までです。

この例では 10 個の除外された IP アドレスを使用して静的 IP アドレスを持つサーバーおよびその他のデバイスを構成して追加の 5 つの IP アドレスは、将来追加する新しいデバイスの静的構成の使用可能な残されます。 この除外範囲で DHCP サーバーには 192.168.0.16 192.168.0.254 経由のアドレス プールが残ります。

AD DS および DNS の構成項目の追加の例を次の表に示します。

|構成項目|値の例|
|-----------------------|------------------|
|ネットワーク接続バインディング|イーサネット|
|DNS サーバーの設定|DC1.corp.contoso.com|
|優先 DNS サーバーの IP アドレス|10.0.0.2|
|スコープの値<br /><br />1。 スコープ名<br />2. 開始 IP アドレス<br />3. 終了 IP アドレス<br />4. サブネット マスク<br />5. デフォルト ゲートウェイ (省略可能)<br />6. リース期間|1。 プライマリ サブネット<br />2.  10.0.0.1<br />3.  10.0.0.254<br />4.  255.255.255.0<br />5.  10.0.0.1<br />6. 8 日|
|IPv6 DHCP サーバーの操作モード|有効になっていません|

## <a name="bkmk_lab"></a>テスト ラボでこのガイドを使用します。

このガイドを使用して、実稼働環境で展開する前に、テスト ラボで DHCP を展開することができます。 

>[!NOTE]
>テスト ラボで DHCP を展開しない場合は、セクションを省略できます[展開 DHCP](#bkmk_deploy)します。

ラボの要件は、物理サーバーまたは仮想マシン \(VMs\) を使用しているかどうかと、Active Directory ドメインを使用してまたはスタンドアロンの DHCP サーバーを展開するかどうかによって異なります。 

次の情報を使用すると、このガイドを使用して、DHCP の展開をテストする必要があります最小のリソースを決定します。

### <a name="test-lab-requirements-with-vms"></a>Vm のテスト ラボの要件

Vm のテスト ラボで DHCP を展開するには、次のリソース必要があります。

ドメインの展開やスタンドアロン展開で、Hyper\ V ホストとして構成されている 1 台のサーバーが必要です。

**ドメインの展開**

この展開では、1 つの物理サーバー、仮想スイッチは 1 つ、2 つの仮想サーバーおよび仮想の 1 台のクライアントが必要です。

物理サーバーで Hyper-V マネージャーで、次の項目を作成します。

1. 1 つ**内部**仮想スイッチ。 作成しない、**外部**仮想切り替えるには、テスト Vm は、DHCP サーバーから IP アドレスを取得して Hyper\ V ホストが DHCP サーバーが含まれるサブネット上にある場合は、あるためです。 さらに、展開するテストの DHCP サーバーは Hyper\ V ホストがインストールされているサブネット上の他のコンピューターに IP アドレスを割り当てる可能性があります。
1. 内部仮想スイッチに接続されている Active Directory ドメイン サービスでドメイン コントローラーとして構成されている Windows Server 2106 を実行している 1 つの VM を作成します。 このガイドを一致するには、このサーバーは 10.0.0.2 の静的に構成された IP アドレスが必要です。 AD DS の展開の詳細については、セクションを参照して**DC1 を展開する**Windows Server 2016 で[コア ネットワーク ガイド](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide#BKMK_deployADDNS01)します。
1. このガイドとを使用して、DHCP サーバーとして構成する Windows Server 2106 を実行している VM が仮想内部に接続されているスイッチを作成します。 
1. 仮想内部に接続されている Windows クライアント オペレーティング システムを実行している 1 つの VM では、作成したとを確認する、DHCP サーバーが動的に割り当てる IP アドレスと DHCP オプション DHCP クライアントに使用することを切り替えます。

**スタンドアロンの DHCP サーバーの展開**

この展開では、1 つの物理サーバー、仮想スイッチは 1 つ、1 つの virtual server、および仮想の 1 台のクライアントが必要です。

物理サーバーで Hyper-V マネージャーで、次の項目を作成します。

1. 1 つ**内部**仮想スイッチ。 作成しない、**外部**仮想切り替えるには、テスト Vm は、DHCP サーバーから IP アドレスを取得して Hyper\ V ホストが DHCP サーバーが含まれるサブネット上にある場合は、あるためです。 さらに、展開するテストの DHCP サーバーは Hyper\ V ホストがインストールされているサブネット上の他のコンピューターに IP アドレスを割り当てる可能性があります。
1. このガイドとを使用して、DHCP サーバーとして構成する Windows Server 2106 を実行している VM が仮想内部に接続されているスイッチを作成します。
1. 仮想内部に接続されている Windows クライアント オペレーティング システムを実行している 1 つの VM では、作成したとを確認する、DHCP サーバーが動的に割り当てる IP アドレスと DHCP オプション DHCP クライアントに使用することを切り替えます。

### <a name="test-lab-requirements-with-physical-servers"></a>物理サーバーとテスト ラボの要件

物理サーバーとテスト ラボで DHCP を展開するには、次のリソースが必要です。

**ドメインの展開**

この展開では、1 つのハブまたはスイッチ、2 つの物理サーバーと 1 台の物理的なクライアントが必要です。

1. 1 つのイーサネット ハブまたはスイッチにイーサネット ケーブルを使って、物理コンピューターを接続することができます
1. Active Directory ドメイン サービスでドメイン コントローラーとして構成されている Windows Server 2106 を実行している 1 台の物理コンピューターです。 このガイドを一致するには、このサーバーは 10.0.0.2 の静的に構成された IP アドレスが必要です。 AD DS の展開の詳細については、セクションを参照して**DC1 を展開する**Windows Server 2016 で[コア ネットワーク ガイド](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide#BKMK_deployADDNS01)します。
1. このガイドを使用して DHCP サーバーとして構成する Windows Server 2106 を実行している 1 台の物理コンピューターです。 
1. DHCP サーバーに使用できることを確認する Windows クライアント オペレーティング システムを実行している 1 台の物理コンピューターが動的に割り当てる IP アドレスと DHCP オプション DHCP クライアントにします。

>[!NOTE]
>十分なこの展開のテスト コンピューターを持っていない場合は、ただし、この構成は、運用環境には推奨されません、AD DS と DHCP の両方の 1 つのテスト コンピューターを使用できます。

**スタンドアロンの DHCP サーバーの展開**

この展開では、1 つのハブまたはスイッチ、1 つの物理サーバーと 1 台の物理的なクライアントが必要です。

1. 1 つのイーサネット ハブまたはスイッチにイーサネット ケーブルを使って、物理コンピューターを接続することができます
2. このガイドを使用して DHCP サーバーとして構成する Windows Server 2106 を実行している 1 台の物理コンピューターです。 
3. DHCP サーバーに使用できることを確認する Windows クライアント オペレーティング システムを実行している 1 台の物理コンピューターが動的に割り当てる IP アドレスと DHCP オプション DHCP クライアントにします。


## <a name="bkmk_deploy"></a>DHCP を展開します。

ここでは、1 台のサーバーの DHCP の展開を使用できる Windows PowerShell コマンドの例を示します。 サーバーでこれらの例のコマンドを実行する前に、ネットワークと環境と一致するコマンドを変更する必要があります。 

たとえば、コマンドを実行する前に、次の項目のコマンドで値の例を置き換える必要があります。

- コンピューター名
- 各スコープ (サブネットごとに 1 のスコープ) を構成する場合の IP アドレスの範囲
- 各 IP アドレスの範囲を構成するサブネット マスク
- 各スコープに対してスコープ名
- 各スコープに対して除外範囲
- デフォルト ゲートウェイ、ドメイン名、および DNS または WINS サーバーなどの DHCP オプションの値
- インターフェイス名

>[!IMPORTANT]
>確認し、コマンドを実行する前に、環境内のすべてのコマンドを変更します。

### <a name="where-to-install-dhcp---on-a-physical-computer-or-a-vm"></a>物理コンピューターまたは VM 上の DHCP をインストールする場所ですか。

DHCP サーバーの役割をインストールするには、物理コンピューターまたは仮想マシン上 \(VM\) Hyper\ V ホストにインストールされています。 Hyper-V 仮想スイッチに VM の仮想ネットワーク アダプターを接続する必要があります、VM に DHCP をインストールするし、DHCP サーバーで Hyper-V ホストが接続されている物理ネットワーク上のコンピューターに IP アドレスの割り当てを提供する、**外部**します。

詳細については、セクションを参照して**Hyper-V マネージャーで仮想スイッチを作成**」トピックの「[仮想ネットワークを作成する](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/connect-to-network)します。

### <a name="run-windows-powershell-as-an-administrator"></a>Windows PowerShell を管理者として実行します。

次の手順を使用して、管理者特権で Windows PowerShell を実行することができます。

1. Windows Server 2016 を実行するコンピューター上] をクリックして**開始**、Windows PowerShell アイコンを右クリックします。 メニューが表示されます。 

2. メニューで、をクリックして**詳細**、] をクリックし、**管理者として実行**します。 メッセージが表示されたら、コンピューターで管理者権限を持つアカウントの資格情報を入力します。 管理者レベルのアカウントを使用するログオンしているコンピューターにユーザー アカウントには、資格情報プロンプトが受け取りません。

3. 管理者特権で Windows PowerShell を開きます。

### <a name="rename-the-dhcp-server-and-configure-a-static-ip-address"></a>DHCP サーバーの名前を変更して静的 IP アドレスを構成します。

されていない場合、次の Windows PowerShell コマンドを使用して、DHCP サーバーの名前を変更して、サーバーの静的 IP アドレスを構成することができます。

**静的 IP アドレスを構成します。**

DNS サーバーの正しい IP アドレスと DHCP サーバーの TCP/IP プロパティを構成して、DHCP サーバーに静的 IP アドレスを割り当てるには、次のコマンドを使用できます。 インターフェイス名と、この例では、IP アドレスは、またコンピューターを構成するために必要な値に置き換える必要があります。

 `New-NetIPAddress -IPAddress 10.0.0.3 -InterfaceAlias "Ethernet" -DefaultGateway 10.0.0.1 -AddressFamily IPv4 -PrefixLength 24`

 `Set-DnsClientServerAddress -InterfaceAlias "Ethernet" -ServerAddresses 10.0.0.2`

これらのコマンドの詳細については、次のトピックを参照してください。

- [New-NetIPAddress](https://technet.microsoft.com/itpro/powershell/windows/tcpip/new-netipaddress)
- [Set-DnsClientServerAddress](https://technet.microsoft.com/itpro/powershell/windows/dns-client/set-dnsclientserveraddress)

**コンピューターを名前します。**

次のコマンドを使用して、名前を変更し、コンピューターを再起動することができます。

`Rename-Computer -Name DHCP1`

 `Restart-Computer`

これらのコマンドの詳細については、次のトピックを参照してください。

- [Rename-Computer](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.management/rename-computer)
- [Restart-Computer](https://msdn.microsoft.com/powershell/reference/4.0/microsoft.powershell.management/restart-computer)

### <a name="join-the-computer-to-the-domain-optional"></a>コンピューターを参加させるドメイン \(Optional\)

Active Directory ドメイン環境で、DHCP サーバーをインストールする場合は、コンピューターをドメインに参加する必要があります。 管理者特権で Windows PowerShell を開き、ドメインの NetBios 名を交換した後、次のコマンドを実行**CORP**、環境に適した値にします。

    Add-Computer CORP

メッセージが表示されたら、コンピューターをドメインに参加させるアクセス許可を持つドメイン ユーザー アカウントの資格情報を入力します。 

    Restart-Computer

Add-Computer コマンドの詳細については、次のトピックを参照してください。

- [Add-Computer](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.management/add-computer)

### <a name="install-dhcp"></a>DHCP をインストールします。

コンピューターが再起動したら、管理者特権で Windows PowerShell を開くし、次のコマンドを実行して DHCP をインストールします。

    Install-WindowsFeature DHCP -IncludeManagementTools

このコマンドの詳細については、次のトピックを参照してください。

- [Install-windowsfeature](https://technet.microsoft.com/itpro/powershell/windows/server-manager/install-windowsfeature)

### <a name="create-dhcp-security-groups"></a>DHCP セキュリティ グループを作成します。

セキュリティ グループを作成するには、Windows PowerShell で、ネットワーク シェル \(netsh\) コマンドを実行し、新しいグループがアクティブになるように、DHCP サービスを再起動する必要があります。

DHCP サーバーで、次の netsh コマンドを実行すると、**DHCP Administrators**と**DHCP Users**でセキュリティ グループが作成**ローカル ユーザーとグループ**DHCP サーバーでします。

    netsh dhcp add securitygroups

次のコマンドは、ローカル コンピューター上の DHCP サービスを再起動します。

    Restart-service dhcpserver

これらのコマンドの詳細については、次のトピックを参照してください。

- [ネットワーク シェル (Netsh)](../netsh/netsh.md)
- [Restart-Service](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.management/restart-service)

### <a name="authorize-the-dhcp-server-in-active-directory-optional"></a>Active Directory \(Optional\) で DHCP サーバーを承認します。

ドメイン環境で DHCP をインストールする場合は、ドメインで動作する DHCP サーバーを承認するために次の手順を実行する必要があります。

>[!NOTE]
>Active Directory ドメインにインストールされている承認されていない DHCP サーバーは正常に機能できないし、DHCP クライアントに IP アドレスをリースしません。 未承認の DHCP サーバーがネットワーク上のクライアントに正しくない IP アドレスを割り当てることを防ぐセキュリティ機能は、未承認の DHCP サーバーの自動で無効にします。

DHCP サーバーを Active Directory で承認された DHCP サーバーの一覧に追加するのには、次のコマンドを使用できます。 

>[!NOTE]
>ドメイン環境を持っていない場合は、このコマンドは実行されません。

 `Add-DhcpServerInDC -DnsName DHCP1.corp.contoso.com -IPAddress 10.0.0.3`

DHCP サーバーが Active Directory で承認されていることを確認するには、次のコマンドを使用できます。

    Get-DhcpServerInDC

Windows PowerShell で表示される結果の例を次に示します。

    
        IPAddress   DnsName
        ---------   -------
        10.0.0.3    DHCP1.corp.contoso.com
    

これらのコマンドの詳細については、次のトピックを参照してください。

- [Add-DhcpServerInDC](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/add-dhcpserverindc)
- [Get-DhcpServerInDC](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/get-dhcpserverindc)

### <a name="notify-server-manager-that-post-install-dhcp-configuration-is-complete-optional"></a>サーバー マネージャー、post\ インストール DHCP の構成が完了 \(Optional\) を通知します。

セキュリティ グループを作成し、Active Directory で DHCP サーバーを承認するなど、post\ インストールのタスクを完了した後にサーバー マネージャーの DHCP ポスト インストールの構成ウィザードを使用して post\ インストールの手順を完了する必要があることを示すユーザー インターフェイスで、アラートが表示もします。

この now\ 不要かつ不正確なメッセージを防止この Windows PowerShell コマンドを使用して、次のレジストリ キーを構成することによって、サーバー マネージャーを表示できます。

    Set-ItemProperty –Path registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ServerManager\Roles\12 –Name ConfigurationState –Value 2

このコマンドの詳細については、次のトピックを参照してください。

- [Set-ItemProperty](https://msdn.microsoft.com/powershell/reference/4.0/microsoft.powershell.management/set-itemproperty?f=255&MSPPError=-2147217396)

### <a name="set-server-level-dns-dynamic-update-configuration-settings-optional"></a>サーバー レベル DNS 動的更新の構成設定 \(Optional\) を設定します。

DHCP サーバーが DHCP クライアント コンピューターの DNS 動的更新を実行する場合は、この設定を構成するには、次のコマンドを実行することができます。 これは、サーバー レベルを設定する、スコープ レベルを設定しない、サーバーで構成するすべてのスコープに影響するためです。 この例のコマンドは、クライアントが少なくともが経過すると、クライアントの DNS リソース レコードを削除する DHCP サーバーも構成します。

    Set-DhcpServerv4DnsSetting -ComputerName "DHCP1.corp.contoso.com" -DynamicUpdates "Always" -DeleteDnsRRonLeaseExpiry $True

次のコマンドを使用すると、DHCP サーバーを登録または DNS サーバー上のクライアント レコードを登録解除に使用する資格情報を構成します。 この例では、DHCP サーバーで、資格情報を保存します。 最初のコマンドを使用して**Get-credential**を作成する、**PSCredential**オブジェクト、および内のオブジェクトを格納し、**$Credential**変数です。 コマンドの入力を求めるユーザー名とパスワード、そのため、DNS サーバー上のリソース レコードを更新するアクセス許可を持つアカウントの資格情報を提供することを確認します。

    
    $Credential = Get-Credential
    Set-DhcpServerDnsCredential -Credential $Credential -ComputerName "DHCP1.corp.contoso.com"
    

これらのコマンドの詳細については、次のトピックを参照してください。

- [セット DhcpServerv4DnsSetting](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/set-dhcpserverv4dnssetting)
- [Set-DhcpServerDnsCredential](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/set-dhcpserverdnscredential)

### <a name="configure-the-corpnet-scope"></a>Corpnet スコープを構成します。

DHCP インストールが完了したら、次のコマンドを使用して構成と Corpnet スコープをアクティブ化、スコープの除外範囲を作成し、DHCP オプションのデフォルト ゲートウェイ、DNS サーバーの IP アドレス、および DNS ドメイン名を構成することができます。

    
    Add-DhcpServerv4Scope -name "Corpnet" -StartRange 10.0.0.1 -EndRange 10.0.0.254 -SubnetMask 255.255.255.0 -State Active`
    
    Add-DhcpServerv4ExclusionRange -ScopeID 10.0.0.0 -StartRange 10.0.0.1 -EndRange 10.0.0.15`
    
    Set-DhcpServerv4OptionValue -OptionID 3 -Value 10.0.0.1 -ScopeID 10.0.0.0 -ComputerName DHCP1.corp.contoso.com`
    
    Set-DhcpServerv4OptionValue -DnsDomain corp.contoso.com -DnsServer 10.0.0.2
    

これらのコマンドの詳細については、次のトピックを参照してください。

- [追加 DhcpServerv4Scope](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/add-dhcpserverv4scope)
- [追加 DhcpServerv4ExclusionRange](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/add-dhcpserverv4exclusionrange)
- [セット DhcpServerv4OptionValue](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/set-dhcpserverv4optionvalue)

### <a name="configure-the-corpnet2-scope-optional"></a>構成、Corpnet2 \(Optional\) のスコープ

DHCP 転送が有効になっているルーターを持つ、最初のサブネットに接続されている 2 番目のサブネットがある場合は、この例では Corpnet2 をという名前、2 つ目のスコープを追加する、次のコマンドを使用できます。 この例は、除外範囲および IP アドレス、デフォルト ゲートウェイにも設定 \ (、subnet\ のルーターの IP アドレス) Corpnet2 サブネットのします。

 `Add-DhcpServerv4Scope -name "Corpnet2" -StartRange 10.0.1.1 -EndRange 10.0.1.254 -SubnetMask 255.255.255.0 -State Active`

 `Add-DhcpServerv4ExclusionRange -ScopeID 10.0.1.0 -StartRange 10.0.1.1 -EndRange 10.0.1.15`

 `Set-DhcpServerv4OptionValue -OptionID 3 -Value 10.0.1.1 -ScopeID 10.0.1.0 -ComputerName DHCP1.corp.contoso.com`

この DHCP サーバーによって処理され、追加のサブネットがあれば、各サブネットのスコープを追加するコマンドのパラメーターのすべての異なる値を使用して、これらのコマンドを繰り返すことができます。

>[!IMPORTANT]
>DHCP クライアントと、DHCP サーバーの間のすべてのルーターが DHCP メッセージ転送用に構成されていることを確認します。 DHCP 転送を構成する方法の詳細については、ルーターのドキュメントを参照してください。

## <a name="bkmk_verify"></a>サーバー機能を確認します。

DHCP サーバーが DHCP クライアントに IP アドレスの動的割り当てを提供することを確認するには、修理されたサブネットに別のコンピューターを接続できます。 ネットワーク アダプターと、コンピューターの電源をオンにイーサネット ケーブルを接続した後は、IP アドレスを DHCP サーバーから要求します。 成功した構成を使用して確認することができます、**ipconfig/all**コマンドと、結果を確認する接続テストを実行することによってなどしようとしたり Windows エクスプ ローラーまたはその他のアプリケーションでブラウザーまたはファイル共有での Web リソースにアクセスします。

クライアントは、DHCP サーバーから IP アドレスを受信していない場合、は、次のトラブルシューティング手順を実行します。

1. 両方のコンピューターと、イーサネット スイッチ、ハブ、またはルーターにイーサネット ケーブルが接続されていることを確認します。
1. ルーターで DHCP サーバーから分離されたネットワーク セグメントにクライアント コンピューターを接続する場合は、DHCP メッセージを転送するルーターが構成されていることを確認します。
1. DHCP サーバーが Active Directory から承認された DHCP サーバーの一覧を取得するには、次のコマンドを実行して Active Directory で承認されていることを確認します。 [Get-dhcpserverindc](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/get-dhcpserverindc)します。
1. DHCP コンソールを開くことによって、スコープがアクティブ化されることを確認 \ (サーバー マネージャー、**ツール**、**DHCP**\)、各スコープのスコープ、し、右クリックを確認するサーバー ツリーを展開します。 表示されるメニューには、選択範囲が含まれている場合**Activate**、] をクリックして**Activate**します。 \ (メニューの選択内容を読み取り、スコープが既にライセンス認証されている場合**Deactivate**. \) 

## <a name="bkmk_dhcpwps"></a>DHCP 用 Windows PowerShell コマンド

次の参照はコマンドの説明と構文を Windows Server 2016 のすべての DHCP サーバーの Windows PowerShell コマンドを提供します。 トピックなど、コマンドの先頭の動詞に基づいてアルファベット順にコマンドの一覧**取得**または**設定**します。

>[!NOTE]
>Windows Server 2012 R2 では、Windows Server 2016 のコマンドを使用できません。

- [DhcpServer モジュール](https://technet.microsoft.com/itpro/powershell/windows/dhcp-server/index)

次の参照はコマンドの説明と構文を Windows Server 2012 R2 のすべての DHCP サーバーの Windows PowerShell コマンドを提供します。 トピックなど、コマンドの先頭の動詞に基づいてアルファベット順にコマンドの一覧**取得**または**設定**します。

>[!NOTE]
>Windows Server 2016 では、Windows Server 2012 R2 のコマンドを使用できます。

- [Windows PowerShell の DHCP サーバー コマンドレット](https://technet.microsoft.com/library/jj590751.aspx)

## <a name="bkmk_list"></a>このガイドで Windows PowerShell コマンドの一覧

コマンドと、このガイドで使用される値の例の単純な一覧を次に示します。

    
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
    


