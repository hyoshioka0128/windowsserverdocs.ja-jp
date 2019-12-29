---
ms.assetid: 0f21951c-b1bf-43bb-a329-bbb40c58c876
title: レプリケーション エラー 1753。エンドポイント マッパーから使用できるエンドポイントはこれ以上ありません
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 64b479663dfc930ec9a6d2055b4c9ad5755b30fc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71389970"
---
# <a name="replication-error-1753-there-are-no-more-endpoints-available-from-the-endpoint-mapper"></a>レプリケーション エラー 1753。エンドポイント マッパーから使用できるエンドポイントはこれ以上ありません

>適用対象: Windows Server

この記事では、Win32 エラー1753で失敗する Active Directory 操作の現象、原因、および解決手順について説明します。「エンドポイントマッパーから使用できるエンドポイントはこれ以上ありません。」

DCDIAG は、接続テスト、Active Directory レプリケーションテスト、または KnowsOfRoleHolders テストが、次のエラー1753で失敗したことを報告しました: "エンドポイントマッパーから使用できるエンドポイントはこれ以上ありません。"

```
Testing server: <site><DC Name>
Starting test: Connectivity
* Active Directory LDAP Services Check
* Active Directory RPC Services Check
[<DC Name>] DsBindWithSpnEx() failed with error 1753,
There are no more endpoints available from the endpoint mapper..
Printing RPC Extended Error Info:
Error Record 1, ProcessID is <process ID> (DcDiag)
System Time is: <date> <time>
Generating component is 2 (RPC runtime)
Status is 1753: There are no more endpoints available from the endpoint mapper. Detection location is 500
NumberOfParameters is 4
Unicode string: ncacn_ip_tcp
Unicode string: <source DC object GUID>._msdcs.contoso.com
Long val: -481213899
Long val: 65537
Error Record 2, ProcessID is 700 (DcDiag)
System Time is: <date> <time>
Generating component is 2 (RPC runtime)
Status is 1753: There are no more endpoints available from the endpoint mapper.
NumberOfParameters is 1
Unicode string: 1025
[Replications Check,<DC Name>] A recent replication attempt failed:
From <source DC> to <destination DC>
Naming Context: <DN path of directory partition>
The replication generated an error (1753):
There are no more endpoints available from the endpoint mapper.
The failure occurred at <date> <time>.
The last success occurred at <date> <time>.
3 failures have occurred since the last success.
The directory on <DC name> is in the process.
of starting up or shutting down, and is not available.
Verify machine is not hung during boot.
```

REPADMIN.EXE は、レプリケーションの試行がステータス1753で失敗したことを報告します。
1753ステータスを一般的に示す REPADMIN コマンドには、次のようなものがあります。

* REPADMIN/REPLSUM
* REPADMIN/SHOWREPL
* REPADMIN/SHOWREPS
* REPADMIN/SYNCALL

"REPADMIN/SHOWREPS" からのサンプル出力では、"レプリケーションアクセスが拒否されました" というエラーが発生し、CONTOSO-DC2 から CONTOSO-DC1 への入力方向のレプリケーションが示されています。

```
Default-First-Site-NameCONTOSO-DC1
DSA Options: IS_GC 
Site Options: (none)
DSA object GUID: b6dc8589-7e00-4a5d-b688-045aef63ec01
DSA invocationID: b6dc8589-7e00-4a5d-b688-045aef63ec01
==== INBOUND NEIGHBORS ======================================
DC=contoso,DC=com
Default-First-Site-NameCONTOSO-DC2 via RPC
DSA object GUID: 74fbe06c-932c-46b5-831b-af9e31f496b2
Last attempt @ <date> <time> failed, result 1753 (0x6d9):
There are no more endpoints available from the endpoint mapper.
<#> consecutive failure(s).
Last success @ <date> <time>.
```

Active Directory サイトおよびサービスの **[レプリケーショントポロジの確認]** コマンドを実行すると、エンドポイントマッパーから使用できるエンドポイントはこれ以上ありません。

ソース DC からの接続オブジェクトを右クリックし、 **[レプリケーショントポロジの確認]** をクリックすると、"エンドポイントマッパーから使用できるエンドポイントはこれ以上ありません" というエラーが表示されます。 画面上のエラーメッセージは次のようになります。

ダイアログタイトルのテキスト: レプリケーショントポロジの確認ダイアログのメッセージテキスト: ドメインコントローラーに接続しようとしたときに、次のエラーが発生しました: エンドポイントマッパーから使用できるエンドポイントはこれ以上ありません。

