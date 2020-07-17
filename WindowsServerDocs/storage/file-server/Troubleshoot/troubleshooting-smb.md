---
title: 高度なトラブルシューティングサーバーメッセージブロック (SMB)
description: Advanced Server Message Block (SMB) のトラブルシューティング方法について説明します。
author: Deland-Han
manager: dcscontentpm
ms.topic: article
ms.author: delhan
ms.date: 12/25/2019
ms.openlocfilehash: 654cb1b0eea65457d521d201739721ed8c3c0203
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80815195"
---
# <a name="advanced-troubleshooting-server-message-block-smb"></a>高度なトラブルシューティングサーバーメッセージブロック (SMB)

サーバーメッセージブロック (SMB) は、クライアントがサーバー上のリソースにアクセスできるようにするための、ファイルシステム操作用のネットワークトランスポートプロトコルです。 SMB プロトコルの主な目的は、TCP/IP 経由で2つのシステム間でリモートファイルシステムアクセスを有効にすることです。

SMB のトラブルシューティングは非常に複雑になる可能性があります。 この記事は、完全なトラブルシューティングガイドではなく、SMB の効果的なトラブルシューティング方法の基本を理解するための簡単な入門資料です。

## <a name="tools-and-data-collection"></a>ツールとデータコレクション

品質の SMB トラブルシューティングの重要な側面の1つは、正しい用語を伝えることです。 この記事では、データの収集と分析の精度を確保するための基本的な SMB 用語について説明します。

> [!Note]
> *SMB サーバー (SRV)* は、ファイルシステムをホストしているシステム (ファイルサーバーとも呼ばれます) を指します。 *SMB クライアント (CLI)* は、OS のバージョンまたはエディションに関係なく、ファイルシステムにアクセスしようとしているシステムを指します。

たとえば、windows Server 2016 を使用して windows 10 でホストされている SMB 共有に接続する場合、Windows Server 2016 は smb クライアントと Windows 10 SMB サーバーになります。

### <a name="collect-data"></a>データの収集

SMB の問題のトラブルシューティングを行う前に、クライアント側とサーバー側の両方でネットワークトレースを最初に収集することをお勧めします。 次のガイドラインが適用されます。

- Windows システムでは、netshell (netsh)、ネットワークモニター、Message アナライザー、または Wireshark を使用してネットワークトレースを収集できます。

- 一般に、サードパーティ製のデバイスには、tcpdump (Linux/FreeBSD/Unix) や pktt (NetApp) などのインボックスパケットキャプチャツールがあります。 たとえば、SMB クライアントまたは SMB サーバーが Unix ホストである場合は、次のコマンドを実行してデータを収集できます。
  
  ```cmd
  # tcpdump -s0 -n -i any -w /tmp/$(hostname)-smbtrace.pcap
  ```
  
  キーボードの**Ctrl + C キー**を使用して、データ収集を停止します。

問題の原因を検出するには、CLI、SRV、またはその間のどこかで、両側のトレースを確認します。

#### <a name="using-netshell-to-collect-data"></a>Netshell を使用したデータの収集

このセクションでは、netshell を使用してネットワークトレースを収集する手順について説明します。

> [!NOTE]  
> Netsh トレースによって ETL ファイルが作成されます。 ETL ファイルは、Message Analyzer (MA) およびネットワークモニター3.4 でのみ開くことができます (パーサーをネットワークモニターパーサー \> Windows に設定します)。

