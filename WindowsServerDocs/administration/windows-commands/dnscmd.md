---
title: dnscmd
description: Dnscmd コマンドのリファレンストピックです。これは、DNS サーバーを管理するためのコマンドラインインターフェイスです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e7f31cb5-a426-4e25-b714-88712b8defd5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7c279513549ba149974933c33044fa861fa89a62
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2020
ms.locfileid: "83437037"
---
# <a name="dnscmd"></a>Dnscmd

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

DNS サーバーを管理するためのコマンド ライン インターフェイスです。 このユーティリティは、日常的な DNS 管理タスクを自動化したり、ネットワーク上で新しい DNS サーバーを簡単に無人セットアップおよび構成したりするために、バッチファイルのスクリプトを作成する場合に役立ちます。

## <a name="syntax"></a>構文

```
dnscmd <servername> <command> [<command parameters>]
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| --------- | ----------- |
| `<servername>` | リモートまたはローカルの DNS サーバーの IP アドレスまたはホスト名。 |

## <a name="dnscmd-ageallrecords-command"></a>dnscmd/ageallrecords コマンド

DNS サーバー上の指定されたゾーンまたはノードにあるリソースレコードについて、タイムスタンプの現在の時刻を設定します。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /ageallrecords <zonename>[<nodename>] | [/tree]|[/f]
```

#### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| ---------- | ----------- |
| `<servername>` | 管理者が管理を計画している DNS サーバーを指定します。これは、IP アドレス、完全修飾ドメイン名 (FQDN)、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |
| `<zonename>` | ゾーンの FQDN を指定します。 |
| `<nodename>` | 次のものを使用して、ゾーン内の特定のノードまたはサブツリーを指定します。<ul><li>**@** ルートゾーンまたは FQDN の場合</li><li>ノードの FQDN (末尾にピリオド (.) を含む名前)</li><li>ゾーンルートに対して相対的な名前の1つのラベル。</li></ul> |
| /ツリー | すべての子ノードもタイムスタンプを受け取ることを指定します。 |
| /f | 確認を求めずにコマンドを実行します。 |

##### <a name="remarks"></a>解説

- **Ageallrecords**コマンドは、現在のバージョンの dns と、エージングと清掃がサポートされていない以前のリリースとの下位互換性を維持するためのものです。 現在の時刻のタイムスタンプをタイムスタンプのないリソースレコードに追加し、タイムスタンプを持つリソースレコードに現在の時刻を設定します。

- レコードにタイムスタンプが付いていない場合、レコードの清掃は行われません。 ネームサーバー (NS) リソースレコード、start of authority (SOA) リソースレコード、および Windows Internet Name Service (WINS) リソースレコードは清掃プロセスに含まれず、 **ageallrecords**コマンドを実行してもタイムスタンプがありません。

- DNS サーバーとゾーンで清掃が有効になっていない場合、このコマンドは失敗します。 ゾーンの清掃を有効にする方法の詳細について**aging**は、 `dnscmd /config` この記事のコマンドの構文内で、aging パラメーターを参照してください。

- DNS リソースレコードにタイムスタンプを追加すると、Windows Server 以外のオペレーティングシステムで実行されている DNS サーバーとの互換性がなくなります。 **Ageallrecords**コマンドを使用して追加されたタイムスタンプを元に戻すことはできません。

- 省略可能なパラメーターが指定されていない場合、コマンドは、指定されたノードにあるすべてのリソースレコードを返します。 少なくとも1つの省略可能なパラメーターに値が指定されている場合、 **dnscmd**は、省略可能なパラメーターに指定されている値または値に対応するリソースレコードのみを列挙します。

### <a name="examples"></a>例

[例 1: タイムスタンプの現在の時刻をリソースレコードに設定する](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)#example-1-set-the-current-time-on-a-time-stamp-to-resource-records)

## <a name="dnscmd-clearcache-command"></a>dnscmd/clearcache コマンド

指定した DNS サーバー上にあるリソースレコードの DNS キャッシュメモリを消去します。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /clearcache
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |

### <a name="example"></a>例

```
dnscmd dnssvr1.contoso.com /clearcache
```

## <a name="dnscmd-config-command"></a>dnscmd/config コマンド

DNS サーバーと個々のゾーンのレジストリの値を変更します。 このコマンドは、指定されたサーバーの構成も変更します。 サーバーレベルとゾーンレベルの設定を受け入れます。

> [!CAUTION]
> 代替手段がなければ、レジストリを直接編集しないでください。 レジストリエディターでは、標準のセーフガードがバイパスされるため、パフォーマンスを低下させたり、システムに損害を与えたり、Windows の再インストールが必要になることもあります。 ほとんどのレジストリ設定は、コントロールパネルまたは Microsoft 管理コンソール (mmc) のプログラムを使用して、安全に変更できます。 レジストリを直接編集する必要がある場合は、最初にバックアップします。 詳細については、レジストリエディターのヘルプを参照してください。

### <a name="server-level-syntax"></a>サーバーレベルの構文

