---
title: ネットワーク アダプターのパフォーマンスを調整する
description: このトピックは、Windows Server 2016 のネットワークサブシステムのパフォーマンスチューニングガイドに含まれています。
audience: Admin
ms.custom:
- CI ID 111485
- CSSTroubleshoot
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 0b9b0f80-415c-4f5e-8377-c09b51d9c5dd
manager: dcscontentpm
ms.author: lizross
author: Teresa-Motiv
ms.date: 12/23/2019
ms.openlocfilehash: f802804d64b3047a2612b7f346de03aff61c30cd
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80316542"
---
# <a name="performance-tuning-network-adapters"></a>ネットワーク アダプターのパフォーマンスを調整する

> 適用対象: Windows Server 2019、Windows Server 2016、Windows Server (半期チャネル)

このトピックでは、Windows Server 2016 以降のバージョンを実行しているコンピューターのパフォーマンスネットワークアダプターを調整する方法について説明します。 ネットワークアダプターにチューニングオプションが用意されている場合は、これらのオプションを使用して、ネットワークのスループットとリソースの使用率を最適化できます。

ネットワークアダプターの正しいチューニング設定は、次の変数によって異なります。

- ネットワーク アダプターとその機能セット  
- サーバーが実行するワークロードの種類  
- サーバーのハードウェアとソフトウェアのリソース  
- サーバーのパフォーマンス目標  

以下のセクションでは、パフォーマンス チューニング オプションの一部について説明します。  

##  <a name="enabling-offload-features"></a><a name="bkmk_offload"></a>オフロード機能の有効化

ネットワーク アダプターのオフロード機能の調整には、一般的にメリットがあります。 ただし、ネットワークアダプターは、高スループットでオフロード機能を処理するのに十分ではない可能性があります。

> [!IMPORTANT]
> オフロード機能の**IPsec タスクオフ**ロードまたは**TCP chimney オフロード**を使用しないでください。 これらのテクノロジは Windows Server 2016 で非推奨とされており、サーバーとネットワークのパフォーマンスに悪影響を及ぼす可能性があります。 さらに、これらのテクノロジはマイクロソフトによって今後サポートされない可能性があります。

たとえば、ハードウェアリソースが限られているネットワークアダプターを考えてみます。
この場合、セグメント化オフロード機能を有効にすると、アダプターの維持可能な最大スループットが低下する可能性があります。 ただし、スループットの低下が許容できる場合は、セグメント化オフロード機能を有効にすることをお勧めします。

> [!NOTE]  
> 一部のネットワークアダプターでは、送信パスと受信パスに対して個別にオフロード機能を有効にする必要があります。

##  <a name="enabling-receive-side-scaling-rss-for-web-servers"></a><a name="bkmk_rss_web"></a>Web サーバーの receive side scaling (RSS) の有効化

サーバーの論理プロセッサよりもネットワーク アダプター数が少ない場合、RSS で Web のスケーラビリティとパフォーマンスを改善できます。 すべての web トラフィックが RSS 対応のネットワークアダプターを経由する場合、サーバーは異なる Cpu 間で同時に異なる接続からの受信 web 要求を処理できます。

> [!IMPORTANT]  
> 同じサーバー上で、RSS 以外のネットワークアダプターと RSS 対応のネットワークアダプターの両方を使用することは避けてください。 Rss とハイパーテキスト転送プロトコル (HTTP) の負荷分散ロジックにより、rss 非対応のネットワークアダプターが1つ以上の RSS 対応ネットワークアダプターを持つサーバーで web トラフィックを受け入れる場合、パフォーマンスが著しく低下する可能性があります。 このような場合、RSS 対応ネットワーク アダプターを使用するか、ネットワーク アダプターのプロパティの **[詳細プロパティ]** タブで RSS を無効にすることをお勧めします。
>  
> ネットワーク アダプターが RSS 対応かどうかを判断するには、ネットワーク アダプターのプロパティの **[詳細プロパティ]** タブの RSS 情報を確認します。

