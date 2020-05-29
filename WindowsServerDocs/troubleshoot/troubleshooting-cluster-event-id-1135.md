---
title: イベント ID 1135 のクラスターの問題のトラブルシューティング
description: イベント ID 1135 のクラスターサービスの起動に関する問題をトラブルシューティングする方法について説明します。
ms.date: 05/28/2020
ms.openlocfilehash: 73357cc5b696a969de82123d3ca2a6fbb36fdc40
ms.sourcegitcommit: ef089864980a1d4793a35cbf4cbdd02ce1962054
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2020
ms.locfileid: "84150460"
---
# <a name="troubleshooting-cluster-issue-with-event-id-1135"></a>イベント ID 1135 のクラスターの問題のトラブルシューティング

この記事は、フェールオーバークラスタリング環境でクラスターサービスの開始時にログに記録される可能性があるイベント ID 1135 を診断および解決するのに役立ちます。

この記事では、

## <a name="start-page"></a>スタート ページ

イベント ID 1135 は、アクティブなフェールオーバークラスターのメンバーシップから1つ以上のクラスターノードが削除されたことを示します。 次のような現象が発生する可能性があります。

- クラスター Failover\ ノードがアクティブなフェールオーバークラスターのメンバーシップから削除されています:[アクティブなフェールオーバークラスターのメンバーシップからノードが削除されているときに問題が発生しました](/problem-nodes-failover-cluster.md)
- イベント ID 1069[イベント id 1069-クラスター化されたサービスまたはアプリケーションの可用性](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc756225(v=ws.10))
- クォーラム損失イベント ID 1177 のイベント ID 1177 [-クォーラムに必要なクォーラムと接続](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc773498(v=ws.10))
- クラスターサービスが停止したイベント ID 1006:[イベント id 1006-クラスターサービスのスタートアップ](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc773418(v=ws.10))

検証とネットワークテストは、問題の原因になる可能性がある構成の問題がないことを確認するために、最初のトラブルシューティングの手順の1つとして推奨されます。

### <a name="check-if-installed-the-recommended-hot-fixes"></a>推奨される修正プログラムがインストールされているかどうかを確認する

クラスターサービスは、フェールオーバークラスターの操作のすべての側面を制御し、クラスター構成データベースを管理する必須のソフトウェアコンポーネントです。 イベント ID 1135 が表示された場合は、以下のサポート技術情報の記事に記載されている修正プログラムをインストールし、クラスターのすべてのノードを再起動して、問題が再発したかどうかを確認することをお勧めします。