```
dnscmd [<servername>] /config <parameter>
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理を計画している DNS サーバーを指定します。これは、ローカルコンピューターの構文、IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |
| `<parameter>` | 設定を指定し、オプションとして値を指定します。 パラメーター値には、*パラメーター* [*値*] という構文を使用します。 |
| /addressの制限`[0|5-28]` | DNS サーバーがクエリに応答して送信できるホストレコードの最大数を指定します。 値はゼロ (0)、または 5 ~ 28 レコードの範囲で指定できます。 既定値は 0 です。 |
| /bindセカンダリ`[0|1]` | 最大の圧縮と効率を実現できるように、ゾーン転送の形式を変更します。 次の値を受け入れます。<ul><li>**0** : 最大圧縮を使用します。 BIND バージョン4.9.4 以降のみと互換性があります。</li><li>**1** -Microsoft 以外の DNS サーバーにメッセージごとに1つのリソースレコードだけを送信し、4.9.4 より前のバインドバージョンと互換性があります。 これが既定の設定です。</li></ul> |
| /bootmethod`[0|1|2|3]` | DNS サーバーの構成情報の取得元となるソースを指定します。 次の値を受け入れます。<ul><li>**0** -構成情報のソースをクリアします。</li><li>**1** -DNS ディレクトリにあるバインドファイル (既定では) から読み込まれ `%systemroot%\System32\DNS` ます。</li><li>**2** -レジストリから読み込まれます。</li><li>**3** -AD DS とレジストリから読み込みます。 これが既定の設定です。</li></ul> |
| /defaultagingstate`[0|1]` | 新しく作成されたゾーンで DNS 清掃機能が既定で有効になっているかどうかを判断します。 次の値を受け入れます。<ul><li>**0** -清掃を無効にします。 これが既定の設定です。</li><li>**1** -清掃を有効にします。</li></ul> |
| /defaultnorefreshinterval`[0x1-0xFFFFFFFF|0xA8]` | 動的に更新されたレコードの更新が受け付けられない期間を設定します。 サーバー上のゾーンは、この値を自動的に継承します。<p>既定値を変更するには、 **0x1-0xffffffff**の範囲の値を入力します。 サーバーの既定値は**0Xa8**です。 |
| /defaultrefreshinterval`[0x1-0xFFFFFFFF|0xA8]` | DNS レコードの動的更新で許容される期間を設定します。 サーバー上のゾーンは、この値を自動的に継承します。<p>既定値を変更するには、 **0x1-0xffffffff**の範囲の値を入力します。 サーバーの既定値は**0Xa8**です。 |
| /disableautoreversezones`[0|1]` | 逆引き参照ゾーンの自動作成を有効または無効にします。 逆引き参照ゾーンは、DNS ドメイン名に対するインターネットプロトコル (IP) アドレスの解決を提供します。 次の値を受け入れます。<ul><li>**0** -逆引き参照ゾーンの自動作成を有効にします。 これが既定の設定です。</li><li>**1** -逆引き参照ゾーンの自動作成を無効にします。</li></ul> |
| /disablensrecordsautocreation`[0|1]` | DNS サーバーがホストするゾーンのネームサーバー (NS) リソースレコードを自動的に作成するかどうかを指定します。 次の値を受け入れます。<ul><li>**0** -DNS サーバーがホストするゾーンのネームサーバー (NS) リソースレコードを自動的に作成します。</li><li>**1** -DNS サーバーがホストするゾーンのネームサーバー (NS) リソースレコードは自動的に作成されません。</li></ul> |
| /dspollinginterval`[0-30]` | Active directory 統合ゾーンの変更に対して、DNS サーバーが AD DS をポーリングする頻度を指定します。 |
| /dstombstoneinterval`[1-30]` |削除されたレコードを AD DS に保持する時間 (秒単位)。 |
| /ednscachetimeout`[3600-15724800]` | 拡張 DNS (EDNS) 情報をキャッシュする秒数を指定します。 最小値は**3600**、最大値は**15724800**です。 既定値は**604800**秒 (1 週間) です。 |
| /enableednsプローブ`[0|1]` | 他のサーバーをプローブして、EDNS がサポートされているかどうかを確認するサーバーを有効または無効にします。 次の値を受け入れます。<ul><li>**0** -EDNS プローブのアクティブなサポートを無効にします。</li><li>**1** -EDNS プローブのアクティブなサポートを有効にします。</li></ul> |
| /enablednssec`[0|1]` | DNS セキュリティ拡張機能 (DNSSEC) のサポートを有効または無効にします。 次の値を受け入れます。<ul><li>**0** -DNSSEC を無効にします。</li><li>**1** -DNSSEC を有効にします。</li></ul> |
| /enableglobalnamessupport`[0|1]` | GlobalNames ゾーンのサポートを有効または無効にします。 GlobalNames ゾーンは、フォレスト全体での単一ラベルの DNS 名の解決をサポートしています。 次の値を受け入れます。<ul><li>**0** -GlobalNames ゾーンのサポートを無効にします。 このコマンドの値を0に設定すると、DNS サーバーサービスは GlobalNames ゾーン内の単一ラベル名を解決しません。</li><li>**1** -GlobalNames ゾーンのサポートを有効にします。 このコマンドの値を1に設定すると、DNS サーバーサービスは GlobalNames ゾーン内の単一ラベル名を解決します。</li></ul> |
| /enableglobalqueryblocklist`[0|1]` | リスト内の名前の名前解決をブロックするグローバルクエリブロックリストのサポートを有効または無効にします。 DNS サーバーサービスは、サービスが初めて開始されるときに、既定でグローバルクエリブロックリストを作成し、有効にします。 現在のグローバルクエリブロックの一覧を表示するには、dnscmd/info **/globalqueryblocklist**コマンドを使用します。 次の値を受け入れます。<ul><li>**0** -グローバルクエリブロックリストのサポートを無効にします。 このコマンドの値を0に設定すると、DNS サーバーサービスはブロック一覧内の名前に対するクエリに応答します。</li><li>**1** -グローバルクエリブロックリストのサポートを有効にします。 このコマンドの値を1に設定すると、DNS サーバーサービスはブロック一覧内の名前に対するクエリに応答しません。</li></ul> |
| /eventloglevel`[0|1|2|4]` | イベントビューアーの DNS サーバーログに記録されるイベントを指定します。 次の値を受け入れます。<ul><li>**0** -イベントをログに記録しません。</li><li>**1** -エラーのみをログに記録します。</li><li>**2** -エラーと警告のみをログに記録します。</li><li>**4** -エラー、警告、および情報イベントをログに記録します。 これが既定の設定です。</li></ul> |
| /forward委任`[0|1]` | DNS サーバーが委任されたサブゾーンのクエリをどのように処理するかを決定します。 これらのクエリは、クエリで参照されているサブゾーン、または DNS サーバーの名前が付けられているフォワーダーの一覧のいずれかに送信できます。 設定のエントリは、転送が有効になっている場合にのみ使用されます。 次の値を受け入れます。<ul><li>**0** -委任されたサブゾーンを参照するクエリを適切なサブゾーンに自動的に送信します。 これが既定の設定です。</li><li>**1** -委任されたサブゾーンを参照するクエリを既存のフォワーダーに転送します。</li></ul> |
| /forwardingtimeout`[<seconds>]` | フォワーダーが応答するの**0x1-0xFFFFFFFF**を待ってから、別のフォワーダーを試すまでの DNS サーバーの秒数を指定します。 既定値は**0x5**、5秒です。 |
| /globalneamesqueryorder`[0|1]` | 名前を解決するときに、DNS サーバーサービスが GlobalNames ゾーンまたはローカルゾーンで最初に表示されるかどうかを指定します。 次の値を受け入れます。<ul><li>**0** : DNS サーバーサービスは、対象となるゾーンに対してクエリを実行する前に、GlobalNames ゾーンに対してクエリを実行して名前の解決を試みます。</li><li>**1** -DNS サーバーサービスは、GlobalNames ゾーンに対してクエリを実行する前に、権限があるゾーンを照会することによって名前の解決を試みます。</li></ul> |
| /globalqueryblocklist`[[<name> [<name>]...]` | 現在のグローバルクエリブロックの一覧を、指定した名前の一覧に置き換えます。 名前を指定しない場合、このコマンドはブロック一覧をクリアします。 既定では、グローバルクエリブロックの一覧には次の項目が含まれています。<ul><li>isatap</li><li>wpad</li></ul>DNS サーバーサービスは、既存のゾーンでこれらの名前が見つかった場合、最初に開始したときにこれらの名前のいずれかまたは両方を削除できます。 |
| /isスレーブ`[0|1]` | 転送されるクエリが応答を受信しない場合に、DNS サーバーがどのように応答するかを決定します。 次の値を受け入れます。<ul><li>**0** -DNS サーバーが下位のものではないことを指定します。 フォワーダーが応答しない場合、DNS サーバーはクエリ自体の解決を試みます。 これが既定の設定です。</li><li>**1** -DNS サーバーが下位であることを指定します。 フォワーダーが応答しない場合、DNS サーバーは検索を終了し、エラーメッセージを競合回避モジュールに送信します。</li></ul> |
| /localnetpriority`[0|1]` | DNS サーバーに同じ名前のホストレコードが複数ある場合に、ホストレコードが返される順序を決定します。 次の値を受け入れます。<ul><li>**0** : レコードを DNS データベースに一覧表示されている順序で返します。</li><li>**1** -最初に類似した IP ネットワークアドレスを持つレコードを返します。 これが既定の設定です。</li></ul> |
| /logfilemaxsize`[<size>]` | Dns .log ファイルの最大サイズ (バイト数 **-0xffffffff**) を指定します。 ファイルの最大サイズに達すると、DNS は最も古いイベントを上書きします。 既定のサイズは**0x400000**で、4メガバイト (mb) です。 |
| /logfilepath`[<path+logfilename>]` | Dns .log ファイルのパスを指定します。 既定のパスは `%systemroot%\System32\Dns\Dns.log` です。 形式を使用して別のパスを指定することもでき `path+logfilename` ます。 |
| /logipfilterlist`<IPaddress> [,<IPaddress>...]` | どのパケットがデバッグログファイルに記録されるかを指定します。 エントリは、IP アドレスの一覧です。 一覧の IP アドレスとの間で送受信されるパケットだけがログに記録されます。 |
| /loglevel`[<eventtype>]` | Dns .log ファイルに記録されるイベントの種類を決定します。 各イベントの種類は、16進数で表されます。 ログに複数のイベントが必要な場合は、16進数の追加を使用して値を追加し、合計を入力します。 次の値を受け入れます。<ul><li>**0x0** -DNS サーバーはログを作成しません。 これが既定のエントリです。</li><li>**0x10** -クエリと通知をログに記録します。</li><li>**0x20** -更新をログに記録します。</li><li>**0xfe** -クエリ以外のトランザクションをログに記録します。</li><li>**0x100** -質問トランザクションをログに記録します。</li><li>**0x200** -応答をログに記録します。</li><li>**0x1000** -ログの送信パケット。</li><li>**0x2000** -ログはパケットを受信します。</li><li>**0x4000** -ユーザーデータグラムプロトコル (UDP) パケットをログに記録します。</li><li>**0x8000** -伝送制御プロトコル (TCP) パケットをログに記録します。</li><li>**0xffff** -すべてのパケットをログに記録します。</li><li>**: active** directory 書き込みトランザクションをログに記録します。</li><li>**0x20000** -active directory 更新トランザクションをログに記録します。</li><li>**0x1000000** -完全なパケットをログに記録します。</li><li>**0x80000000** -書き込みトランザクションをログに記録します。</li><li></ul> |
| /maxcachesize | DNS サーバーのメモリキャッシュの最大サイズをキロバイト (KB) 単位で指定します。 |
| /maxcachettl`[<seconds>]` | レコードがキャッシュに保存される秒数 (**0x0-0xffffffff**) を決定します。 **0x0**の設定を使用すると、DNS サーバーはレコードをキャッシュしません。 既定の設定は、 **0x15180** (86400 秒または1日) です。 |
| /maxnegativecachettl`[<seconds>]` | クエリに対する否定応答を記録するエントリが DNS キャッシュに格納されたままになる秒数を指定します (**0x1-0xffffffff**)。 既定の設定は**0x384** (900 秒) です。 |
| /namecheckflag`[0|1|2|3]` | DNS 名をチェックするときに使用する文字の標準を指定します。 次の値を受け入れます。<ul><li>**0** : インターネット技術標準化委員会 (IETF) の Request for Comments (rfc) に準拠した ANSI 文字を使用します。</li><li>**1** -必ずしも IETF rfc に準拠していない ANSI 文字を使用します。</li><li>**2** -マルチバイト UCS 変換形式 8 (utf-8) 文字を使用します。 これが既定の設定です。</li><li>**3** -すべての文字を使用します。</li></ul> |
| /norecursion`[0|1]` | DNS サーバーが再帰的な名前解決を実行するかどうかを決定します。 次の値を受け入れます。<ul><li>**0** : DNS サーバーは、クエリで要求されている場合、再帰的な名前解決を実行します。 これが既定の設定です。</li><li>**1** -DNS サーバーは、再帰的な名前解決を実行しません。</li></ul> |
| /notcp | このパラメーターは互換性のために残されていますが、現在のバージョンの Windows Server には影響しません。 |
| /recursionretry`[<seconds>]` | DNS サーバーがリモートサーバーへの接続を再試行する前に待機する秒数 (**0x1-0xffffffff**) を指定します。 既定の設定は**0x3** (3 秒) です。 この値は、低速のワイドエリアネットワーク (WAN) リンクで再帰が発生した場合に増加する必要があります。 |
| /recursiontimeout`[<seconds>]` | DNS サーバーがリモートサーバーへの接続試行を中止するまでに待機する秒数 (**0x1-0xffffffff**) を指定します。 設定の範囲は**0x1** ~ **0xffffffff**です。 既定の設定は**0xf です**(15 秒) です。 この値は、低速 WAN リンク経由で再帰が発生した場合に増加する必要があります。 |
| その他の方法`[0|1]` | サーバーに同じ名前のホストレコードが複数ある場合に、ホストレコードが返される順序を決定します。 次の値を受け入れます。<ul><li>**0** : DNS サーバーはラウンドロビンを使用しません。 代わりに、最初のレコードがすべてのクエリに返されます。</li><li>**1** -DNS サーバーは、返されたレコードの中から、一致するレコードの一覧の一番上から一番下までをローテーションします。 これが既定の設定です。</li></ul> |
| /rpcprotocol`[0x0|0x1|0x2|0x4|0xFFFFFFFF]` | リモートプロシージャコール (RPC) が DNS サーバーから接続するときに使用するプロトコルを指定します。 次の値を受け入れます。<ul><li>**0x0** -DNS の RPC を無効にします。</li><li>**0x01** -Tcp/ip を使用します。</li><li>**0x2** -名前付きパイプを使用します。</li><li>**0x4** -ローカルプロシージャコール (LPC) を使用します。</li><li>**0xffffffff** -すべてのプロトコル。 これが既定の設定です。</li></ul> |
| /scavenginginterval`[<hours>]` | DNS サーバーの清掃機能が有効になっているかどうかを判断し、清掃サイクル間の時間数 (**0x0-0xffffffff**) を設定します。 既定の設定は**0x0**で、DNS サーバーの清掃を無効にします。 **0x0**を超える設定では、サーバーの清掃が有効になり、清掃サイクル間の時間数が設定されます。 |
| /secureresponses`[0|1]` | DNS がキャッシュに保存されているレコードをフィルター処理するかどうかを指定します。 次の値を受け入れます。<ul><li>**0** -クエリに名前を指定するすべての応答をキャッシュに保存します。 これが既定の設定です。</li><li>**1** -同じ DNS サブツリーに属するレコードのみをキャッシュに保存します。</li></ul> |
| /sendport`[<port>]` | 再帰クエリを他の DNS サーバーに送信するために DNS が使用するポート番号 (**0x0-0xffffffff**) を指定します。 既定の設定は**0x0**です。これは、ポート番号がランダムに選択されることを意味します。 |
| /serverlevelplugindll`[<dllpath>]` | カスタムプラグインのパスを指定します。 Dllpath が有効な DNS サーバープラグインの完全修飾パス名を指定すると、DNS サーバーはプラグイン内の関数を呼び出して、ローカルにホストされているすべてのゾーンのスコープ外にある名前クエリを解決します。 照会された名前がプラグインのスコープ外の場合、DNS サーバーは、構成どおりに転送または再帰を使用して名前解決を実行します。 Dllpath が指定されていない場合、カスタムプラグインが既に構成されている場合、DNS サーバーはカスタムプラグインを使用しなくなります。 |
| /strictfileparsing`[0|1]` | ゾーンの読み込み中に誤ったレコードが検出された場合の DNS サーバーの動作を決定します。 次の値を受け入れます。<ul><li>**0** -サーバーでエラーが発生した場合でも、DNS サーバーは引き続きゾーンを読み込みます。 このエラーは、DNS ログに記録されます。 これが既定の設定です。</li><li>**1** -dns サーバーはゾーンの読み込みを停止し、dns ログにエラーを記録します。</li></ul> |
| /updateoptions`<RecordValue>` | 指定された種類のレコードの動的更新を禁止します。 ログで複数のレコードの種類を禁止する場合は、16進数の追加を使用して値を追加し、合計を入力します。 次の値を受け入れます。<ul><li>**0x0** -レコードの種類を制限しません。</li><li>**0x1** -start of AUTHORITY (SOA) リソースレコードを除外します。</li><li>**0x2** -ネームサーバー (NS) リソースレコードを除外します。</li><li>**0x4** -ネームサーバー (NS) リソースレコードの委任を除外します。</li><li>**0x8** -サーバーホストレコードを除外します。</li><li>**0x100** -セキュリティで保護された動的更新中に、start of AUTHORITY (SOA) リソースレコードを除外します。</li><li>**0x200** -セキュリティで保護された動的更新中に、ルートネームサーバー (NS) リソースレコードを除外します。</li><li>**0X30f** -標準の動的更新中に、ネームサーバー (NS) リソースレコード、start of AUTHORITY (SOA) リソースレコード、およびサーバーホストレコードは除外されます。 セキュリティで保護された動的更新中に、ルートネームサーバー (NS) リソースレコードと start of authority (SOA) リソースレコードは除外されます。 委任およびサーバーホストの更新を許可します。</li><li>**0x400** -セキュリティで保護された動的更新中に、委任ネームサーバー (NS) リソースレコードを除外します。</li><li>**0x800** -セキュリティで保護された動的更新中に、サーバーホストレコードを除外します。</li><li>**0x1000000** -委任署名者 (DS) レコードを除外します。</li><li>**0x80000000** -DNS 動的更新を無効にします。</li></ul> |
| /writeauthorityns`[0|1]` | DNS サーバーがネームサーバー (NS) リソースレコードを応答の機関セクションに書き込むタイミングを決定します。 次の値を受け入れます。<ul><li>**0** : ネームサーバー (NS) リソースレコードを、参照のみの Authority セクションに書き込みます。 この設定は、Rfc 1034、ドメイン名の概念と機能、および Rfc 2181 を使用して DNS 仕様に準拠しています。 これが既定の設定です。</li><li>**1** -すべての正常な権限のある応答の Authority セクションにネームサーバー (NS) リソースレコードを書き込みます。</li></ul> |
| /xfrconnecttimeout`[<seconds>]` | プライマリ DNS サーバーがセカンダリサーバーからの転送応答を待機する秒数を指定します (**0x0-0xffffffff**)。 既定値は**0x1e** (30 秒) です。 タイムアウト値が期限切れになると、接続は終了します。 |

### <a name="zone-level-syntax"></a>ゾーンレベルの構文

指定されたゾーンの構成を変更します。 ゾーン名はゾーンレベルのパラメーターに対してのみ指定する必要があります。

```
dnscmd /config <parameters>
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<parameter>` | 設定、ゾーン名、およびをオプションの値として指定します。 パラメーター値には、次の構文を使用 `zonename parameter [value]` します。 |
| /aging`<zonename>`| 特定のゾーンでの清掃を有効または無効にします。 |
| /allownsレコードの自動作成 `<zonename>``[value]` | DNS サーバーのネームサーバー (NS) リソースレコードの自動作成設定を上書きします。 このゾーンに既に登録されているネームサーバー (NS) リソースレコードには影響しません。 そのため、不要になった場合は、手動で削除する必要があります。 |
| /allowupdate`<zonename>` | 指定されたゾーンが動的更新を受け入れるかどうかを判断します。 |
| /forwarderslave`<zonename>` | DNS**サーバーの**設定を上書きします。 |
| /forwardertimeout`<zonename>` | フォワーダーが応答するのを DNS ゾーンが待機する秒数を指定します。この秒数が経過すると、別のフォワーダーが試行されます。 この値は、サーバーレベルで設定されている値よりも優先されます。 |
| /norefreshinterval`<zonename>` | 指定されたゾーンの DNS レコードを動的に更新できないゾーンの時間間隔を設定します。 |
| /refreshinterval`<zonename>` | 更新によって指定されたゾーンの DNS レコードを動的に更新できるゾーンの時間間隔を設定します。 |
| /securesecondaries`<zonename>` | このゾーンのマスタサーバーからゾーンの更新を受け取ることができるセカンダリサーバーを決定します。 |

## <a name="dnscmd-createbuiltindirectorypartitions-command"></a>dnscmd/createbuiltindirectorypartitions コマンド

DNS アプリケーション ディレクトリ パーティションを作成します。 DNS をインストールすると、サービスのアプリケーションディレクトリパーティションがフォレストレベルとドメインレベルで作成されます。 このコマンドを使用して、削除された、または作成されていない DNS アプリケーションディレクトリパーティションを作成します。 パラメーターを指定しない場合、このコマンドはドメインの組み込みの DNS ディレクトリパーティションを作成します。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /createbuiltindirectorypartitions [/forest] [/alldomains]
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |
| /forest | フォレストの DNS ディレクトリパーティションを作成します。 |
| /alldomains | フォレスト内のすべてのドメインに対して DNS パーティションを作成します。 |

## <a name="dnscmd-createdirectorypartition-command"></a>dnscmd/createdirectorypartition コマンド

DNS アプリケーション ディレクトリ パーティションを作成します。 DNS をインストールすると、サービスのアプリケーションディレクトリパーティションがフォレストレベルとドメインレベルで作成されます。 この操作では、追加の DNS アプリケーションディレクトリパーティションを作成します。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /createdirectorypartition <partitionFQDN>
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |
| `<partitionFQDN>` | 作成される DNS アプリケーションディレクトリパーティションの FQDN。 |

## <a name="dnscmd-deletedirectorypartition-command"></a>dnscmd/deletedirectorypartition コマンド

既存の DNS アプリケーションディレクトリパーティションを削除します。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /deletedirectorypartition <partitionFQDN>
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |
| `<partitionFQDN>` | 削除される DNS アプリケーションディレクトリパーティションの FQDN。 |

## <a name="dnscmd-directorypartitioninfo-command"></a>dnscmd/directorypartitioninfo コマンド

指定された DNS アプリケーションディレクトリパーティションに関する情報を一覧表示します。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /directorypartitioninfo <partitionFQDN> [/detail]
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |
| `<partitionFQDN>` | DNS アプリケーションディレクトリパーティションの FQDN。 |
| /detail | アプリケーションディレクトリパーティションに関するすべての情報を一覧表示します。 |

## <a name="dnscmd-enlistdirectorypartition-command"></a>dnscmd/enlistdirectorypartition コマンド

指定されたディレクトリパーティションのレプリカセットに DNS サーバーを追加します。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /enlistdirectorypartition <partitionFQDN>
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |
| `<partitionFQDN>` | DNS アプリケーションディレクトリパーティションの FQDN。 |

## <a name="dnscmd-enumdirectorypartitions-command"></a>dnscmd/enumdirectorypartitions コマンド

指定されたサーバーの DNS アプリケーションディレクトリパーティションを一覧表示します。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /enumdirectorypartitions [/custom]
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |
| /カスタム | ユーザーが作成したディレクトリパーティションのみを一覧表示します。 |

## <a name="dnscmd-enumrecords-command"></a>dnscmd/enumrecords コマンド

DNS ゾーン内の指定したノードのリソースレコードを一覧表示します。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /enumrecords <zonename> <nodename> [/type <rrtype> <rrdata>] [/authority] [/glue] [/additional] [/node | /child | /startchild<childname>] [/continue | /detail]
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |
| /enumrecords | 指定されたゾーンのリソースレコードを一覧表示します。 |
| `<zonename>` | リソースレコードが属しているゾーンの名前を指定します。 |
| `<nodename>` | リソースレコードのノードの名前を指定します。 |
| `[/type <rrtype> <rrdata>]` | 表示するリソースレコードの種類と、想定されるデータの種類を指定します。 次の値を受け入れます。<ul><li>`<rrtype>`-一覧表示するリソースレコードの種類を指定します。</li><li>`<rrdata>`-予想されるレコードの種類を指定します。</li></ul> |
| /機関 | 権限のあるデータが含まれます。 |
| /グルー | グルーデータを含みます。 |
| /追加 | 一覧にあるリソースレコードに関するすべての追加情報が含まれます。 |
| /node:( | 指定されたノードのリソースレコードのみを一覧表示します。 |
| /child | 指定された子ドメインのリソースレコードのみを一覧表示します。 |
| /スタート子`<childname>` | 指定された子ドメインのリストを開始します。 |
| 続行/ | リソースレコードとその種類およびデータのみを一覧表示します。 |
| /detail | リソースレコードに関するすべての情報を一覧表示します。 |

#### <a name="example"></a>例

```
dnscmd /enumrecords test.contoso.com test /additional
```

## <a name="dnscmd-enumzones-command"></a>dnscmd/enumzones コマンド

指定した DNS サーバー上に存在するゾーンを一覧表示します。 **Enumzones**パラメーターは、ゾーンの一覧のフィルターとして機能します。 フィルターが指定されていない場合は、ゾーンの完全な一覧が返されます。 フィルターを指定すると、返されたゾーンの一覧には、そのフィルターの条件を満たすゾーンだけが含まれます。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /enumzones [/primary | /secondary | /forwarder | /stub | /cache | /auto-created] [/forward | /reverse | /ds | /file] [/domaindirectorypartition | /forestdirectorypartition | /customdirectorypartition | /legacydirectorypartition | /directorypartition <partitionFQDN>]
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |
| /primary | 標準プライマリゾーンまたは active directory 統合ゾーンのいずれかであるすべてのゾーンを一覧表示します。 |
| /secondary | すべての標準セカンダリゾーンを一覧表示します。 |
| /フォワーダー | 未解決のクエリを別の DNS サーバーに転送するゾーンを一覧表示します。 |
| /stub | すべてのスタブゾーンを一覧表示します。 |
| /cache | キャッシュに読み込まれているゾーンのみを一覧表示します。 |
| /自動作成済み] | DNS サーバーのインストール中に自動的に作成されたゾーンを一覧表示します。 |
| /転送 | 前方参照ゾーンの一覧を表示します。 |
| /反転 | 逆引き参照ゾーンの一覧を表示します。 |
| /ds | Active directory 統合ゾーンの一覧を表示します。 |
| /file | ファイルによってバックアップされているゾーンを一覧表示します。 |
| /domaindirectorypartition | ドメインディレクトリパーティションに格納されているゾーンを一覧表示します。 |
| /forestdirectorypartition | フォレストの DNS アプリケーションディレクトリパーティションに格納されているゾーンを一覧表示します。 |
| /customdirectorypartition | ユーザー定義のアプリケーションディレクトリパーティションに格納されているすべてのゾーンを一覧表示します。 |
| /legacydirectorypartition | ドメインディレクトリパーティションに格納されているすべてのゾーンを一覧表示します。 |
| /directorypartition`<partitionFQDN>` | 指定されたディレクトリパーティションに格納されているすべてのゾーンを一覧表示します。 |

#### <a name="examples"></a>例

- [例 2: DNS サーバーのゾーンの完全な一覧を表示する](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)#example-2-display-a-complete-list-of-zones-on-a-dns-server)

- [例 3: DNS サーバーでより自動作成ゾーンの一覧を表示する](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)#example-3-display-a-list-of-autocreated-zones-on-a-dns-server)

## <a name="dnscmd-exportsettings-command"></a>dnscmd/exportsettings コマンド

DNS サーバーの構成の詳細を一覧表示するテキストファイルを作成します。 このテキストファイルの名前は*Dnssettings .txt*です。 サーバーのディレクトリに配置され `%systemroot%\system32\dns` ます。 **Dnscmd/exportsettings**によって作成されたファイル内の情報を使用して、構成の問題のトラブルシューティングを行ったり、複数のサーバーが同じように構成されていることを確認したりできます。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /exportsettings
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |

## <a name="dnscmd-info-command"></a>dnscmd/info コマンド

指定されたサーバーのレジストリの DNS セクションの設定を表示 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DNS\Parameters` します。 ゾーンレベルのレジストリ設定を表示するには、コマンドを使用し `dnscmd zoneinfo` ます。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /info [<settings>]
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |
| `<settings>` | **Info**コマンドによって返される設定は、個別に指定できます。 設定が指定されていない場合は、共通設定のレポートが返されます。 |

#### <a name="example"></a>例

- [例 4: DNS サーバーから IsSlave 設定を表示する](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)#example-4-display-the-isslave-setting-from-a-dns-server)

- [例 5: DNS サーバーから RecursionTimeout 設定を表示する](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)#example-5-display-the-recursiontimeout-setting-from-a-dns-server)

## <a name="dnscmd-ipvalidate-command"></a>dnscmd/ipvalidate コマンド

IP アドレスが、機能している DNS サーバーを識別するか、DNS サーバーが特定のゾーンのフォワーダー、ルートヒントサーバー、またはマスターサーバーとして機能するかどうかをテストします。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /ipvalidate <context> [<zonename>] [[<IPaddress>]]
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |
| `<context>` | 実行するテストの種類を指定します。 次のいずれかのテストを指定できます。<ul><li>**/dnsservers** -指定したアドレスを持つコンピューターが DNS サーバーで動作しているかどうかをテストします。</li><li>**/フォワーダー** -指定したアドレスがフォワーダーとして機能できる DNS サーバーを識別することをテストします。</li><li>**/roothints** -指定したアドレスがルートヒントネームサーバーとして機能する DNS サーバーを識別することをテストします。</li><li>**/zonemasters** -指定したアドレスが、*ゾーンゾーン*のマスターサーバーである DNS サーバーを識別することをテストします。 |
| `<zonename>` | ゾーンを識別します。 このパラメーターを **/zonemasters**パラメーターと共に使用します。 |
| `<IPaddress>` | コマンドがテストする IP アドレスを指定します。 |

#### <a name="examples"></a>例

```
nscmd dnssvr1.contoso.com /ipvalidate /dnsservers 10.0.0.1 10.0.0.2
dnscmd dnssvr1.contoso.com /ipvalidate /zonemasters corp.contoso.com 10.0.0.2
```

## <a name="dnscmd-nodedelete-command"></a>dnscmd/nodedelete コマンド

指定されたホストのすべてのレコードを削除します。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /nodedelete <zonename> <nodename> [/tree] [/f]
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |
| `<zonename>` | ゾーンの名前を指定します。 |
| `<nodename>` | 削除するノードのホスト名を指定します。 |
| /ツリー | すべての子レコードを削除します。 |
| /f | 確認を求めずにコマンドを実行します。 |

#### <a name="example"></a>例

[例 6: ノードからレコードを削除する](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)#example-6-delete-the-records-from-a-node)

## <a name="dnscmd-recordadd-command"></a>dnscmd/recordadd コマンド

DNS サーバーの指定したゾーンにレコードを追加します。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /recordadd <zonename> <nodename> <rrtype> <rrdata>
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |
| `<zonename>` | レコードが存在するゾーンを指定します。 |
| `<nodename>` | ゾーン内の特定のノードを指定します。 |
| `<rrtype>` | 追加するレコードの種類を指定します。 |
| `<rrdata>` | 予想されるデータの種類を指定します。 |

> [!NOTE]
> レコードを追加した後は、正しいデータ型とデータ形式を使用していることを確認してください。 リソースレコードの種類と適切なデータの種類の一覧については、「 [Dnscmd の例](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10))」を参照してください。