1. SMB サーバーと SMB クライアントの両方で、 **C**ドライブに**一時**フォルダーを作成します。その後、次のコマンドを実行します。

   ```cmd
   netsh trace start capture=yes report=yes scenario=NetConnection level=5 maxsize=1024 tracefile=c:\\Temp\\%computername%\_nettrace.etl**
   ```
   
   PowerShell を使用している場合は、次のコマンドレットを実行します。
   
   ```PowerShell
   New-NetEventSession -Name trace -LocalFilePath "C:\Temp\$env:computername`_netCap.etl" -MaxFileSize 1024

   Add-NetEventPacketCaptureProvider -SessionName trace -TruncationLength 1500

   Start-NetEventSession trace
   ```
   
2. 問題を再現します。

3. 次のコマンドを実行して、トレースを停止します。

   ```cmd
   netsh trace stop
   ```
   
   PowerShell を使用している場合は、次のコマンドレットを実行します。

   ```PowerShell
   Stop-NetEventSession trace  
   Remove-NetEventSession trace
   ```

> [!NOTE] 
> 転送されるデータの最小量だけをトレースする必要があります。 パフォーマンスの問題については、状況によって許可されている場合は、常に良好なトレースと無効なトレースの両方を取得します。

### <a name="analyze-the-traffic"></a>トラフィックを分析する

SMB は、TCP/IP をネットワークトランスポートプロトコルとして使用するアプリケーションレベルのプロトコルです。 そのため、SMB の問題は TCP/IP の問題によって発生することもあります。

TCP/IP で次の問題が発生しているかどうかを確認します。

1. TCP の3方向ハンドシェイクは終了しません。 これは通常、ファイアウォールブロックがあるか、サーバーサービスが実行されていないことを示します。

2. 転送が発生しています。 これにより、複合 TCP 輻輳調整のために、ファイル転送の速度が低下する可能性があります。

3. 5回の再転送後に TCP リセットが行われると、システム間の接続が失われたか、いずれかの SMB サービスがクラッシュしたか、応答を停止したことを意味します。

4. TCP 受信ウィンドウが非常に強くなっています。 これは、ストレージが遅い場合や、データが補助的な関数ドライバー (AFD) Winsock バッファーから取得されない問題が原因で発生する場合があります。

顕著な TCP/IP の問題がない場合は、SMB エラーを探します。 これを行うには、次の手順に従います。

1. SMB エラーは、SMB2 プロトコル仕様に対して常に確認してください。 多くの SMB エラーは害を受けません (有害ではありません)。 次の情報を参照して、エラーが次の問題のいずれかに関連していることを確認する前に、SMB がエラーを返した理由を特定します。

   - [SMB2 Message 構文](https://docs.microsoft.com/openspecs/windows_protocols/ms-smb2/6eaf6e75-9c23-4eda-be99-c9223c60b181)トピックでは、各 SMB コマンドとそのオプションについて説明します。
    
   - [SMB2 クライアント処理](https://docs.microsoft.com/openspecs/windows_protocols/ms-smb2/df0625a5-6516-4fbe-bf97-01bef451cab2)トピックでは、SMB クライアントが要求を作成し、サーバーメッセージに応答する方法について説明します。

   - [SMB2 Server Processing](https://docs.microsoft.com/openspecs/windows_protocols/ms-smb2/e1d08834-42e0-41ca-a833-fc26f5132a6f)トピックでは、SMB サーバーが要求を作成し、クライアント要求に応答する方法について説明します。

2. FSCTL\_の直後に TCP リセットコマンドが送信されたかどうかを確認し\_ネゴシエート\_情報 (negotiate の検証) コマンドを実行します。 その場合は、次の情報を参照してください。

   - クライアントまたはサーバーでネゴシエートの検証プロセスが失敗した場合、SMB セッションを終了 (TCP リセット) する必要があります。

   - WAN optimizer が SMB ネゴシエートパケットを変更しているため、このプロセスが失敗する可能性があります。

   - 接続が途中で終了した場合は、クライアントとサーバー間の最新の exchange 通信を特定します。

#### <a name="analyze-the-protocol"></a>プロトコルの分析

ネットワークトレースで実際の SMB プロトコルの詳細を確認し、使用されているコマンドとオプションを正確に把握します。

> [!NOTE]
> SMBv3 以降のバージョンのコマンドを解析できるのは、Message Analyzer だけです。

- SMB では、実行するように指示されているだけであることに注意してください。

- アプリケーションが実行しようとしている操作の詳細については、「SMB コマンド」を参照してください。

コマンドと操作をプロトコル仕様と比較して、すべてが正しく動作していることを確認します。 そうでない場合は、下位レベルのデータを収集して、根本原因に関する詳細情報を探します。 これを行うには、次の手順に従います。

1. 標準のパケットキャプチャを収集します。

2. **Netsh**コマンドを実行して、ネットワークスタックに問題があるかどうか、またはファイアウォールやウイルス対策プログラムなどの Windows フィルタリングプラットフォーム (WFP) アプリケーションで削除されたかどうかに関する詳細情報を収集します。

3. 他のすべてのオプションが失敗した場合は、SMB 自体で問題が発生していると思われる場合、または他のどのデータも根本原因を特定するのに十分ではない場合は、t. を収集します。

例 :

- 1つのファイルサーバーへのファイル転送速度が低下しています。

- 両側のトレースは、SRV が読み取り要求に対して低速で応答することを示しています。

- ウイルス対策プログラムを削除すると、低速ファイル転送が解決されます。

- この問題を解決するには、ウイルス対策プログラム manufactory に問い合わせてください。

> [!NOTE]
> 必要に応じて、トラブルシューティング中にウイルス対策プログラムを一時的にアンインストールすること**も**できます。

#### <a name="event-logs"></a>イベント ログ

次のスクリーンショットに示すように、SMB クライアントと SMB サーバーの両方に詳細なイベントログ構造があります。 イベントログを収集して、問題の根本原因を見つけやすくします。

![イベント ログ](media/troubleshooting-smb-1.png)

## <a name="smb-related-system-files"></a>SMB 関連のシステムファイル

ここでは、SMB 関連のシステムファイルの一覧を示します。 システムファイルを更新し続けるには、最新の更新プログラムの[ロールアップ](https://support.microsoft.com/help/4498140/windows-10-update-history)がインストールされていることを確認してください。

**% Windir%\\system32\\ドライバー**の下に一覧表示される SMB クライアントバイナリ:

- RDBSS

- MRXSMB

- MRXSMB10

- MRXSMB20

- MUP.SYS

- SMBdirect

**% Windir%\\system32\\ドライバー**の下に一覧表示される SMB サーバーバイナリ:

- SRVNET

- SRV.SYS

- SRV2

- SMBdirect

- **% Windir%\\system32**の下

- srvsvc .dll

![SMB コンポーネント](media/troubleshooting-smb-2.png)

### <a name="update-suggestions"></a>更新候補

SMB の問題をトラブルシューティングする前に、次のコンポーネントを更新することをお勧めします。

- ファイルサーバーにはファイルストレージが必要です。 記憶域に iSCSI コンポーネントがある場合は、それらのコンポーネントを更新します。

- ネットワークコンポーネントを更新します。

- パフォーマンスと安定性を向上させるには、Windows Core を更新します。

## <a name="reference"></a>参照

[Microsoft SMB プロトコルパケット交換シナリオ](https://docs.microsoft.com/windows/win32/fileio/microsoft-smb-protocol-packet-exchange-scenario)