Active Directory サイトおよびサービスの **[今すぐレプリケート]** コマンドは、"エンドポイントマッパーから使用できるエンドポイントがありません" を返します。
ソース DC からの接続オブジェクトを右クリックし、 **[今すぐレプリケート]** を選択すると、"エンドポイントマッパーから使用できるエンドポイントはこれ以上ありません" というエラーが表示されます。
画面上のエラーメッセージは次のようになります。

ダイアログタイトルテキスト: [今すぐレプリケート] ダイアログメッセージテキスト: ドメインコントローラー \<ソース DC > からドメインコントローラー \<宛先 DC > への名前付けコンテキスト \<% directory パーティション名% > を同期しようとして、次のエラーが発生しました:

エンドポイントマッパーから使用できるエンドポイントはこれ以上ありません。
操作は続行されません

-2146893022 状態の NTDS KCC、NTDS General、または Microsoft-Windows-ActiveDirectory_DomainService イベントは、イベントビューアーのディレクトリサービスログに記録されます。

一般に-2146893022 ステータスを示すイベントには、次のような Active Directory ます。

| イベント ID | イベント ソース | イベントの文字列|
| --- | --- | --- |
| 1655 | NTDS 全般 | Active Directory は、次のグローバル カタログと通信しようとして、試行が成功しなかった場合。 |
| 1925 | NTDS KCC | 次の書き込み可能なディレクトリ パーティションのレプリケーション リンクを確立できませんでした。 |
| 1265 | NTDS KCC | 知識整合性チェッカー (KCC) によって、次のディレクトリパーティションとソースドメインコントローラーに対してレプリケーションアグリーメントを追加しようとしましたが、失敗しました。 |

## <a name="cause"></a>原因

次の手順では、手順 1. の rpc エンドポイントマッパー (EPM) を使用してサーバーアプリケーションを登録し、手順 7. で rpc クライアントからクライアントアプリケーションにデータを渡す方法について説明します。

### <a name="adds-rpc-workflow"></a>RPC ワークフローを追加します。

1. サーバーアプリは、エンドポイントを RPC エンドポイントマッパー (EPM) に登録します。
1. クライアントが (ユーザー、OS、またはアプリケーション開始操作に代わって) RPC 呼び出しを行う
1. クライアント側の RPC は、ターゲットコンピューターの EPM に接続し、エンドポイントに対してクライアント呼び出しを完了するように要求します。
1. サーバーコンピューターの EPM がエンドポイントで応答する
1. クライアント側 RPC はサーバーアプリに接続します
1. サーバーアプリが呼び出しを実行し、結果をクライアント RPC に返します。
1. クライアント側 RPC はクライアントアプリに結果を返します。

エラー1753は、ステップ #3 と #4 の間のエラーによって生成されます。 具体的には、エラー1753は、rpc クライアント (送信先 DC) がポート135経由で RPC サーバー (ソース DC) に接続できたが、rpc サーバー (ソース DC) 上の EPM が対象となる RPC アプリケーションを見つけられず、サーバー側のエラー1753を返したことを意味します。 1753エラーが発生した場合は、RPC クライアント (送信先 DC) が、RPC サーバー (AD レプリケーションソース DC) からネットワーク経由でサーバー側のエラー応答を受信したことを示します。

1753エラーの具体的な根本原因は次のとおりです。