#### <a name="examples"></a>例

```
dnscmd dnssvr1.contoso.com /recordadd test A 10.0.0.5
dnscmd /recordadd test.contoso.com test MX 10 mailserver.test.contoso.com
```

## <a name="dnscmd-recorddelete-command"></a>dnscmd/recorddelete コマンド

指定されたゾーンにリソースレコードを削除します。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /recorddelete <zonename> <nodename> <rrtype> <rrdata> [/f]
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |
| `<zonename>` | リソースレコードが存在するゾーンを指定します。 |
| `<nodename>` | ホストの名前を指定します。 |
| `<rrtype>` | 削除するリソースレコードの種類を指定します。 |
| `<rrdata>` | 予想されるデータの種類を指定します。 |
| /f | 確認を求めずにコマンドを実行します。 ノードには複数のリソースレコードを含めることができるため、このコマンドでは、削除するリソースレコードの種類について非常に固有の情報を要求する必要があります。 データ型を指定し、リソースレコードデータの種類を指定しない場合、指定したデータ型のすべてのレコードが指定したノードで削除されます。 |

#### <a name="examples"></a>例

```
dnscmd /recorddelete test.contoso.com test MX 10 mailserver.test.contoso.com
```

## <a name="dnscmd-resetforwarders-command"></a>dnscmd/resetforwarders コマンド