- [Windows Server 2012 R2 の修正プログラム](https://support.microsoft.com/help/2920151)
- [Windows Server 2012 用の修正プログラム](https://support.microsoft.com/help/2784261)
- [Windows Server 2008 R2 の修正プログラム](https://support.microsoft.com/help/2545685)

### <a name="check-if-the-cluster-service-running-on-all-the-nodes"></a>すべてのノードでクラスターサービスが実行されているかどうかを確認する

Windows オペレーティングシステムに従って次のコマンドを実行し、クラスターサービスが継続的に実行され、使用可能であることを確認します。

#### <a name="for-windows-server-2008-r2-cluster"></a>Windows Server 2008 R2 クラスターの場合

管理者特権でのコマンドプロンプトで **、cluster.exe ノード/stat**を実行します。  

#### <a name="for-windows-server-2012-and-windows-server-2012-r2-cluster"></a>Windows Server 2012 および Windows Server 2012 R2 クラスターの場合

PS コマンドの実行:**クラスターノード/status**  

クラスターサービスは継続的に実行され、すべてのノードで使用できますか。

## <a name="solution-for-cluster-service-is-failing"></a>クラスタサービスのソリューションが失敗しています

クラスターサービスで障害が発生した場合は、 [Windows Server 2008 と2008R2 のフェールオーバークラスターの起動スイッチ](/archive/blogs/askcore/windows-server-2008-and-2008r2-failover-cluster-startup-switches)に関する記事を使用してトラブルシューティングを行います。


## <a name="several-scenarios-of-event-id-1135"></a>イベント ID 1135 のいくつかのシナリオ

クラスターのすべてのノードで、システムイベントログを詳しく見てみましょう。 ノードに表示されているイベント ID 1135 を確認し、このイベントのすべてのインスタンスをコピーします。 これにより、それらを見て確認するのに便利です。

```console
Event ID 1135
Cluster node ' **NODE A** ' was removed from the active failover cluster membership. The Cluster service on this node may have stopped. This could also be due to the node having lost communication with other active nodes in the failover cluster. Run the Validate a Configuration wizard to check your network configuration. If the condition persists, check for hardware or software errors related to the network adapters on this node. Also check for failures in any other network components to which the node is connected such as hubs, switches, or bridges.
```

次の3つの一般的なシナリオがあります。

### <a name="scenario-a"></a>シナリオ A

すべてのイベントを確認しています。また、クラスター内のすべてのノードが、ノード A が通信を失ったことを示しています。

![シナリオ a ](media/troubleshooting-cluster-event-id-1135/18647.png)
 シナリオ a ![](media/troubleshooting-cluster-event-id-1135/18648.png)

ノード A にシステムログが表示されると、クラスター内の残りのすべてのノードに対するイベントが発生する可能性があります。

#### <a name="solution"></a>解決策

これにより、ネットワークの輻輳、またはノード A への通信が失われたことが原因で、問題が発生したことがわかります。

ネットワークの構成と通信に関する問題を確認し、検証する必要があります。 ノード A に関する問題を忘れないように注意してください。

### <a name="scenario-b"></a>シナリオ B

ノード上のイベントを確認し、クラスターが2つのサイトに分散しているとします。 サイト1とノード D のノード A、ノード B、およびノード C は、サイト2のノード E & ます。

![シナリオ B](media/troubleshooting-cluster-event-id-1135/18649.png)

ノード A、B、および C では、ログに記録されたイベントがノード D & E に接続されていることがわかります。同様に、ノード D & E でイベントが表示された場合、イベントは、A、B、および C との通信が失われたことを示唆します。

![シナリオ B](media/troubleshooting-cluster-event-id-1135/18650.png)

#### <a name="solution"></a>解決策

類似したアクティビティが表示される場合は、これらのサイトを接続するリンク経由で通信エラーが発生したことを示しています。 サイト間の接続を確認することをお勧めします。これが WAN 接続を経由している場合は、接続について ISP に確認することをお勧めします。

### <a name="scenario-c"></a>シナリオ C

ノードのイベントを見ると、ノードの名前が特定のパターンでカウントされていないことがわかります。 クラスターが2つのサイトに分散しているとします。 サイト1とノード D のノード A、ノード B、およびノード C は、サイト2でノード E & ます。

- ノード A: ノード B、D、E のイベントが表示されます。
- ノード B: ノード C、D、E のイベントが表示されます。
- ノード C: ノード A、B、E のイベントが表示されます。
- ノード D: ノード A、C、E のイベントが表示されます。
- ノード E: ノード B、C、D のイベントが表示されます。
- またはその他の組み合わせ。

![シナリオ C](media/troubleshooting-cluster-event-id-1135/18651.png)

#### <a name="solution"></a>解決策

このようなイベントは、ノード間のネットワークチャネルが開始されていて、クラスター通信メッセージが適時に到達していない場合に発生する可能性があります。これにより、ノード間の通信が失われ、クラスターのメンバーシップからノードが削除されます。

## <a name="review-cluster-networks"></a>クラスターネットワークを確認する

クラスターネットワークを確認する場合は、次の3つのオプションを1つずつ確認して、このトラブルシューティングガイドを続行することをお勧めします。

### <a name="check-for-antivirus-exclusion"></a>ウイルス対策の除外を確認する

クラスターサービスを実行しているサーバーで、次のファイルシステムの場所をウイルススキャンから除外します。

- ファイル共有監視のパス

- *フォルダーの場所*

ウイルス対策ソフトウェア内でリアルタイムスキャンコンポーネントを構成して、次のディレクトリとファイルを除外します。

- 既定の仮想マシン構成ディレクトリ (C:\ProgramData\Microsoft\Windows\Hyper-V)

- カスタム仮想マシンの構成ディレクトリ

- 既定のバーチャルハードディスクドライブディレクトリ (C:\Users\Public\Documents\Hyper-V\Virtual ハードディスク)

- カスタムバーチャルハードディスクドライブディレクトリ

- カスタムレプリケーションデータディレクトリ (Hyper-v レプリカを使用している場合)

- スナップショットディレクトリ

- mms

    > [!NOTE]
    > このファイルは、ウイルス対策ソフトウェア内のプロセスの除外として構成されている必要があります。)

- Vmwp .exe

    > [!NOTE]
    > このファイルは、ウイルス対策ソフトウェア内のプロセスの除外として構成されている必要があります。

さらに、クラスターの共有ボリュームと共にライブマイグレーションを使用する場合は、CSV パス*C:\ clusterstorage*とそのすべてのサブディレクトリを除外します。 クラスターサービスとウイルス対策ソフトウェアがインストールされている場合のフェールオーバーの問題または一般的な問題のトラブルシューティングを行う場合は、ウイルス対策ソフトウェアを一時的にアンインストールするか、ソフトウェアの製造元に確認して、ウイルス対策ソフトウェアがクラスターサービスで動作するかどうかを確認してください。 ほとんどの場合、ウイルス対策ソフトウェアを無効にするだけでは不十分です。 ウイルス対策ソフトウェアを無効にした場合でも、コンピューターを再起動するとフィルタードライバーは読み込まれたままになります。

### <a name="check-for-network-port-configuration-in-firewall"></a>ファイアウォールでネットワークポートの構成を確認する

クラスターサービスは、サーバークラスターの操作を制御し、クラスターデータベースを管理します。 クラスターは、1台のコンピューターとして機能する独立したコンピューターのコレクションです。 マネージャー、プログラマ、およびユーザーには、クラスターが単一のシステムとして表示されます。 ソフトウェアは、クラスターのノード間でデータを分散します。 ノードで障害が発生した場合、他のノードは、存在しないノードが以前に提供していたサービスとデータを提供します。 ノードが追加または修復されると、クラスターソフトウェアによって一部のデータがそのノードに移行されます。

システムサービス名: **ClusSvc**  

|アプリケーション|Protocol|Port|
|---|---|---|
|クラスターサービス|UDP|3343|
|クラスターサービス|TCP|3343 (ノードの結合操作中にこのポートが必要です。)|
|RPC|TCP|135|
|クラスター管理者|UDP|137|
|Kerberos|UDP\TCP|464 *|
|SMB|TCP|445|
|ランダムに割り当てられた高 UDP ポート * *|UDP|1024と65535の間のランダムなポート番号<br/>49152と65535の間のランダムなポート番号 * * *|
||||

> [!NOTE]
> さらに、Windows Server 2008 以降の Windows フェールオーバークラスターで検証を正常に実行するには、ICMP4、ICMP6 の受信トラフィックと送信トラフィックを許可します。

- 詳細については、「 [Windows Server 2012 フェールオーバークラスターの作成がエラー0xc000005e で失敗する](https://support.microsoft.com/help/2830510)」を参照してください。

- これらのポートをカスタマイズする方法の詳細については、「参照」セクションの「 [Windows のサービス概要およびネットワークポート要件](https://support.microsoft.com/help/832017/)」を参照してください。

これは、Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows 7、Windows Server 2008、および Windows Vista の範囲です。

さらに、次のコマンドを実行して、ファイアウォールのネットワークポート構成を確認します。 例: このコマンドは、フェールオーバークラスターで使用されるポート3343を特定するのに役立ちます。

```console
netsh advfirewall firewall show rule name="Failover Clusters (UDP-In)" verbose
```

### <a name="run-the-cluster-validation-report-for-any-errors-or-warnings"></a>クラスター検証レポートを実行してエラーまたは警告を確認する

クラスター検証ツールは、ハードウェアと設定がフェールオーバークラスタリングと互換性があることを確認するために、一連のテストを実行します。

次の手順に従ってください。

1. クラスター検証レポートを実行して、エラーまたは警告を確認します。 詳細については、「[クラスター検証テストについて: ネットワーク](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771323(v=ws.11)?redirectedfrom=MSDN)」を参照してください。

    ![subhatt1](media/troubleshooting-cluster-event-id-1135/18653.png)

2. ネットワークの警告とエラーを確認します。 詳細については、「[クラスター検証テストについて: ネットワーク](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771323(v=ws.11)?redirectedfrom=MSDN)」を参照してください。

    ![カテゴリネットワーク別の結果 ](media/troubleshooting-cluster-event-id-1135/18654.png) ![](media/troubleshooting-cluster-event-id-1135/18655.png)

#### <a name="check-the-list-network-binding-order"></a>ネットワークバインド順序の一覧を確認します。

このテストでは、ネットワークが各ノードのアダプターにバインドされる順序を示します。

[アダプターとバインド] タブには、接続がネットワークサービスによってアクセスされる順序で一覧表示されます。 これらの接続の順序は、一般的な TCP/IP 呼び出し/パケットがネットワークに送信される順序を反映しています。

ネットワークアダプターのバインド順序を変更するには、次の手順に従います。

1. [**スタート**]、[**実行**] の順にクリックし、「ncpa.cpl」」と入力して、[ **OK]** をクリックします。 [**ネットワーク接続**] ウィンドウの [ **LAN と高速インターネット**] セクションで、使用可能な接続を確認できます。

2. [**詳細**設定] メニューの [**詳細設定**] をクリックし、[**アダプターとバインド**] タブをクリックします。

3. [**接続**] 領域で、一覧内で上に移動する接続を選択します。 矢印ボタンを使用して、接続を移動します。 一般的なルールとして、ネットワークと通信するカード (ドメイン接続、他のネットワークへのルーティングなど) は、最初にバインドされたカード (一覧の先頭) にする必要があります。

クラスターノードはマルチホームシステムです。 ネットワークの優先順位は、送信ネットワーク接続の DNS クライアントに影響します。 クライアント通信に使用されるネットワークアダプターは、バインド順序の一番上にある必要があります。 ルーティングされていないネットワークは、優先順位の低いネットワークに配置できます。 Windows Server 2012 および Windows Server2012 R2 では、クラスターネットワークドライバー (NETFT.SYS) アダプタは、[バインド順] の一覧の下部に自動的に配置されます。

#### <a name="check-the-validate-network-communication"></a>ネットワーク通信の検証

ネットワークの待機時間によっても発生する可能性があります。 ノード間でパケットが失われることはありませんが、タイムアウト期間が経過する前にノードに到達できない可能性があります。

テスト対象サーバーがすべてのネットワーク上で許容範囲内の待ち時間で通信できることを検証します。

たとえば、[ネットワーク通信の検証] で、ネットワーク待機時間の問題について次のメッセージが表示される場合があります。

```console
Succeeded in pinging network interface node003.contoso.com IP Address 192.168.0.2 from network interface node004.contoso.com IP Address 192.168.0.3 with maximum delay 500 after 1 attempt(s).
Either address 10.0.0.96 is not reachable from 192.168.0.2 or **the ping latency is greater than the maximum allowed 2000 ms** This may be expected, since network interfaces node003.contoso.com - Heartbeat Network and node004.contoso.com - Production Network are on different cluster networks
Either address 192.168.0.2 is not reachable from 10.0.0.96 or **the ping latency is greater than the maximum allowed 2000 ms** This may be expected, since network interfaces node004.contoso.com - Production Network and node003.contoso.com - Heartbeat Network for MSCS are on different cluster networks
```

マルチサイトクラスターの場合は、タイムアウト値を増やすことができます。 詳細については、「[マルチサイトフェールオーバークラスターでハートビートと DNS 設定を構成する](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd197562(v=ws.10)?redirectedfrom=MSDN)」を参照してください。

WAN 接続の問題については、ISP に確認してください。

次のいずれかの問題が発生しているかどうかを確認します。

##### <a name="network-packets-lost-between-nodes"></a>ノード間でネットワークパケットが失われました

1. パフォーマンスを使用したパケット損失の確認

    パケットがノード間のネットワーク上で失われると、ハートビートは失敗します。 パフォーマンスモニターを使用して、"Network Interface\Packets Received が破棄されました" というカウンターを確認することで、この問題が発生しているかどうかを簡単に確認できます。 このカウンターを追加したら、平均値、最小値、および最大値を確認し、0より大きい値の場合は受信バッファーをアダプター用に調整する必要があります。

    ![カウンターの追加](media/troubleshooting-cluster-event-id-1135/18652.png)

    VmWare 仮想化プラットフォームでネットワークパケットが失われている場合は、「VmWare 仮想化プラットフォームにインストールされているクラスター」セクションを参照してください。

2. NIC ドライバーをアップグレードする

    この問題は、古い NIC drivers\Integration コンポーネント (IC)、vmtools、または NIC アダプターの不具合が原因で発生する可能性があります。
    物理マシン上のノード間でネットワークパケットが失われた場合は、ネットワークアダプターのドライバーを更新してください。 古いまたは古いネットワークカードドライバーやファームウェア。
    場合によっては、ネットワークカードやスイッチの構成の誤りが原因でハートビートが失われることもあります。

##### <a name="cluster-installed-in-the-vmware-virtualization-platform"></a>VmWare 仮想化プラットフォームにインストールされたクラスター

Vmware 環境の場合、VMware アダプターの問題を確認します。 

この問題は、トラフィックの増加中にパケットが破棄された場合に発生する可能性があります。 トラフィックのフィルター処理が行われていないことを確認します (たとえば、メールフィルターを使用します)。 この可能性を排除した後、ゲストオペレーティングシステムのバッファー数を徐々に増やして確認します。

バーストトラフィックの破棄を減らすには、次の手順を実行します。

1. Windows キー + R を使用して、[実行] ボックスを開きます。
2. 「Devmgmt.msc」と入力し、 **enter**キーを押します。
3. **ネットワークアダプター**の展開  
4. **Vmxnet3 を右クリックし、[プロパティ] をクリックします。**  
5. **[詳細設定]** タブをクリックします。
6. [**小さい Rx バッファー** ] をクリックし、値を大きくします。 既定値は512で、最大値は8192です。
7. [ **Rx リング #1**サイズ] をクリックし、値を大きくします。 既定値は1024で、最大値は4096です。

VMware 環境の場合は、次の Url を確認して、vmware アダプターの問題を確認します。

- [VMWARE ESX のフェールオーバークラスターメンバーシップから削除されているノード](/archive/blogs/askcore/nodes-being-removed-from-failover-cluster-membership-on-vmware-esx)。

- [ESXi の VMXNET3 vNIC のゲストオペレーティングシステムレベルでの大きなパケット損失](https://kb.vmware.com/s/article/2039495)

##### <a name="noticed-any-network-congestion"></a>ネットワークの輻輳に気付きます

ネットワークの混雑により、ネットワーク接続の問題が発生することもあります。

ネットワークが MS およびベンダーからの推奨事項として構成されていることを確認します。「 [Windows フェールオーバークラスターネットワークの構成](/archive/blogs/askcore/configuring-windows-failover-cluster-networks)」を参照してください。

##### <a name="check-the-network-configuration"></a>ネットワーク構成を確認します

それでもうまくいかない場合は、クラスター GUI でパーティション分割されたネットワークが表示されているか、ハートビート NIC で NIC チーミングが有効になっているかどうかを確認してください。

クラスター GUI にパーティション分割されたネットワークが表示される場合は、「パーティション分割された[クラスターネットワーク](/archive/blogs/askcore/partitioned-cluster-networks)」を参照して、問題のトラブルシューティングを行ってください。

ハートビート NIC で NIC チーミングが有効になっている場合は、チーミングベンダーの推奨事項に従って、チーミングソフトウェアの機能を確認します。

##### <a name="upgrade-the-nic-drivers"></a>NIC ドライバーをアップグレードする

この問題は、古い NIC ドライバーまたは NIC アダプターの不具合が原因で発生する可能性があります。

物理マシン上のノード間でネットワークパケットが失われた場合は、ネットワークアダプターのドライバーを更新してください。 古いまたは古いネットワークカードドライバーやファームウェア。

場合によっては、ネットワークカードやスイッチの構成の誤りが原因でハートビートが失われることもあります。

##### <a name="check-the-network-configuration"></a>ネットワーク構成を確認します

それでも問題が解決しない場合は、クラスター GUI でパーティション分割されたネットワークが表示されているか、ハートビート NIC で NIC チーミングが有効になっているかどうかを確認します。