### <a name="rss-profiles-and-rss-queues"></a>RSS プロファイルと RSS キュー

既定の RSS 定義済みプロファイルは**Numastatic**です。これは、以前のバージョンの Windows で使用されていた既定とは異なります。 RSS プロファイルの使用を開始する前に、利用可能なプロファイルを確認して、どのような利点があるか、およびネットワーク環境とハードウェアにどのように適用されるかを理解してください。

たとえば、タスクマネージャーを開き、サーバー上の論理プロセッサを確認し、受信トラフィックに使用率が低いと思われる場合は、RSS キューの数を既定の2からネットワークアダプターでサポートされている最大の数に増やすことができます。 ネットワーク アダプターによっては、ドライバーの一部として RSS キュー数を変更するオプションがあります。

##  <a name="increasing-network-adapter-resources"></a><a name="bkmk_resources"></a>ネットワークアダプターのリソースを増やす

受信バッファーや送信バッファーなどのリソースを手動で構成できるネットワークアダプターの場合は、割り当てられたリソースを増やす必要があります。  

ネットワーク アダプターによっては、受信バッファーを低く設定して、ホストから割り当てられるメモリを節約している場合があります。 値を低くすると、パケットが損失し、パフォーマンスが低下します。 そのため、受信量が多いシナリオの場合、受信バッファー値を最大値まで増やすことをお勧めします。

> [!NOTE]  
> ネットワークアダプターがリソースの手動構成を公開しない場合、リソースが動的に構成されるか、リソースが変更できない固定値に設定されます。

### <a name="enabling-interrupt-moderation"></a>割り込みモデレーションの有効化

割り込みモデレーションを制御するために、一部のネットワークアダプターでは、さまざまな割り込みモデレーションレベル、異なるバッファー合体パラメーター (送信バッファーと受信バッファーの場合は別々)、またはその両方が公開されます。

CPU にバインドされたワークロードでは、割り込みのモデレーションを考慮する必要があります。 割り込みモデレーションを使用する場合は、割り込みと待機時間の短縮により、ホストの CPU 節約率と待機時間の間のトレードオフについて検討します。 ネットワークアダプターが割り込みのモデレーションを実行しないが、バッファーの合体を公開している場合は、結合されたバッファーの数を増やして、送信または受信ごとにより多くのバッファーを許可することで、パフォーマンスを向上させることができます。

##  <a name="performance-tuning-for-low-latency-packet-processing"></a><a name="bkmk_low"></a>待機時間の短いパケット処理のパフォーマンスチューニング

多くのネットワーク アダプターには、オペレーティング システムが原因の待機時間を最適化するオプションがあります。 待機時間は、ネットワーク ドライバーが着信パケットを処理してから、ネットワーク ドライバーがパケットを返送するまでの経過時間です。 通常、この時間はマイクロ秒単位で測定されます。 比較のために、通常、長距離間のパケット送信の送信時間は、ミリ秒単位 (1 桁大きい単位) で測定されます。 この調整によって、パケットの送信にかかる時間は短縮されません。

次に、精度がマイクロ秒のネットワークのパフォーマンス チューニングをいくつか提案します。