DNS サーバーがローカルで解決できない場合に dns サーバーが DNS クエリを転送する IP アドレスを選択またはリセットします。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /resetforwarders <IPaddress> [,<IPaddress>]...][/timeout <timeout>] [/slave | /noslave]
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |
| `<IPaddress>` | DNS サーバーが未解決のクエリを転送する IP アドレスを一覧表示します。 |
| /timeout`<timeout>` | DNS サーバーがフォワーダーからの応答を待機する秒数を設定します。 既定では、この値は5秒です。 |
| /slave | フォワーダーがクエリの解決に失敗した場合に、DNS サーバーが独自の反復クエリを実行しないようにします。 |
| /noslave | フォワーダーがクエリの解決に失敗した場合に、DNS サーバーが独自の反復クエリを実行できるようにします。 これが既定の設定です。 |
| /f | 確認を求めずにコマンドを実行します。 ノードには複数のリソースレコードを含めることができるため、このコマンドでは、削除するリソースレコードの種類について非常に固有の情報を要求する必要があります。 データ型を指定し、リソースレコードデータの種類を指定しない場合、指定したデータ型のすべてのレコードが指定したノードで削除されます。 |

##### <a name="remarks"></a>解説

- 既定では、クエリを解決できない場合、DNS サーバーは反復クエリを実行します。