* サーバーアプリが開始されていません (つまり、上記の "詳細" 図の手順 #1)。
* サーバーアプリが開始されましたが、初期化中に何らかのエラーが発生したため、RPC エンドポイントマッパーへの登録ができませんでした (例: "詳細" 図の手順 #1 を試行しましたが、失敗しました)。
* サーバーアプリが開始されましたが、それ以降は停止しました。 (たとえば、上の "詳細" ダイアグラムの手順 #1 は正常に完了しましたが、サーバーが停止したため、後で元に戻されました)。
* サーバーアプリは、エンドポイントを手動で登録解除しました (3 に似ていますが、意図的です。 可能性はありませんが、完全を期すために含まれています)。
* RPC クライアント (宛先 DC) は、DNS、WINS、または host/Lmhosts ファイルの IP マッピングエラーの名前により、意図したものとは異なる RPC サーバーに接続しています。

エラー1753の原因は次のとおりです。

* RPC クライアント (接続先 DC) と RPC サーバー (ソース DC) の間にポート135を介したネットワーク接続がない
* ポート135を使用した RPC サーバー (ソース DC) と、一時的なポートを介した RPC クライアント (接続先 DC) との間にネットワーク接続がない。
* パスワードが一致していないか、ソース DC が Kerberos で暗号化されたパケットの暗号化を解除できない

## <a name="resolutions"></a>解決策

エンドポイントマッパーを使用してサービスを登録するサービスが開始されたことを確認します。

* Windows 2000 および Windows Server 2003 Dc の場合: ソース DC が通常モードで起動されていることを確認します。
* Windows Server 2008 または Windows Server 2008 R2 の場合: ソース DC のコンソールで、サービスマネージャー (services.msc) を起動し、Active Directory Domain Services サービスが実行されていることを確認します。

RPC クライアント (接続先 DC) が目的の RPC サーバー (ソース DC) に接続されていることを確認します。

共通 Active Directory フォレスト内のすべての Dc は、ドメインコントローラーの CNAME レコードを _msdcs に登録します。 フォレスト内に存在するドメインに関係なく、フォレストルートドメイン > DNS ゾーンを \<します。 DC CNAME レコードは、各ドメインコントローラーの NTDS 設定オブジェクトの objectGUID 属性から派生します。

レプリケーションベースの操作を実行する場合、宛先 DC は、ソース Dc CNAME レコードの DNS を照会します。 CNAME レコードには、ソース DC の完全修飾コンピューター名が含まれています。これは、DNS クライアントキャッシュの参照、ホスト/LMHost ファイルの参照、DNS 内のホスト A/AAAA レコード、または WINS を使用してソース Dc の IP アドレスを派生させるために使用されます。

DNS、WINS、Host、および LMHOST ファイルの古い NTDS 設定オブジェクトと無効な名前から IP へのマッピングによって、RPC クライアント (接続先 DC) が間違った RPC サーバー (ソース DC) に接続される場合があります。 さらに、不適切な名前から IP へのマッピングによって、rpc クライアント (送信先 DC) が、RPC サーバーアプリケーション (この場合は Active Directory ロール) がインストールされていないコンピューターに接続する場合があります。 (例: DC2 の古いホストレコードには、DC3 またはメンバーコンピューターの IP アドレスが含まれています)。

コピー先 dc に存在するソース DC の objectGUID が Active Directory のソース dc コピーに格納されているソース DC objectGUID と一致することを確認します。 Active Directory 不整合がある場合は、ntds 設定オブジェクトで repadmin/showobjmeta を使用して、ソース DC の最後の昇格に対応しているものを確認します (ヒント: NTDS 設定オブジェクトの日付スタンプを、ソース dc dcpromo.exe の最後の昇格日に対して/showobjmeta から作成します。 DCPROMO の最後の変更/作成日を使用することが必要になる場合があります。ログファイル自体)。 オブジェクトの Guid が一致しない場合、宛先 DC は、CNAME レコードが IP マッピングに対して不適切な名前を持つホストレコードを参照しているソース DC に対して古い NTDS 設定オブジェクトを持つ可能性があります。

宛先 DC で IPCONFIG/ALL を実行し、宛先 DC が名前解決に使用している DNS サーバーを特定します。

```
c:>ipconfig /all
```

宛先 DC で、ソース Dc の完全修飾 DC CNAME レコードに対して NSLOOKUP を実行します。

```
c:>nslookup -type=cname <fully qualified cname of source DC> <destination DCs primary DNS Server IP >
c:>nslookup -type=cname <fully qualified cname of source DC> <destination DCs secondary DNS Server IP>
```

NSLOOKUP によって返される IP アドレスが、ソース DC のホスト名/セキュリティ id を "所有" していることを確認します。

```
C:>NBTSTAT -A <IP address returned by NSLOOKUP in the step above>
```

ソース DC のコンソールにログオンし、コマンドプロンプトから "IPCONFIG" を実行して、ソース DC が上の NSLOOKUP コマンドによって返された IP アドレスを所有していることを確認します。

DNS でのホストと IP のマッピングが古くなっているか、重複していないか確認します

```
NSLOOKUP -type=hostname <single label hostname of source DC> <primary DNS Server IP on destination DC>
NSLOOKUP -type=hostname <single label hostname of source DC> <secondary DNS Server IP on destination DC>

NSLOOKUP -type=hostname <fully qualified computer name of source DC> <primary DNS Server IP on destination DC>
NSLOOKUP -type=hostname <fully qualified computer name of source DC> <secondary DNS Server IP on dest. DC>
```

ホストレコードに無効な IP アドレスが存在する場合は、DNS 清掃が有効になっていて、適切に構成されているかどうかを調査します。

上記のテストまたはネットワークトレースに無効な IP アドレスを返す名前クエリが表示されない場合は、ホストファイル、LMHOSTS ファイル、WINS サーバーの古いエントリを検討してください。 WINS フォールバック名前解決を実行するように DNS サーバーを構成することもできます。

* サーバーアプリケーション (Active Directory et al) が RPC サーバー (ソース DC) のエンドポイントマッパーに登録されていることを確認します。
* Active Directory は、既知と動的に登録されたポートを組み合わせて使用します。 次の表に、Active Directory ドメインコントローラーで使用される既知のポートとプロトコルを示します。

| RPC サーバーアプリケーション | ポート | TCP | UDP |
| --- | --- | --- | --- |
| DNS サーバー | 53 | X | X |
| Kerberos | 88 | X | X |
| LDAP サーバー | 389 | X | X |
| Microsoft-DS | 445 | X | X |
| LDAP SSL | 636 | X | X |
| グローバル カタログ サーバー | 3268 | X |   |
| グローバル カタログ サーバー | 3269 | X |   |

既知のポートはエンドポイントマッパーに登録されていません。

また、Active Directory およびその他のアプリケーションは、RPC の一時的なポート範囲に動的に割り当てられたポートを受信するサービスも登録します。 このような RPC サーバーアプリケーションには、windows 2000 および windows server 2003 コンピューター上の1024と5000の間に動的に TCP ポートが割り当てられます。また、windows Server 49152 と Windows server 65535 R2 コンピューターでは、2008と2008の範囲の間にポートが割り当てられます。 レプリケーションで使用される RPC ポートは、[サポート技術情報の記事 224196](https://support.microsoft.com/kb/224196)に記載されている手順に従って、レジストリにハードコーディングできます。 ハードコーディングされたポートを使用するように構成されている場合、Active Directory は引き続き EPM に登録されます。

対象の RPC サーバーアプリケーションが rpc サーバーの rpc エンドポイントマッパー (AD レプリケーションの場合はソース DC) に登録されていることを確認します。

このタスクを実行するにはさまざまな方法がありますが、次の構文を使用して、ソース DC のコンソールで管理者特権のコマンドプロンプトから PORTQRY をインストールして実行します。

```
portquery -n <source DC> -e 135 > file.txt
```

Portqry の出力では、ncacn_ip_tcp プロトコルの "MS NT ディレクトリ DRS インターフェイス" (UUID = 351...) によって動的に登録されたポート番号に注意してください。 以下のスニペットは、Windows Server 2008 R2 DC からの portquery の出力例を示しています。

```
UUID: e3514235-4b06-11d1-ab04-00c04fc2dcd2 MS NT Directory DRS Interface
ncacn_np:CONTOSO-DC01[\pipe\lsass] 
UUID: e3514235-4b06-11d1-ab04-00c04fc2dcd2 MS NT Directory DRS Interface
ncacn_np:CONTOSO-DC01[\PIPE\protected_storage] 
UUID: e3514235-4b06-11d1-ab04-00c04fc2dcd2 MS NT Directory DRS Interface
ncacn_ip_tcp:CONTOSO-DC01[49156] 
UUID: e3514235-4b06-11d1-ab04-00c04fc2dcd2 MS NT Directory DRS Interface
ncacn_http:CONTOSO-DC01[49157] 
UUID: e3514235-4b06-11d1-ab04-00c04fc2dcd2 MS NT Directory DRS Interface
ncacn_http:CONTOSO-DC01[6004]
```

このエラーを解決するには、次のような方法があります。

* ソース DC が通常モードで起動し、ソース DC の OS と DC ロールが完全に開始されていることを確認します。
* Active Directory ドメインサービスが実行されていることを確認します。 サービスが現在停止されているか、既定のスタートアップ値を使用して構成されていない場合は、既定のスタートアップ値をリセットし、変更された DC を再起動してから、操作を再試行してください。
* Rpc サービスおよび rpc ロケーターのスタートアップ値とサービスの状態が、rpc クライアント (接続先 DC) と RPC サーバー (ソース DC) の OS バージョンに対して正しいことを確認します。 サービスが現在停止されているか、既定のスタートアップ値を使用して構成されていない場合は、既定のスタートアップ値をリセットし、変更された DC を再起動してから、操作を再試行してください。
   * さらに、サービスコンテキストが次の表に示す既定の設定と一致していることを確認します。

      | サービス | Windows Server 2003 以降の既定の状態 (スタートアップの種類) | Windows Server 2000 の既定の状態 (スタートアップの種類) |
      | --- | --- | --- |
      | リモート プロシージャ コール | 開始 (自動) | 開始 (自動) |
      | リモートプロシージャコールロケーター | Null または停止 (手動) | 開始 (自動) |

* 動的ポート範囲のサイズが制限されていないことを確認します。 RPC ポート範囲を列挙するための Windows Server 2008 および Windows Server 2008 R2 の NETSH 構文を次に示します。

   ```
   netsh int ipv4 show dynamicport tcp
   netsh int ipv4 show dynamicport udp
   netsh int ipv6 show dynamicport tcp
   netsh int ipv6 show dynamicport udp
   ```

* KB 224196 で定義されているハードコードされたポート定義が、ソース Dc の OS バージョンの動的ポート範囲内にあることを確認します。 [サポート技術情報の記事 224196](https://support.microsoft.com/kb/224196)を確認し、ハードコーディングされたポートがソース DC のオペレーティングシステムのバージョンの一時的なポート範囲内にあることを確認します。

* プロトコルキーが HKLM\Software\Microsoft\Rpc の下に存在し、次の5つの既定値が含まれていることを確認します。

   ```
   ncacn_http REG_SZ rpcrt4.dll
   ncacn_ip_tcp REG_SZ rpcrt4.dll
   ncacn_nb_tcp REG_SZ rpcrt4.dll
   ncacn_np REG_SZ rpcrt4.dll
   ncacn_ip_udp REG_SZ rpcrt4.dll
   ```

## <a name="more-information"></a>詳細情報

RPC エラー1753と-2146893022: ターゲットプリンシパル名が正しくないことが原因で、IP マッピングへの不適切な名前が指定されている例

Contoso.com ドメインは DC1 と DC2 で構成され、IP アドレスは x. x. x. x. 1.2 です。 DC2 のホスト "A"/"AAAA" レコードは、DC1 用に構成されたすべての DNS サーバーに正しく登録されています。 さらに、DC1 の HOSTS ファイルには、完全修飾ホスト名を IP アドレス DC2s にマッピングするエントリが含まれています。 その後、DC2's の IP アドレスの変更と、新しいメンバーコンピューターが、IP アドレスが x. x. 1.2 のドメインに参加するようになります。 Active Directory サイトとサービススナップインの **[今すぐレプリケート]** コマンドによってトリガーされた AD レプリケーションの試行は、次のトレースに示すように、エラー1753で失敗します。

```
F# SRC    DEST    Operation
1 x.x.1.1 x.x.1.2 ARP:Request, x.x.1.1 asks for x.x.1.2
2 x.x.1.2 x.x.1.1 ARP:Response, x.x.1.2 at 00-13-72-28-C8-5E
3 x.x.1.1 x.x.1.2 TCP:Flags=......S., SrcPort=50206, DstPort=DCE endpoint resolution(135)
4 x.x.1.2 x.x.1.1 ARP:Request, x.x.1.2 asks for x.x.1.1
5 x.x.1.1 x.x.1.2 ARP:Response, x.x.1.1 at 00-15-5D-42-2E-00
6 x.x.1.2 x.x.1.1 TCP:Flags=...A..S., SrcPort=DCE endpoint resolution(135)
7 x.x.1.1 x.x.1.2 TCP:Flags=...A...., SrcPort=50206, DstPort=DCE endpoint resolution(135)
8 x.x.1.1 x.x.1.2 MSRPC:c/o Bind: UUID{E1AF8308-5D1F-11C9-91A4-08002B14A0FA} EPT(EPMP)
9 x.x.1.2 x.x.1.1 MSRPC:c/o Bind Ack: Call=0x2 Assoc Grp=0x5E68 Xmit=0x16D0 Recv=0x16D0
10 x.x.1.1 x.x.1.2 EPM:Request: ept_map: NDR, DRSR(DRSR) {E3514235-4B06-11D1-AB04-00C04FC2DCD2} [DCE endpoint resolution(135)]
11 x.x.1.2 x.x.1.1 EPM:Response: ept_map: 0x16C9A0D6 - EP_S_NOT_REGISTERED
```

フレーム**10**で、宛先 dc は、ソース dc エンドポイントマッパーをポート135経由で Active Directory レプリケーションサービスクラス UUID E351... に対して照会します。

フレーム**11**では、ソース dc (この場合は、dc ロールをまだホストしていないため、E351...ローカル EPM を使用したレプリケーションサービスの UUID は、シンボリックエラー EP_S_NOT_REGISTERED を返します。このエラーは、10進数のエラー1753、16進数のエラー0x6d9、および "エンドポイントマッパーから使用できるエンドポイントがありません" にマップされます。

その後、IP アドレスが x. x. 1.2 のメンバーコンピューターは、contoso.com ドメインのレプリカ "" に昇格します。 ここでも、 **[今すぐレプリケート]** コマンドを使用してレプリケーションを開始しますが、この時間は "ターゲットプリンシパル名が正しくありません" というエラーが表示されて失敗します。 ネットワークアダプターが割り当てられているコンピューターの IP アドレスは、ドメインコントローラーであり、現在通常モードで起動されていて、E351...レプリケーションサービスの UUID はローカルの EPM を使用しますが、DC2 の名前またはセキュリティ id を所有しておらず、DC1 から Kerberos 要求の暗号化を解除できないため、要求は "ターゲットプリンシパル名が正しくありません" というエラーで失敗するようになりました。 このエラーは、10進数のエラー-2146893022/16 進数のエラー0x80090322 にマップされます。

このような無効なホスト間マッピングは、ホスト/lmhost ファイルの古いエントリ、DNS 内のホスト A/AAAA 登録、または WINS によって発生する可能性があります。

概要: この例では、ホスト間の無効なマッピング (この場合はホストファイル内) が原因で、ターゲット DC が、Active Directory Domain Services サービスが実行されていない "ソース" DC (またはその問題のためにインストールされている) に解決されたために失敗しました。レプリケーション SPN がまだ登録されていないため、ソース DC からエラー1753が返されました。 2番目のケースでは、ホストから IP への無効なマッピング (ホストファイルでも) が原因で、宛先 DC が、E351...レプリケーション SPN ですが、そのソースには意図したソース DC とは異なるホスト名とセキュリティ id があるため、試行は失敗しました。エラー-2146893022: ターゲットプリンシパル名が正しくありません。

## <a name="related-topics"></a>関連トピック

* [エラー1753で失敗した Active Directory 操作のトラブルシューティング: エンドポイントマッパーから使用できるエンドポイントはこれ以上ありません。](https://support.microsoft.com/kb/2089874)
* [サポート技術情報の記事839880製品 CD からの Windows Server 2003 サポートツールを使用した RPC エンドポイントマッパーエラーのトラブルシューティング](https://support.microsoft.com/kb/839880)
* [サポート技術情報の記事 832017 Windows Server システムのサービスの概要とネットワークポートの要件](https://support.microsoft.com/kb/832017/)
* [サポート技術情報の記事 224196 Active Directory レプリケーショントラフィックとクライアント RPC トラフィックを特定のポートに制限する](https://support.microsoft.com/kb/224196/)
* [サポート技術情報の記事 154596: ファイアウォールで動作するように RPC 動的ポート割り当てを構成する方法](https://support.microsoft.com/kb/154596)
* [RPC のしくみ](https://msdn.microsoft.com/library/aa373935(VS.85).aspx)
* [サーバーが接続を準備する方法](https://msdn.microsoft.com/library/aa373938(VS.85).aspx)
* [クライアントが接続を確立する方法](https://msdn.microsoft.com/library/aa373937(VS.85).aspx)
* [インターフェイスの登録](https://msdn.microsoft.com/library/aa375357(VS.85).aspx)
* [ネットワーク上でサーバーを使用できるようにする](https://msdn.microsoft.com/library/aa373974(VS.85).aspx)
* [登録 (エンドポイントを)](https://msdn.microsoft.com/library/aa375255(VS.85).aspx)
* [リッスン (クライアント呼び出しを)](https://msdn.microsoft.com/library/aa373966(VS.85).aspx)
* [クライアントが接続を確立する方法](https://msdn.microsoft.com/library/aa373937(VS.85).aspx)
* [特定のポートへの Active Directory レプリケーショントラフィックとクライアント RPC トラフィックを制限する](https://support.microsoft.com/kb/224196)
* [AD DS 内のターゲット DC の SPN](https://msdn.microsoft.com/library/dd207688(PROT.13).aspx)