- コンピューターの BIOS を、C 状態を無効にして **High Performance (高パフォーマンス)** に設定します。 この設定はシステムと BIOS によって変わる点に注意してください。一部のシステムは、オペレーティング システムが電源管理を制御している場合に、パフォーマンスが高くなります。 電源管理設定の確認と調整は、**設定**から行うことも、 **powercfg**コマンドを使用して行うこともできます。 詳細については、「 [Powercfg のコマンドラインオプション](https://docs.microsoft.com/windows-hardware/design/device-experiences/powercfg-command-line-options)」を参照してください。

- オペレーティング システムの電源管理プロファイルを **高パフォーマンス** システムに設定します。  
   > [!NOTE]  
   > システム BIOS が電源管理のオペレーティングシステム制御を無効にするように設定されている場合、この設定は正しく機能しません。

- 静的オフロードを有効にします。 たとえば、UDP チェックサム、TCP チェックサム、および Send Large Offload (LSO) 設定を有効にします。

- 大量のマルチキャストトラフィックを受信するときなど、トラフィックがマルチストリームになっている場合は、RSS を有効にします。

- 待機時間をできるだけ短くする必要があるネットワーク カード ドライバーの場合、**Interrupt Moderation (割り込み節度)** を無効にします。 この構成は、より多くの CPU 時間を使用し、トレードオフを表す可能性があることに注意してください。

- パケットを処理するプログラム (ユーザー スレッド) に使用されているコアと CPU キャッシュを共有しているコア プロセッサで、ネットワーク アダプターの割り込みと DPC を処理します。 CPU アフィニティの調整を使用してプロセスを特定の論理プロセッサに誘導し、RSS の構成と組み合わせて、この処理を実行することができます。 割り込み、DPC、ユーザー モード スレッドに同じコアを使用すると、コアの使用に関する ISR、DPC、およびスレッドが競合することで負荷が増えるため、パフォーマンスが低下します。

##  <a name="system-management-interrupts"></a><a name="bkmk_smi"></a>システム管理の割り込み

多くのハードウェアシステムでは、エラー修正コード (ECC) メモリエラーの報告、レガシ USB 互換性の維持、ファンの制御、BIOS 制御電源の管理など、さまざまなメンテナンス機能にシステム管理割り込み (SMI-S) を使用しています。設定。

SMI-S はシステムの最高優先度の割り込みで、CPU を管理モードにします。 このモードでは、SMI-S は通常 BIOS に含まれる割り込みサービスルーチンを実行している間、他のすべてのアクティビティをプリエンプションします。

残念ながら、この動作によって100マイクロ秒以上の待機時間が急増する可能性があります。

待機時間を最小限にする必要がある場合は、SMI を可能な限り低く抑えることができる BIOS バージョンをハードウェア プロバイダーに問い合わせることをお勧めします。 これらの BIOS バージョンは、"低待機時間 BIOS" または "SMI-S 無償 BIOS" と呼ばれることがよくあります。 場合によっては、SMI アクティビティが重要な機能 (冷却ファンなど) の制御に使用されているため、ハードウェア プラットフォームで SMI アクティビティを排除できない可能性があります。

> [!NOTE]  
> オペレーティングシステムは、論理プロセッサが特別なメンテナンスモードで実行されているため、SMIs を制御できません。これにより、オペレーティングシステムの介入ができなくなります。

##  <a name="performance-tuning-tcp"></a><a name="bkmk_tcp"></a>TCP のパフォーマンスチューニング

 次の項目を使用して、TCP のパフォーマンスを調整できます。

###  <a name="tcp-receive-window-autotuning"></a><a name="bkmk_tcp_params"></a>TCP 受信ウィンドウの自動チューニング

Windows Vista、Windows Server 2008、およびそれ以降のバージョンの Windows では、Windows ネットワークスタックは、tcp 受信ウィンドウの自動*チューニングレベル*という機能を使用して、tcp 受信ウィンドウサイズをネゴシエートします。 この機能は、tcp ハンドシェイク中に TCP 通信ごとに定義された受信ウィンドウサイズをネゴシエートできます。

以前のバージョンの Windows では、Windows ネットワークスタックは固定サイズの受信ウィンドウ (65535 バイト) を使用しています。これにより、接続の総スループットが制限されていました。 TCP 接続の達成可能なスループットの合計によって、ネットワークの使用シナリオが制限される可能性があります。 TCP 受信ウィンドウ自動調整では、これらのシナリオでネットワークを完全に使用できます。

特定のサイズの TCP 受信ウィンドウの場合、次の式を使用して、1つの接続の合計スループットを計算できます。

> *達成可能スループットの合計 (バイト*単位) = *TCP 受信ウィンドウサイズ (バイト*単位) \* (1/*接続の待機時間 (秒*))

たとえば、待機時間が10ミリ秒の接続の場合、達成可能なスループットの合計は 51 Mbps です。 この値は、大規模な企業ネットワークインフラストラクチャには適しています。 ただし、自動チューニングを使用して受信ウィンドウを調整することで、接続は 1 Gbps の接続の完全な回線速度を実現できます。  

一部のアプリケーションでは、TCP 受信ウィンドウのサイズを定義します。 アプリケーションで受信ウィンドウサイズが定義されていない場合、リンク速度は次のようにサイズを決定します。

- 1メガビット/秒 (Mbps) 以下: 8 キロバイト (KB)
- 1 mbps ~ 100 Mbps:17 KB
- 100 Mbps ~ 10 ギガビット/秒 (Gbps):64 KB
- 10 Gbps 以上: 128 KB

たとえば、1 Gbps のネットワークアダプターがインストールされているコンピューターでは、ウィンドウのサイズは 64 KB にする必要があります。

また、この機能では、ネットワークのパフォーマンスを向上させるために、他の機能もすべて使用できます。 これらの機能には、 [RFC 1323](https://tools.ietf.org/html/rfc1323)で定義されている残りの TCP オプションが含まれます。 これらの機能を使用することにより、Windows ベースのコンピューターでは、サイズの小さい TCP 受信ウィンドウサイズをネゴシエートできますが、構成によっては定義された値でスケーリングされます。 この動作により、ネットワークデバイスのサイズがより簡単に処理できるようになります。

> [!NOTE]  
> [RFC 1323](https://tools.ietf.org/html/rfc1323)で定義されているように、ネットワークデバイスが**TCP ウィンドウスケールオプション**に準拠していないという問題が発生する可能性があります。そのため、はスケールファクターをサポートしていません。 このような場合は、この KB 934430 を参照してください。[ファイアウォールデバイスの背後で Windows Vista を使用しようとすると、ネットワーク接続が失敗](https://support.microsoft.com/help/934430/network-connectivity-fails-when-you-try-to-use-windows-vista-behind-a)します。または、ネットワークデバイスベンダーのサポートチームに問い合わせてください。  

#### <a name="review-and-configure-tcp-receive-window-autotuning-level"></a>TCP 受信ウィンドウの自動チューニングレベルを確認して構成する

Netsh コマンドまたは Windows PowerShell コマンドレットを使用して、TCP 受信ウィンドウの自動チューニングレベルを確認または変更できます。

> [!NOTE]  
> Windows 10 または Windows Server 2019 より前のバージョンの Windows では、レジストリを使用して TCP 受信ウィンドウサイズを構成することはできません。 非推奨の設定の詳細については、「[非推奨の TCP パラメーター](#deprecated-tcp-parameters)」を参照してください。

> [!NOTE]  
> 使用可能な自動チューニングレベルの詳細については、「自動[チューニングレベル](#autotuning-levels)」を参照してください。

**Netsh を使用して自動チューニングレベルを確認または変更するには**

現在の設定を確認するには、コマンドプロンプトウィンドウを開き、次のコマンドを実行します。

```cmd
netsh interface tcp show global
```

このコマンドの出力は次のようになります。

```
Querying active state...

TCP Global Parameters  
-----
Receive-Side Scaling State : enabled
Chimney Offload State : disabled
Receive Window Auto-Tuning Level : normal
Add-On Congestion Control Provider : default
ECN Capability : disabled
RFC 1323 Timestamps : disabled
Initial RTO : 3000
Receive Segment Coalescing State : enabled
Non Sack Rtt Resiliency : disabled
Max SYN Retransmissions : 2
Fast Open : enabled
Fast Open Fallback : enabled
Pacing Profile : off
```

この設定を変更するには、コマンドプロンプトで次のコマンドを実行します。

```cmd
netsh interface tcp set global autotuninglevel=<Value>
```

> [!NOTE]  
> 上記のコマンドでは、\<*値*> が自動チューニングレベルの新しい値を表します。

このコマンドの詳細については、「[インターフェイス伝送制御プロトコル用の Netsh コマンド](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731258(v=ws.10))」を参照してください。

**Powershell を使用して自動チューニングレベルを確認または変更するには**

現在の設定を確認するには、PowerShell ウィンドウを開き、次のコマンドレットを実行します。

```PowerShell
Get-NetTCPSetting | Select SettingName,AutoTuningLevelLocal
```

このコマンドレットの出力は、次のようになります。

```
SettingName           AutoTuningLevelLocal
-----------          --------------------
Automatic
InternetCustom       Normal
DatacenterCustom     Normal
Compat               Normal
Datacenter           Normal
Internet             Normal
```

設定を変更するには、PowerShell コマンドプロンプトで次のコマンドレットを実行します。

```PowerShell
Set-NetTCPSetting -AutoTuningLevelLocal <Value>
```

> [!NOTE]  
> 上記のコマンドでは、\<*値*> が自動チューニングレベルの新しい値を表します。

これらのコマンドレットの詳細については、次の記事を参照してください。

- [NetTCPSetting](https://docs.microsoft.com/powershell/module/nettcpip/get-nettcpsetting?view=win10-ps)
- [NetTCPSetting](https://docs.microsoft.com/powershell/module/nettcpip/set-nettcpsetting?view=win10-ps)

#### <a name="autotuning-levels"></a>自動チューニングレベル

受信ウィンドウの自動チューニングは、5つのレベルのいずれかに設定できます。 既定のレベルは**Normal**です。 次の表では、これらのレベルについて説明します。

|Level |16 進数値 |コメント |
| --- | --- | --- |
|[標準] (既定) |0x8 (スケールファクターは 8) |ほとんどすべてのシナリオに対応できるように、TCP 受信ウィンドウを拡張するように設定します。 |
|無効 |使用できるスケールファクターがありません |TCP 受信ウィンドウを既定値で設定します。 |
|Restricted (制限する) |0x4 (スケールファクター 4) |TCP 受信ウィンドウを既定値を超えて拡張するように設定しますが、一部のシナリオではこのような増加を制限します。 |
|高制限 |0x2 (スケールファクター 2) |TCP 受信ウィンドウを既定値を超えて拡張するように設定しますが、非常に控えめです。 |
|実験用 |0xE (スケールファクター 14) |極端なシナリオに対応できるように、TCP 受信ウィンドウを拡張するように設定します。 |

アプリケーションを使用してネットワークパケットをキャプチャする場合、アプリケーションは、ウィンドウの自動チューニングレベルの設定に応じて、次のようなデータを報告する必要があります。

- 自動チューニングレベル:**標準 (既定の状態)**

   ```
   Frame: Number = 492, Captured Frame Length = 66, MediaType = ETHERNET
   + Ethernet: Etype = Internet IP (IPv4),DestinationAddress:[D8-FE-E3-65-F3-FD],SourceAddress:[C8-5B-76-7D-FA-7F]
   + Ipv4: Src = 192.169.0.5, Dest = 192.169.0.4, Next Protocol = TCP, Packet ID = 2667, Total IP Length = 52
   - Tcp: [Bad CheckSum]Flags=......S., SrcPort=60975, DstPort=Microsoft-DS(445), PayloadLen=0, Seq=4075590425, Ack=0, Win=64240 ( Negotiating scale factor 0x8 ) = 64240
   SrcPort: 60975
   DstPort: Microsoft-DS(445)
   SequenceNumber: 4075590425 (0xF2EC9319)
   AcknowledgementNumber: 0 (0x0)
   + DataOffset: 128 (0x80)
   + Flags: ......S. ---------------------------------------------------------> SYN Flag set
   Window: 64240 ( Negotiating scale factor 0x8 ) = 64240 ---------> TCP Receive Window set as 64K as per NIC Link bitrate. Note it shows the 0x8 Scale Factor.
   Checksum: 0x8182, Bad
   UrgentPointer: 0 (0x0)
   - TCPOptions:
   + MaxSegmentSize: 1
   + NoOption:
   + WindowsScaleFactor: ShiftCount: 8 -----------------------------> Scale factor, defined by AutoTuningLevel
   + NoOption:
   + NoOption:
   + SACKPermitted:
   ```

- 自動チューニングレベル:**無効**

   ```
   Frame: Number = 353, Captured Frame Length = 62, MediaType = ETHERNET
   + Ethernet: Etype = Internet IP (IPv4),DestinationAddress:[D8-FE-E3-65-F3-FD],SourceAddress:[C8-5B-76-7D-FA-7F]
   + Ipv4: Src = 192.169.0.5, Dest = 192.169.0.4, Next Protocol = TCP, Packet ID = 2576, Total IP Length = 48
   - Tcp: [Bad CheckSum]Flags=......S., SrcPort=60956, DstPort=Microsoft-DS(445), PayloadLen=0, Seq=2315885330, Ack=0, Win=64240 ( ) = 64240
   SrcPort: 60956
   DstPort: Microsoft-DS(445)
   SequenceNumber: 2315885330 (0x8A099B12)
   AcknowledgementNumber: 0 (0x0)
   + DataOffset: 112 (0x70)
   + Flags: ......S. ---------------------------------------------------------> SYN Flag set
   Window: 64240 ( ) = 64240 ----------------------------------------> TCP Receive Window set as 64K as per NIC Link bitrate. Note there is no Scale Factor defined. In this case, Scale factor is not being sent as a TCP Option, so it will not be used by Windows.
   Checksum: 0x817E, Bad
   UrgentPointer: 0 (0x0)
   - TCPOptions:
   + MaxSegmentSize: 1
   + NoOption:
   + NoOption:
   + SACKPermitted:
   ```

- 自動チューニングレベル:**制限付き**

   ```
   Frame: Number = 3, Captured Frame Length = 66, MediaType = ETHERNET
   + Ethernet: Etype = Internet IP (IPv4),DestinationAddress:[D8-FE-E3-65-F3-FD],SourceAddress:[C8-5B-76-7D-FA-7F]
   + Ipv4: Src = 192.169.0.5, Dest = 192.169.0.4, Next Protocol = TCP, Packet ID = 2319, Total IP Length = 52
   - Tcp: [Bad CheckSum]Flags=......S., SrcPort=60890, DstPort=Microsoft-DS(445), PayloadLen=0, Seq=1966088568, Ack=0, Win=64240 ( Negotiating scale factor 0x4 ) = 64240
   SrcPort: 60890
   DstPort: Microsoft-DS(445)
   SequenceNumber: 1966088568 (0x75302178)
   AcknowledgementNumber: 0 (0x0)
   + DataOffset: 128 (0x80)
   + Flags: ......S. ---------------------------------------------------------> SYN Flag set
   Window: 64240 ( Negotiating scale factor 0x4 ) = 64240 ---------> TCP Receive Window set as 64K as per NIC Link bitrate. Note it shows the 0x4 Scale Factor.
   Checksum: 0x8182, Bad
   UrgentPointer: 0 (0x0)
   - TCPOptions:
   + MaxSegmentSize: 1
   + NoOption:
   + WindowsScaleFactor: ShiftCount: 4 -------------------------------> Scale factor, defined by AutoTuningLevel.
   + NoOption:
   + NoOption:
   + SACKPermitted:
   ```

- 自動チューニングレベル:**高い制限**

   ```
   Frame: Number = 115, Captured Frame Length = 66, MediaType = ETHERNET
   + Ethernet: Etype = Internet IP (IPv4),DestinationAddress:[D8-FE-E3-65-F3-FD],SourceAddress:[C8-5B-76-7D-FA-7F]
   + Ipv4: Src = 192.169.0.5, Dest = 192.169.0.4, Next Protocol = TCP, Packet ID = 2388, Total IP Length = 52
   - Tcp: [Bad CheckSum]Flags=......S., SrcPort=60903, DstPort=Microsoft-DS(445), PayloadLen=0, Seq=1463725706, Ack=0, Win=64240 ( Negotiating scale factor 0x2 ) = 64240
   SrcPort: 60903
   DstPort: Microsoft-DS(445)
   SequenceNumber: 1463725706 (0x573EAE8A)
   AcknowledgementNumber: 0 (0x0)
   + DataOffset: 128 (0x80)
   + Flags: ......S. ---------------------------------------------------------> SYN Flag set
   Window: 64240 ( Negotiating scale factor 0x2 ) = 64240 ---------> TCP Receive Window set as 64K as per NIC Link bitrate. Note it shows the 0x2 Scale Factor.
   Checksum: 0x8182, Bad
   UrgentPointer: 0 (0x0)
   - TCPOptions:
   + MaxSegmentSize: 1
   + NoOption:
   + WindowsScaleFactor: ShiftCount: 2 ------------------------------> Scale factor, defined by AutoTuningLevel
   + NoOption:
   + NoOption:
   + SACKPermitted:
   ```

- 自動チューニングレベル:**試験段階**

   ```
   Frame: Number = 238, Captured Frame Length = 66, MediaType = ETHERNET
   + Ethernet: Etype = Internet IP (IPv4),DestinationAddress:[D8-FE-E3-65-F3-FD],SourceAddress:[C8-5B-76-7D-FA-7F]
   + Ipv4: Src = 192.169.0.5, Dest = 192.169.0.4, Next Protocol = TCP, Packet ID = 2490, Total IP Length = 52
   - Tcp: [Bad CheckSum]Flags=......S., SrcPort=60933, DstPort=Microsoft-DS(445), PayloadLen=0, Seq=2095111365, Ack=0, Win=64240 ( Negotiating scale factor 0xe ) = 64240
   SrcPort: 60933
   DstPort: Microsoft-DS(445)
   SequenceNumber: 2095111365 (0x7CE0DCC5)
   AcknowledgementNumber: 0 (0x0)
   + DataOffset: 128 (0x80)
   + Flags: ......S. ---------------------------------------------------------> SYN Flag set
   Window: 64240 ( Negotiating scale factor 0xe ) = 64240 ---------> TCP Receive Window set as 64K as per NIC Link bitrate. Note it shows the 0xe Scale Factor.
   Checksum: 0x8182, Bad
   UrgentPointer: 0 (0x0)
   - TCPOptions:
   + MaxSegmentSize: 1
   + NoOption:
   + WindowsScaleFactor: ShiftCount: 14 -----------------------------> Scale factor, defined by AutoTuningLevel
   + NoOption:
   + NoOption:
   + SACKPermitted:
   ```

#### <a name="deprecated-tcp-parameters"></a>非推奨の TCP パラメーター

Windows Server 2003 の次のレジストリ設定はサポートされなくなり、以降のバージョンでは無視されます。

- **TcpWindowSize**
- **NumTcbTablePartitions**  
- **MaxHashTableSize**  

これらの設定はすべて、次のレジストリサブキーにありました。

> **HKEY_LOCAL_MACHINE \System\CurrentControlSet\Services\Tcpip\Parameters**  

###  <a name="windows-filtering-platform"></a><a name="bkmk_wfp"></a>Windows フィルタリングプラットフォーム

Windows Vista および Windows Server 2008 では、Windows Filtering Platform (WFP) が導入されました。 WFP は、Microsoft 以外の独立系ソフトウェアベンダー (Isv) に Api を提供して、パケット処理フィルターを作成します。 たとえば、ファイアウォールとウイルス対策ソフトウェアが含まれています。

> [!NOTE]  
> 正しく記述されていない WFP フィルターを使用すると、サーバーのネットワークパフォーマンスが大幅に低下する可能性があります。 詳細については、Windows デベロッパーセンターの「[パケット処理ドライバーとアプリを WFP に移植する](https://docs.microsoft.com/windows-hardware/drivers/network/porting-packet-processing-drivers-and-apps-to-wfp)」を参照してください。

このガイドのすべてのトピックへのリンクについては、「[ネットワークサブシステムのパフォーマンスチューニング](net-sub-performance-top.md)」を参照してください。