- **Resetforwarders**コマンドを使用して IP アドレスを設定すると、dns サーバーは、指定された ip アドレスで dns サーバーに対して再帰的なクエリを実行します。 フォワーダーがクエリを解決しない場合、DNS サーバーは独自の反復クエリを実行できます。

- **/スレーブ**パラメーターを使用すると、DNS サーバーは独自の反復クエリを実行しません。 つまり、DNS サーバーは、一覧内の DNS サーバーに対してのみ未解決のクエリを転送します。フォワーダーが解決しない場合、反復クエリは試行されません。 1つの IP アドレスを DNS サーバーのフォワーダーとして設定する方が効率的です。 ネットワーク内の内部サーバーに対して**resetforwarders**コマンドを使用すると、外部接続がある1つの DNS サーバーに未解決のクエリを転送できます。

- フォワーダーの IP アドレスを2回一覧表示すると、DNS サーバーはそのサーバーに2回転送を試みます。

#### <a name="examples"></a>例

```
dnscmd dnssvr1.contoso.com /resetforwarders 10.0.0.1 /timeout 7 /slave
dnscmd dnssvr1.contoso.com /resetforwarders /noslave
```

## <a name="dnscmd-resetlistenaddresses-command"></a>dnscmd/resetlistenaddresses コマンド

DNS クライアント要求をリッスンするサーバーの IP アドレスを指定します。 既定では、DNS サーバー上のすべての IP アドレスは、クライアントの DNS 要求をリッスンします。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /resetlistenaddresses <listenaddress>
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |
| `<listenaddress>` | Dns クライアント要求をリッスンする DNS サーバーの IP アドレスを指定します。 リッスンアドレスが指定されていない場合、サーバー上のすべての IP アドレスがクライアント要求をリッスンします。 |

#### <a name="examples"></a>例

```
dnscmd dnssvr1.contoso.com /resetlistenaddresses 10.0.0.1
```

## <a name="dnscmd-startscavenging-command"></a>dnscmd/start清掃コマンド

指定した DNS サーバーで古いリソースレコードをすぐに検索するように DNS サーバーに指示します。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /startscavenging
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |

##### <a name="remarks"></a>解説

- このコマンドが正常に完了すると、すぐに清掃が開始されます。 清掃が失敗した場合、警告メッセージは表示されません。

- 清掃を開始するコマンドは正常に完了したように見えますが、次の前提条件を満たしていないと清掃は開始されません。

    - サーバーとゾーンの両方で清掃が有効になっています。

    - ゾーンが開始されます。

    - リソースレコードにはタイムスタンプがあります。

- サーバーの清掃を有効にする方法の詳細については、「 **/config** 」の「**サーバーレベルの構文**」の**scavenginginterval**パラメーターを参照してください。

- ゾーンの清掃を有効にする方法の詳細については、「 **/config** 」セクションの「**ゾーンレベルの構文**」にある**aging**パラメーターを参照してください。

- 一時停止しているゾーンを再起動する方法の詳細については、この記事の**zoneresume**パラメーターを参照してください。

- タイムスタンプのリソースレコードを確認する方法の詳細については、この記事の「 **ageallrecords**パラメーター」を参照してください。

#### <a name="examples"></a>例

```
dnscmd dnssvr1.contoso.com /startscavenging
```

## <a name="dnscmd-statistics-command"></a>dnscmd/statistics コマンド

指定した DNS サーバーのデータを表示またはクリアします。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /statistics [<statid>] [/clear]
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |
| `<statid>` | 表示する統計または統計の組み合わせを指定します。 **Statistics**コマンドを実行すると、DNS サーバーの開始時または再開時に開始されるカウンターが表示されます。 Id 番号は、統計情報を識別するために使用されます。 統計 ID 番号が指定されていない場合は、すべての統計が表示されます。 指定できる数値と、表示される対応する統計情報を次に示します。<ul><li>**00000001** -時間</li><li>**00000002** -クエリ</li><li>**00000004** -Query2</li><li>**00000008** -再帰</li><li>**00000010** -マスター</li><li>**00000020** -セカンダリ</li><li>**00000040** -WINS</li><li>**00000100** -更新</li><li>**00000200** -SkwanSec</li><li>**00000400** -Ds</li><li>**00010000** -メモリ</li><li>**00100000** -packetmem</li><li>**00040000** -Dbase</li><li>**00080000** -レコード</li><li>**00200000** -nbstatmem</li><li>**/clear** -指定された統計カウンターを0にリセットします。</li></ul> |

#### <a name="examples"></a>例

- [例 7:](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)#example-7-display-time-statistics-for-a-dns-server)

- [例 8: DNS サーバーの NbstatMem の統計情報を表示する](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)#example-8-display-nbstatmem-statistics-for-a-dns-server)

## <a name="dnscmd-unenlistdirectorypartition-command"></a>dnscmd/unenlistdirectorypartition コマンド

指定されたディレクトリパーティションのレプリカセットから DNS サーバーを削除します。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /unenlistdirectorypartition <partitionFQDN>
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |
| `<partitionFQDN>` | 削除される DNS アプリケーションディレクトリパーティションの FQDN。 |

## <a name="dnscmd-writebackfiles-command"></a>dnscmd/writebackfiles コマンド

DNS サーバーのメモリが変更されていないかどうかを確認し、永続ストレージに書き込みます。 **Writebackfiles**コマンドは、すべてのダーティゾーンまたは指定されたゾーンを更新します。 永続ストレージにまだ書き込まれていないメモリの変更がある場合、ゾーンはダーティになります。 これは、すべてのゾーンをチェックするサーバーレベルの操作です。 この操作で1つのゾーンを指定することも、ゾーンの**書き戻し**操作を使用することもできます。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /writebackfiles <zonename>
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |
| `<zonename>` | 更新するゾーンの名前を指定します。 |

#### <a name="examples"></a>例

```
dnscmd dnssvr1.contoso.com /writebackfiles
```

## <a name="dnscmd-zoneadd-command"></a>dnscmd/zoneadd コマンド

DNS サーバーにゾーンを追加します。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /zoneadd <zonename> <zonetype> [/dp <FQDN> | {/domain | enterprise | legacy}]
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |
| `<zonename>` | ゾーンの名前を指定します。 |
| `<zonetype>` | 作成するゾーンの種類を指定します。 **/フォワーダー**または **/dsforwarder**のゾーンの種類を指定すると、条件付きの転送を実行するゾーンが作成されます。 各ゾーンの種類には、次のような必須パラメーターがあります。<ul><li>**/dsprimary** -active directory 統合ゾーンを作成します。</li><li>**/プライマリ `<filename>` の自動//**-標準のプライマリゾーンを作成し、ゾーン情報を格納するファイルの名前を指定します。</li><li>**/セカンダリ `<masterIPaddress> [<masterIPaddress>...]` **-標準のセカンダリゾーンを作成します。</li><li>スタブの自動作成-ファイルによってサポートされるスタブゾーンを作成します。 ** `<masterIPaddress> [<masterIPaddress>...]` `<filename>` **</li><li>**/dsstub `<masterIPaddress> [<masterIPaddress>...]` **-Active directory 統合スタブゾーンを作成します。</li><li>**/フォワーダー `<masterIPaddress> [<masterIPaddress>]` ... `<filename>` **サーバー 1: 未解決のクエリを別の DNS サーバーに転送することを指定します。</li><li>**/dsforwarder** -作成された active directory 統合ゾーンが、未解決のクエリを別の DNS サーバーに転送することを指定します。</li></ul> |
| `<FQDN>` | ディレクトリパーティションの FQDN を指定します。 |
| /domain | ドメインディレクトリパーティションにゾーンを格納します。 |
| /エンタープライズ | は、エンタープライズディレクトリパーティションにゾーンを格納します。 |
| /レガシ | 従来のディレクトリパーティションにゾーンを格納します。 |

#### <a name="examples"></a>例

```
dnscmd dnssvr1.contoso.com /zoneadd test.contoso.com /dsprimary
dnscmd dnssvr1.contoso.com /zoneadd secondtest.contoso.com /secondary 10.0.0.2
```

## <a name="dnscmd-zonechangedirectorypartition-command"></a>dnscmd/zonechangedirectorypartition コマンド

指定されたゾーンが存在するディレクトリパーティションを変更します。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /zonechangedirectorypartition <zonename> {[<newpartitionname>] | [<zonetype>]}
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |
| `<zonename>` | ゾーンが存在する現在のディレクトリパーティションの FQDN。 |
| `<newpartitionname>` | ゾーンの移動先となるディレクトリパーティションの FQDN。 |
| `<zonetype>` | ゾーンの移動先となるディレクトリパーティションの種類を指定します。 |
| /domain | ゾーンを組み込みのドメインディレクトリパーティションに移動します。 |
| /forest | ゾーンを組み込みのフォレストディレクトリパーティションに移動します。 |
| /レガシ | Active directory ドメインコントローラーの事前に作成されたディレクトリパーティションにゾーンを移動します。 これらのディレクトリパーティションは、ネイティブモードでは不要です。 |

## <a name="dnscmd-zonedelete-command"></a>dnscmd/zonedelete コマンド

指定されたゾーンを削除します。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /zonedelete <zonename> [/dsdel] [/f]
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |
| `<zonename>` | 削除するゾーンの名前を指定します。 |
| /dsdel | Azure Directory Domain Services (AD DS) からゾーンを削除します。 |
| /f | 確認を求めずにコマンドを実行します。 |

#### <a name="examples"></a>例

- [例 9: DNS サーバーからゾーンを削除する](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)#example-9-delete-a-zone-from-a-dns-server)

## <a name="dnscmd-zoneexport-command"></a>dnscmd/zoneexport コマンド

指定されたゾーンのリソースレコードを一覧表示するテキストファイルを作成します。 **ゾーンエクスポート**操作は、トラブルシューティングのために、active directory 統合ゾーンのリソースレコードのファイルを作成します。 既定では、このコマンドによって作成されるファイルは、既定ではディレクトリである DNS ディレクトリに配置され `%systemroot%/System32/Dns` ます。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /zoneexport <zonename> <zoneexportfile>
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |
| `<zonename>` | ゾーンの名前を指定します。 |
| `<zoneexportfile>` | 作成するファイルの名前を指定します。 |

#### <a name="examples"></a>例

- [例 10: ゾーンリソースレコードの一覧をファイルにエクスポートする](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)#example-10-export-zone-resource-records-list-to-a-file)

## <a name="dnscmd-zoneinfo"></a>dnscmd/zoneinfo

指定されたゾーンのレジストリのセクションの設定を表示します。`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DNS\Parameters\Zones\<zonename>`

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /zoneinfo <zonename> [<setting>]
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |
| `<zonename>` | ゾーンの名前を指定します。 |
| `<setting>` | **ゾーン情報**コマンドによって返される設定は、個別に指定できます。 設定を指定しない場合は、すべての設定が返されます。 |

##### <a name="remarks"></a>解説

- サーバーレベルのレジストリ設定を表示するには、 **/info**コマンドを使用します。

- このコマンドで表示できる設定の一覧については、 **/config**コマンドを参照してください。

#### <a name="examples"></a>例

- [例 11: レジストリから RefreshInterval 設定を表示する](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)#example-11-display-refreshinterval-setting-from-the-registry)

- [例 12: レジストリからエージング設定を表示する](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)#example-12-display-aging-setting-from-the-registry)

## <a name="dnscmd-zonepause-command"></a>dnscmd/zonepause コマンド

指定されたゾーンを一時停止し、クエリ要求を無視します。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /zonepause <zonename>
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |
| `<zonename>` | 一時停止するゾーンの名前を指定します。 |

##### <a name="remarks"></a>解説

- ゾーンを再開し、一時停止した後で使用できるようにするには、 **/zoneresume**コマンドを使用します。

#### <a name="examples"></a>例

```
dnscmd dnssvr1.contoso.com /zonepause test.contoso.com
```

## <a name="dnscmd-zoneprint-command"></a>dnscmd/zoneprint コマンド

ゾーン内のレコードを一覧表示します。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /zoneprint <zonename>
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |
| `<zonename>` | 一覧表示するゾーンの名前を指定します。 |







## <a name="dnscmd-zonerefresh-command"></a>dnscmd/zonerefresh コマンド

セカンダリ DNS ゾーンを強制的にマスタゾーンから更新します。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /zonerefresh <zonename>
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |
| `<zonename>` | 更新するゾーンの名前を指定します。 |

##### <a name="remarks"></a>解説

- **Zonerefresh**コマンドを実行すると、マスターサーバーの SOA (start of authority) リソースレコードのバージョン番号が強制的にチェックされます。 マスターサーバーのバージョン番号がセカンダリサーバーのバージョン番号よりも大きい場合は、セカンダリサーバーを更新するゾーン転送が開始されます。 バージョン番号が同じである場合、ゾーン転送は行われません。

- 強制チェックは、既定で15分ごとに実行されます。 既定値を変更するには、コマンドを使用し `dnscmd config refreshinterval` ます。

#### <a name="examples"></a>例

```
dnscmd dnssvr1.contoso.com /zonerefresh test.contoso.com
```

## <a name="dnscmd-zonereload-command"></a>dnscmd/zonereload コマンド

ソースからゾーン情報をコピーします。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /zonereload <zonename>
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |
| `<zonename>` | 再読み込みするゾーンの名前を指定します。 |

##### <a name="remarks"></a>解説

- ゾーンが active directory と統合されている場合は、Active Directory Domain Services (AD DS) から再読み込みされます。

- ゾーンが標準のファイルベースのゾーンである場合は、ファイルから再読み込みされます。

#### <a name="examples"></a>例

```
dnscmd dnssvr1.contoso.com /zonereload test.contoso.com
```

## <a name="dnscmd-zoneresetmasters-command"></a>dnscmd/zoneresetmasters コマンド

ゾーン転送情報を提供するマスタサーバーの IP アドレスをセカンダリゾーンにリセットします。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /zoneresetmasters <zonename> [/local] [<IPaddress> [<IPaddress>]...]
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |
| `<zonename>` | リセットするゾーンの名前を指定します。 |
| /local | ローカルのマスターリストを設定します。 このパラメーターは、active directory 統合ゾーンで使用されます。 |
| `<IPaddress>` | セカンダリゾーンのマスタサーバーの IP アドレス。 |

##### <a name="remarks"></a>解説

- この値は、最初にセカンダリゾーンが作成されるときに設定されます。 セカンダリサーバーで、**ゾーンの eresetmasters**コマンドを使用します。 この値は、マスター DNS サーバーで設定されている場合は効果がありません。

#### <a name="examples"></a>例

```
dnscmd dnssvr1.contoso.com /zoneresetmasters test.contoso.com 10.0.0.1
dnscmd dnssvr1.contoso.com /zoneresetmasters test.contoso.com /local
```

## <a name="dnscmd-zoneresetscavengeservers-command"></a>dnscmd/zoneresetscavengeservers コマンド

指定されたゾーンを清掃できるサーバーの IP アドレスを変更します。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /zoneresetscavengeservers <zonename> [/local] [<IPaddress> [<IPaddress>]...]
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |
| `<zonename>` | 清掃するゾーンを指定します。 |
| /local | ローカルのマスターリストを設定します。 このパラメーターは、active directory 統合ゾーンで使用されます。 |
| `<IPaddress>` | 清掃を実行できるサーバーの IP アドレスが一覧表示されます。 このパラメーターを省略した場合、このゾーンをホストするすべてのサーバーで清掃を実行できます。 |

##### <a name="remarks"></a>解説

- 既定では、ゾーンをホストするすべてのサーバーがそのゾーンを清掃できます。

- ゾーンが複数の DNS サーバーでホストされている場合、このコマンドを使用して、ゾーンを清掃する回数を減らすことができます。

- このコマンドの影響を受ける DNS サーバーとゾーンで清掃が有効になっている必要があります。

#### <a name="examples"></a>例

```
dnscmd dnssvr1.contoso.com /zoneresetscavengeservers test.contoso.com 10.0.0.1 10.0.0.2
```

## <a name="dnscmd-zoneresetsecondaries-command"></a>dnscmd/zoneresetsecondaries コマンド

ゾーン転送が要求されたときにマスターサーバーが応答するセカンダリサーバーの IP アドレスの一覧を指定します。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /zoneresetsecondaries <zonename> {/noxfr | /nonsecure | /securens | /securelist <securityIPaddresses>} {/nonotify | /notify | /notifylist <notifyIPaddresses>}
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |
| `<zonename>` | セカンダリサーバーをリセットするゾーンの名前を指定します。 |
| /local | ローカルのマスターリストを設定します。 このパラメーターは、active directory 統合ゾーンで使用されます。 |
| /noxfr | ゾーン転送を許可しないことを指定します。 |
| /非セキュリティ | すべてのゾーン転送要求を許可することを指定します。 |
| /セキュリティー | ゾーンのネームサーバー (NS) リソースレコードに一覧表示されているサーバーにのみ転送を許可することを指定します。 |
| /securelist | ゾーン転送をサーバーの一覧のみに許可することを指定します。 このパラメーターの後には、マスターサーバーが使用する IP アドレスまたはアドレスを指定する必要があります。 |
| `<securityIPaddresses>` | マスターサーバーからゾーン転送を受信する IP アドレスを一覧表示します。 このパラメーターは、 **/dns リスト**パラメーターと共にのみ使用されます。 |
| /nonotify | 変更通知がセカンダリサーバーに送信されないことを指定します。 |
| /通知 | 変更通知をすべてのセカンダリサーバーに送信することを指定します。 |
| /notifylist | 変更通知をサーバーの一覧のみに送信することを指定します。 このコマンドの後には、マスターサーバーが使用する IP アドレスまたはアドレスを指定する必要があります。 |
| `<notifyIPaddresses>` | 変更通知の送信先となるセカンダリサーバーの IP アドレスまたはアドレスを指定します。 この一覧は、 **/notifylist**パラメーターと共にのみ使用されます。 |

##### <a name="remarks"></a>解説

- マスターサーバーでゾーンの**eresetsecondary**コマンドを使用して、セカンダリサーバーからのゾーン転送要求にどのように応答するかを指定します。

#### <a name="examples"></a>例

```
dnscmd dnssvr1.contoso.com /zoneresetsecondaries test.contoso.com /noxfr /nonotify
dnscmd dnssvr1.contoso.com /zoneresetsecondaries test.contoso.com /securelist 11.0.0.2
```

## <a name="dnscmd-zoneresettype-command"></a>dnscmd/zoneresettype コマンド

ゾーンの種類を変更します。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /zoneresettype <zonename> <zonetype> [/overwrite_mem | /overwrite_ds]
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |
| `<zonename>` | 型が変更されるゾーンを識別します。 |
| `<zonetype>` | 作成するゾーンの種類を指定します。 各型には、次のような必要なパラメーターがあります。<ul><li>**/dsprimary** -active directory 統合ゾーンを作成します。</li><li>**/プライマリ `<filename>` の自動//**-標準のプライマリゾーンを作成します。</li><li>**/セカンダリ `<masterIPaddress> [,<masterIPaddress>...]` **-標準のセカンダリゾーンを作成します。</li><li>スタブの自動作成-ファイルによってサポートされるスタブゾーンを作成します。 ** `<masterIPaddress>[,<masterIPaddress>...]` `<filename>` **</li><li>**/dsstub `<masterIPaddress>[,<masterIPaddress>...]` **-Active directory 統合スタブゾーンを作成します。</li><li>**/フォワーダー `<masterIPaddress[,<masterIPaddress>]` ... `<filename>` **サーバー 1: 未解決のクエリを別の DNS サーバーに転送することを指定します。</li><li>**/dsforwarder** -作成された active directory 統合ゾーンが、未解決のクエリを別の DNS サーバーに転送することを指定します。</li></ul> |
| /overwrite_mem | AD DS のデータの DNS データを上書きします。 |
| /overwrite_ds | AD DS 内の既存のデータを上書きします。 |

##### <a name="remarks"></a>解説

- ゾーンの種類を **/dsforwarder**として設定すると、条件付きの転送を実行するゾーンが作成されます。

#### <a name="examples"></a>例

```
dnscmd dnssvr1.contoso.com /zoneresettype test.contoso.com /primary /file test.contoso.com.dns
dnscmd dnssvr1.contoso.com /zoneresettype second.contoso.com /secondary 10.0.0.2
```

## <a name="dnscmd-zoneresume-command"></a>dnscmd/zoneresume コマンド

以前に一時停止していた指定されたゾーンを開始します。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /zoneresume <zonename>
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |
| `<zonename>` | 再開するゾーンの名前を指定します。 |

##### <a name="remarks"></a>解説

- この操作を使用すると、 **/zonepause**操作から再開できます。

#### <a name="examples"></a>例

```
dnscmd dnssvr1.contoso.com /zoneresume test.contoso.com
```

## <a name="dnscmd-zoneupdatefromds-command"></a>dnscmd/zoneupdatefromds コマンド

指定された active directory 統合ゾーンを AD DS から更新します。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /zoneupdatefromds <zonename>
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |
| `<zonename>` | 更新するゾーンの名前を指定します。 |

##### <a name="remarks"></a>解説

- Active directory 統合ゾーンは、既定で5分ごとにこの更新を実行します。 このパラメーターを変更するには、コマンドを使用し `dnscmd config dspollinginterval` ます。

#### <a name="examples"></a>例

```
dnscmd dnssvr1.contoso.com /zoneupdatefromds
```

## <a name="dnscmd-zonewriteback-command"></a>dnscmd/zonewriteback コマンド

指定されたゾーンに関連する変更について DNS サーバーのメモリを確認し、永続ストレージに書き込みます。

### <a name="syntax"></a>構文

```
dnscmd [<servername>] /zonewriteback <zonename>
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `<servername>` | 管理する DNS サーバーを指定します。 IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカルサーバーが使用されます。 |
| `<zonename>` | 更新するゾーンの名前を指定します。 |

##### <a name="remarks"></a>解説

- これはゾーンレベルの操作です。 **/Writebackfiles**操作を使用して、DNS サーバー上のすべてのゾーンを更新できます。

#### <a name="examples"></a>例

```
dnscmd dnssvr1.contoso.com /zonewriteback test.contoso.com
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)