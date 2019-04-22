---
title: Dnscmd
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e7f31cb5-a426-4e25-b714-88712b8defd5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 39478e9b7dd8e8c69ed07f5d431486a7ed96b9cb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59815503"
---
# <a name="dnscmd"></a>Dnscmd

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

DNS サーバーを管理するためのコマンド ライン インターフェイス。 このユーティリティは、スクリプト日常的な DNS の管理タスクを自動化するために、またはネットワーク上に新しい DNS サーバーの単純な無人セットアップと構成を実行するバッチ ファイルで役立ちます。  
## <a name="syntax"></a>構文  
```  
dnscmd <ServerName> <command> [<command parameters>]  
```  
## <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|<ServerName>|リモートまたはローカルの DNS サーバーの IP アドレスまたはホスト名。|  
## <a name="commands"></a>コマンド  
|コマンド|説明|  
|------|--------|  
|[dnscmd /ageallrecords](#BKMK_1)|ゾーンまたはノードのすべてのタイムスタンプには、現在の時刻を設定します。|  
|[dnscmd /clearcache](#BKMK_2)|DNS サーバーのキャッシュをクリアします。|  
|[dnscmd /config](#BKMK_3)|DNS サーバーまたはゾーンの構成をリセットします。|  
|[dnscmd /createbuiltindirectorypartitions](#BKMK_4)|組み込みの DNS アプリケーション ディレクトリ パーティションを作成します。|  
|[dnscmd /createdirectorypartition](#BKMK_5)|DNS アプリケーション ディレクトリ パーティションを作成します。|  
|[dnscmd /deletedirectorypartition](#BKMK_6)|DNS アプリケーション ディレクトリ パーティションを削除します。|  
|[dnscmd /directorypartitioninfo](#BKMK_7)|DNS アプリケーション ディレクトリ パーティションに関する情報を一覧表示します。|  
|[dnscmd /enlistdirectorypartition](#BKMK_8)|DNS アプリケーション ディレクトリ パーティションのレプリケーション セットを DNS サーバーを追加します。|  
|[dnscmd /enumdirectorypartitions](#BKMK_9)|サーバーの DNS アプリケーション ディレクトリ パーティションを一覧表示します。|  
|[dnscmd /enumrecords](#BKMK_10)|ゾーン内のリソース レコードを一覧表示します。|  
|[dnscmd/enumzones](#BKMK_11)|指定されたサーバーでホストされているゾーンを一覧表示します。|  
|[dnscmd /exportsettings](#BKMK_25a)|サーバーの構成情報をテキスト ファイルに書き込みます。|  
|[dnscmd /info](#BKMK_12)|サーバーの情報を取得します。|  
|[dnscmd /ipvalidate](#BKMK_29a)|リモート DNS サーバーを検証します。|  
|[dnscmd /nodedelete](#BKMK_13)|ゾーン内のノードのすべてのレコードを削除します。|  
|[dnscmd /recordadd](#BKMK_14)|リソース レコードをゾーンに追加します。|  
|[dnscmd /recorddelete](#BKMK_15)|リソース レコードをゾーンから削除します。|  
|[dnscmd /resetforwarders](#BKMK_16)|再帰クエリを転送する DNS サーバーを設定します。|  
|[dnscmd /resetlistenaddresses](#BKMK_17)|DNS 要求を処理するサーバーの IP アドレスを設定します。|  
|[dnscmd /startscavenging](#BKMK_18)|サーバーが清掃を開始します。|  
|[dnscmd /statistics](#BKMK_19)|クエリまたはサーバーの統計情報データをクリアします。|  
|[dnscmd /unenlistdirectorypartition](#BKMK_20)|DNS アプリケーション ディレクトリ パーティションのレプリケーション セットから DNS サーバーを削除します。|  
|[dnscmd /writebackfiles](#BKMK_21)|すべてのゾーンまたはルート ヒントのデータをファイルに保存します。|  
|[dnscmd /zoneadd](#BKMK_22)|DNS サーバーに新しいゾーンを作成します。|  
|[dnscmd /zonechangedirectorypartition](#BKMK_23)|ゾーンが存在するディレクトリ パーティションを変更します。|  
|[dnscmd /zonedelete](#BKMK_24)|DNS サーバーからゾーンを削除します。|  
|[dnscmd /zoneexport](#BKMK_25)|ゾーンのリソース レコードをテキスト ファイルに書き込みます。|  
|[dnscmd /zoneinfo](#BKMK_26)|ゾーン情報が表示されます。|  
|[dnscmd/zonepause](#BKMK_27)|ゾーンを一時停止します。|  
|[dnscmd /zoneprint](#BKMK_28)|ゾーン内のすべてのレコードを表示します。|  
|[dnscmd /zonerefresh](#BKMK_30)|マスター ゾーンのセカンダリ ゾーンの更新を強制します。|  
|[dnscmd /zonereload](#BKMK_31)|そのデータベースからのゾーンを再読み込みします。|  
|[dnscmd /zoneresetmasters](#BKMK_32)|セカンダリ ゾーンのゾーン転送の情報を提供するマスター サーバーを変更します。|  
|[dnscmd /zoneresetscavengeservers](#BKMK_33)|ゾーンの清掃を行うサーバーを変更します。|  
|[dnscmd /zoneresetsecondaries](#BKMK_34)|ゾーンのセカンダリ情報をリセットします。|  
|[dnscmd /zoneresettype](#BKMK_29)|ゾーンの種類を変更します。|  
|[dnscmd /zoneresume](#BKMK_35)|ゾーンを再開します。|  
|[dnscmd /zoneupdatefromds](#BKMK_36)|Active directory Domain Services (AD DS) からデータを active directory 統合ゾーンを更新します。|  
|[dnscmd /zonewriteback](#BKMK_37)|ゾーン データをファイルに保存します。|  
### <a name="BKMK_1"></a>dnscmd /ageallrecords  
指定されたゾーンまたは DNS サーバー上のノードでのリソース レコードのタイムスタンプには、現在の時刻を設定します。  
#### <a name="syntax"></a>構文  
```  
dnscmd [<ServerName>] /ageallrecords <ZoneName>[<NodeName>] | [/tree]|[/f]  
```  
#### <a name="parameters"></a>パラメーター  
<ServerName>  
管理者が管理対象 DNS サーバーを指定します。 は、IP アドレス、完全修飾ドメイン名 (FQDN)、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
<ZoneName>  
ゾーンの FQDN を指定します。  
<NodeName>  
ゾーンでは、特定のノードまたはサブツリーを指定します。 *NodeName*ノードまたはサブツリーを次を使用してゾーンを指定します。  
-   @ ルート ゾーンまたは FQDN  
-   (末尾のピリオド (.) の名前) のノードの FQDN  
-   ゾーンのルートを基準とした名前の 1 つのラベル  
/tree  
すべての子ノードもタイムスタンプが表示されることを指定します。  
/f  
確認を求めずにコマンドを実行します。  
#### <a name="remarks"></a>注釈  
-   **Ageallrecords**コマンドは、旧バージョンとの間の互換性 DNS の現在のバージョンと以前のリリースの DNS をエージングと清掃のサポートされていませんでした。 現在の時刻のタイムスタンプ、タイムスタンプがないリソース レコードに追加したり、リソース レコードのタイムスタンプが、現在の時刻を設定します。  
-   レコードがタイムスタンプがない場合、レコードの清掃は発生しません。 ネーム サーバー (NS) リソース レコード、authority (SOA) リソース レコードを開始し、Windows インターネット ネーム サービス (WINS) リソース レコードの清掃のプロセスには含まれません、タイムスタンプがない場合でも、 **ageallrecords**コマンドを実行します。  
-   このコマンドは、DNS サーバーとゾーンの清掃が有効にしない限り失敗します。 ゾーンの清掃を有効にする方法については、次を参照してください。、**エージング**でゾーン レベルの構文の下のパラメーター、 [config](#BKMK_3)コマンド。  
-   DNS リソース レコードにタイムスタンプを追加では、Windows 2000、Windows XP、または Windows Server 2003 以外のオペレーティング システムで実行される DNS サーバーと互換性のないになります。 使用して追加したタイムスタンプ、 **ageallrecords**コマンドを元に戻すことはできません。  
-   指定されていない省略可能なパラメーターの場合は、指定したノードにあるすべてのリソース レコードが返されます。 少なくとも 1 つのオプションのパラメーターの値が指定されている場合**dnscmd**省略可能なパラメーターまたはパラメーターで指定されている値に対応するリソース レコードのみを列挙します。  
#### <a name="example"></a>例  
参照してください[例 1。リソース レコードにタイムスタンプを現在の時刻を設定](https://technet.microsoft.com/library/cc784399(v=ws.10).aspx)します。  
### <a name="BKMK_2"></a>dnscmd /clearcache  
指定された DNS サーバー上のリソース レコードの DNS キャッシュのメモリをクリアします。  
#### <a name="syntax"></a>構文  
```  
dnscmd [<ServerName>] /clearcache  
```  
#### <a name="parameters"></a>パラメーター  
<ServerName>  
IP アドレス、FQDN、またはホスト名によって表されるを管理する DNS サーバーを指定します。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
#### <a name="sample-usage"></a>サンプルの使用法  
`dnscmd dnssvr1.contoso.com /clearcache`  
### <a name="BKMK_3"></a>dnscmd /config  
DNS サーバーと個別のゾーンのレジストリの値を変更します。 サーバー レベルの設定とゾーン レベルの設定を受け入れます。  
> [!CAUTION]  
> 代替手段があるない場合は、直接、レジストリを編集しないでください。 レジストリ エディターは、標準の保護をバイパスする、設定にパフォーマンスが低下することができます、システムの破損やでも Windows を再インストールする必要があります。 ほとんどのレジストリ設定は、コントロール パネルまたは Microsoft 管理コンソール (mmc) では、プログラムを使用して安全に変更できます。 レジストリを直接編集する必要がある場合は、最初にバックアップします。 詳細については、レジストリ エディターのヘルプを読み取ります。  
#### <a name="server-level-syntax"></a>サーバー レベルの構文  
```  
dnscmd [<ServerName>] /config <Parameter>  
```  
#### <a name="dnscmd-config"></a>dnscmd /config  
指定したサーバーの構成を変更します。  
#### <a name="parameters"></a>パラメーター  
<ServerName>  
DNS サーバーを管理することを計画しているを指定は、ローカル コンピューターの構文、IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
<Parameter>  
設定を指定し、オプションの値として。 パラメーターの値は、この構文を使用します。*パラメーター* [*値*]  
このセクションの残りの部分では、次のパラメーター値がについて説明します。  
-   **/addressanswerlimit**  
-   **/bindsecondaries**  
-   **/bootmethod**  
-   **/defaultagingstate**  
-   **/defaultnorefreshinterval**  
-   **/defaultrefreshinterval**  
-   **/disableautoreversezones**  
-   **/disablensrecordsautocreation**  
-   **/dspollinginterval**  
-   **/dstombstoneinterval**  
-   **/ednscachetimeout**  
-   **/enablednsprobes**  
-   **/enablednssec**  
-   **/enableglobalnamessupport**  
-   **/enableglobalqueryblocklist**  
-   **/eventloglevel**  
-   **/forwarddelegations**  
-   **/forwardingtimeout**  
-   **/globalnamesqueryorder**  
-   **/globalqueryblocklist**  
-   **/isslave**  
-   **/localnetpriority**  
-   **/logfilemaxsize**  
-   **/logfilepath**  
-   **/logipfilterlist**  
-   **/loglevel**  
-   **/maxcachesize**  
-   **/maxcachettl**  
-   **/namecheckflag**  
-   **/notcp**  
-   **/norecursion**  
-   **/recursionretry**  
-   **/recursiontimeout**  
-   **/roundrobin**  
-   **/rpcprotocol**  
-   **/scavenginginterval**  
-   **/secureresponses**  
-   **/sendport**  
-   **/strictfileparsing**  
-   **/updateoptions**  
-   **/writeauthorityns**  
-   **/xfrconnecttimeout**  
**/addressanswerlimit [0 | 5 月 28 日]**  
DNS サーバーは、クエリに対する応答で送信できるホスト レコードの最大数を指定します。 値がゼロ (0) を指定できますか、5 ~ 28 レコードの範囲を指定できます。 既定値は、ゼロ (0) です。  
**/bindsecondaries[0|1]**  
最大圧縮率と効率性を実現にするために、ゾーン転送の形式を変更します。 ただし、この形式では、以前のバージョンの Berkeley Internet Name Domain (BIND) と互換性がありません。  
**0**  
最大圧縮を使用します。 この形式は、4.9.4 のバインド バージョンと互換性があり、以降のみです。  
**1**  
Microsoft 以外の DNS サーバーには、メッセージごとに 1 つだけのリソース レコードを送信します。 この形式は 4.9.4 バインド前のバージョンとの互換性です。 これは、既定の設定です。  
**/bootmethod [0 | 1 | 2 | 3]。**  
DNS サーバーの構成情報の取得元となるソースを決定します。  
**0**  
構成情報のソースをクリアします。  
**1**  
%Systemroot%\System32\DNS 既定では、DNS のディレクトリにバインド ファイルから読み込みます。  
**2**  
レジストリから読み込みます。  
**3**  
AD DS とレジストリから読み込みます。 これは、既定の設定です。  
**/defaultagingstate [0 | 1]**  
既定では新しく作成されたゾーンで DNS 清掃機能が有効になっているかどうかを判断します。  
**0**  
清掃を無効にします。 これは、既定の設定です。  
**1**  
清掃を有効にします。  
**/defaultnorefreshinterval[0x1-0xFFFFFFFF|0xA8]**  
動的に更新されたレコードの更新が受け入れはありません時間の期間を設定します。 サーバー上のゾーンでは、この値を自動的に継承します。 既定値を変更するには、範囲の値を入力**0x1 0 xffffffff**します。 サーバーから既定値は**0xA8**します。  
**/defaultrefreshinterval [0x1-0xFFFFFFFF|0xA8]**  
DNS レコードの動的更新は許可されている時間の期間を設定します。 サーバー上のゾーンでは、この値を自動的に継承します。 既定値を変更するには、範囲の値を入力**0x1 0 xffffffff**します。 サーバーから既定値は**0xA8**します。  
**/disableautoreversezones [0 | 1]**  
有効または逆引き参照ゾーンの自動作成を無効にします。 逆引き参照ゾーンは、インターネット プロトコル (IP) アドレスの DNS ドメイン名への解決を提供します。  
**0**  
逆引き参照ゾーンの自動作成を有効にします。 これは、既定の設定です。  
**1**  
逆引き参照ゾーンの自動作成を無効にします。  
**/disablensrecordsautocreation {0|1}**  
かどうか、DNS サーバーが自動的に作成ネーム サーバー (NS) リソース レコードをホストしているゾーンを指定します。  
**0**  
ゾーンのネーム サーバー (NS) リソース レコードを自動的に作成し、DNS サーバーがホストされます。  
**1**  
自動的に作成されませんゾーンのネーム サーバー (NS) リソース レコードを DNS サーバーでホストします。  
**/dspollinginterval 0-30**  
どのくらいの頻度、DNS サーバー AD DS の変更をポーリング active directory 統合ゾーンを指定します。  
**/dstombstoneinterval 1 ~ 30**  
AD DS で削除されたレコードを保持する秒単位の時間。  
**/ednscachetimeout [<seconds>]**  
拡張の DNS (EDNS) 情報をキャッシュする秒数を指定します。 最小値は 3600、および最大値は 15,724,800 します。 既定値は、604,800 秒 (1 週間) です。  
**/enableednsprobes {0|1}**  
有効または他のサーバーをサポートしている EDNS かをプローブするサーバーを無効にします。  
**0**  
EDNS プローブの有効なサポートを無効にします。  
**1**  
EDNS プローブの有効なサポートを有効にします。  
**/enablednssec {0|1}**  
有効または、DNS セキュリティ拡張機能 (DNSSEC) に対するサポートを無効にします。  
**0**  
DNSSEC を無効にします。  
**1**  
DNSSEC を有効にします。  
**/enableglobalnamessupport {0 | 1}**  
有効または、GlobalNames ゾーンのサポートを無効にします。 GlobalNames ゾーンは、フォレスト全体で単一ラベル DNS 名の解決をサポートします。  
**0**  
GlobalNames ゾーンのサポートを無効にします。 このコマンドの値を設定すると**0**、DNS サーバー サービスは GlobalNames ゾーンで単一ラベル名を解決できません。  
**1**  
GlobalNames ゾーンのサポートを有効にします。 このコマンドの値を設定すると**1**、DNS サーバー サービスは GlobalNames ゾーンで単一ラベル名を解決します。  
**/enableglobalqueryblocklist {0 | 1}**  
有効または一覧の名前の名前解決をブロックするグローバル クエリ禁止リストのサポートを無効にします。 DNS サーバー サービスは、作成し、最初にサービスの起動時に、既定では、グローバル クエリ禁止リストを有効します。 現在のグローバル クエリ禁止リストを表示する、 **dnscmd/info/globalqueryblocklist**コマンド。  
**0**  
グローバル クエリ禁止リストのサポートを無効にします。 このコマンドの値を設定すると**0**、DNS サーバー サービスが、ブロック一覧の名前に対するクエリに応答します。  
**1**  
グローバル クエリ禁止リストのサポートを有効にします。 このコマンドの値を設定すると**1**、DNS サーバー サービスが、ブロック一覧の名前に対するクエリに応答しません。  
**/eventloglevel [0 | 1 | 2 | 4]**  
イベント ビューアーの DNS サーバー ログに記録するイベントを決定します。  
**0**  
イベントをログはありません。  
**1**  
エラーのみを記録します。  
**2**  
エラーと警告のみを記録します。  
**4**  
エラー、警告、および情報イベントを記録します。 これは、既定の設定です。  
**/forwarddelegations [0 | 1]**  
DNS サーバーが委任されたサブゾーンのクエリを処理する方法を決定します。 これらのクエリは、DNS サーバーのクエリで参照されるサブゾーンにまたはというフォワーダの一覧を送信できます。 エントリの設定では、転送が有効になっている場合にのみ使用されます。  
**0**  
自動的に適切なサブゾーンに委任された"サブゾーン"を参照するクエリを送信します。 これは、既定の設定です。  
**1**  
既存のフォワーダーに委任されたサブゾーンを参照するクエリを転送します。  
**/forwardingtimeout [<seconds>]**  
(0x1-0 xffffffff) までの秒数のもう 1 つのフォワーダーを試す前に応答するフォワーダー DNS サーバーが待機するかを決定します。 既定値は**0x5**、これは 5 秒です。  
**/globalneamesqueryorder** {**0|1**}  
かどうか、DNS サーバー サービスでは、最初、GlobalNames ゾーンまたはローカルのゾーンの名前を解決するときを指定します。  
**0**  
DNS サーバー サービスは、対象の権限のあるゾーンのクエリを実行する前に、GlobalNames ゾーンのクエリを実行して名前を解決しようとします。  
**1**  
DNS サーバー サービスは、対象の権限のある、GlobalNames ゾーンのクエリを実行する前に、ゾーンのクエリを実行して名前を解決しようとします。  
**/globalqueryblocklist[[<name> [<name>]...]**  
現在のグローバル クエリ禁止リストを指定した名前の一覧に置き換えます。 任意の名前を指定しない場合、このコマンドは、ブロック一覧をクリアします。 既定では、グローバル クエリ禁止リストには、次のものが含まれています。  
-   isatap  
-   wpad  
DNS サーバー サービスを削除できますこれらの名前は、どちらも、最初に開始時に既存のゾーンでこれらの名前を見つけた場合。  
**/isslave [0 | 1]**  
転送するクエリが応答を受信しないときの DNS サーバーの応答を決定します。  
**0**  
DNS サーバーは、従属要素ではないを指定します (とも呼ばれる、*スレーブ*)。 フォワーダーが応答しない場合、DNS サーバーは、クエリ自体を解決しようとします。 これは、既定の設定です。  
**1**  
DNS サーバーが下位であることを指定します。 フォワーダーが応答しない場合、DNS サーバーは、検索を終了し、競合回避モジュールにエラー メッセージを送信します。  
**/localnetpriority [0 | 1]**  
DNS サーバーが同じ名前の複数のホスト レコードをホスト レコードが返される順序を決定します。  
**0**  
DNS データベースに表示される順序でレコードを返します。  
**1**  
ような IP を持つレコードを返します。 ネットワーク アドレスに最初にします。 これは、既定の設定です。  
**/logfilemaxsize [<size>]**  
Dns.log ファイルのバイト数 (0 xffffffff 0x10000) では、最大サイズを指定します。 ファイルには、最大サイズに達すると、DNS は、最も古いイベントを上書きします。 既定のサイズは 4 メガバイト (MB) をある 0x400000、です。  
**/logfilepath [<path+LogFileName>]**  
Dns.log ファイルのパスを指定します。 既定のパスは、%systemroot%\system32\dns\dns.log です。 別のパスを指定するには、形式を使用して*パス + LogFileName*します。  
**/logipfilterlist <IPaddress> [,<IPaddress>...]**  
パケットがデバッグ ログ ファイルに記録されますを指定します。 エントリは、IP アドレスの一覧です。 リスト内の IP アドレスとの間に向かうパケットのみが記録されます。  
**/loglevel [<Eventtype>]**  
イベントの種類が Dns.log ファイルに記録されるかを決定します。 各イベントの種類は、16 進数で表されます。 ログ イベントの 1 つ以上の場合は、16 進数の追加を使用して、値を追加し、合計を入力します。  
**0x0**  
DNS サーバーでは、ログは作成されません。 これは、既定のエントリです。  
**0x10**  
クエリ ログに記録します。  
**0x10**  
通知を記録します。  
**0x20**  
更新プログラムを記録します。  
**0 xfe**  
Nonquery トランザクション ログに記録します。  
**0x100**  
トランザクションをログに質問します。  
**0x200**  
回答を記録します。  
**0x1000**  
ログは、パケットを送信します。  
**0x2000**  
ログは、パケットを受信します。  
**0x4000**  
ユーザー データグラム プロトコル (UDP) パケットを記録します。  
**0x8000**  
伝送制御プロトコル (TCP) のパケットを記録します。  
**0 xffff**  
すべてのパケットを記録します。  
**0x10000**  
Active directory 書き込みトランザクション ログに記録します。  
**0x20000**  
Active directory の更新のトランザクション ログに記録します。  
**0x1000000**  
ログの完全なパケット。  
**0x80000000**  
トランザクション ログ ライト スルーします。  
**/maxcachesize**  
DNS サーバーのメモリ キャッシュの最大サイズをキロバイト (KB) 単位でを指定します。  
**/maxcachettl [<seconds>]**  
(0x0 0 xffffffff) までの秒数のレコードは、キャッシュに保存を決定します。 場合、 **0x0**設定を使用すると、DNS サーバーがレコードをキャッシュしません。 既定の設定は**0x15180** (86,400 秒または 1 日)。  
**/maxnegativecachettl [<seconds>]**  
(0x1-0 xffffffff) までの秒数をクエリに否定応答を記録するエントリに保存、DNS キャッシュを指定します。 既定の設定は**0x384** (900 秒)。  
**/namecheckflag [0 | 1 | 2 | 3]。**  
DNS 名をチェックするときにどの文字標準が使用を指定します。  
**0**  
インターネット技術標準化を遵守する ANSI 文字を使用して強制的に (IETF) の Request for Comments (Rfc)。  
**1**  
IETF Rfc では、必ずしも準拠していない ANSI 文字を使用します。  
**2**  
マルチバイト UCS 変換の使用には、8 (utf-8) 文字が書式設定します。 これは、既定の設定です。  
**3**  
すべての文字を使用します。  
**/norecursion [0 | 1]**  
DNS サーバーが再帰的名前解決を実行するかどうかを判断します。  
**0**  
DNS サーバーは、クエリで要求された場合に、再帰的名前解決を実行します。 これは、既定の設定です。  
**1**  
DNS サーバーでは、再帰的名前解決は実行されません。  
**/notcp**  
このパラメータは古い形式、および Windows Server の現在のバージョンに影響を与えません。  
**/recursionretry [<seconds>]**  
(0x1-0 xffffffff) の DNS サーバーをもう一度リモート サーバーに接続する前に待機する秒数を決定します。 既定の設定は、0x3 (3 秒) です。 低速ワイド エリア ネットワーク (WAN) リンク経由で再帰が発生した場合は、この値を増やす必要があります。  
**/recursiontimeout [<seconds>]**  
(0x1-0 xffffffff) の DNS サーバーがリモート サーバーに接続試行を中止するまで待機する秒数を決定します。 設定の範囲**0x1**を通じて**0 xffffffff**します。 既定の設定は**0 xf** (15 秒)。 低速の WAN リンク経由で再帰が発生した場合は、この値を増やす必要があります。  
**/roundrobin [0 | 1]**  
サーバーが同じ名前の複数のホスト レコードをホスト レコードが返される順序を決定します。  
0  
DNS サーバーは、ラウンド ロビンを使用しません。 代わりに、すべてのクエリに、最初のレコードを返します。  
**1**  
DNS サーバーは、一致するレコードの一覧の一番下に上から返されるレコードの間で回転します。 これは、既定の設定です。  
**/rpcprotocol [0x0 | 0x1 | 0x2 | 0x4 | 0 xffffffff]**  
DNS サーバーから接続するときにリモート プロシージャ コール (RPC) が使用するプロトコルを指定します。  
**0x0**  
DNS の RPC を無効にします。  
**0x1**  
TCP/IP を使用します。  
**0x2**  
名前付きパイプを使用します。  
**0x4**  
ローカル プロシージャ呼び出し (LPC) を使用します。  
**0 xffffffff**  
すべてのプロトコル。 これは、既定の設定です。  
**/scavenginginterval [<hours>]**  
DNS サーバーの清掃機能が有効であり、サイクルを清掃間隔の時間 (0x0 0 xffffffff) の数を設定するかどうかを判断します。 既定の設定は**0x0**、DNS サーバーの清掃を無効にします。 設定よりも大きい**0x0**サーバーの清掃を有効にし、清掃サイクル間の時間数を設定します。  
**[0 | 1]**  
DNS がキャッシュに保存されているレコードをフィルター処理するかどうかを判断します。  
**0**  
名前のクエリに応答するすべてをキャッシュに保存します。 これは、既定の設定です。  
**1**  
キャッシュに同じ DNS サブツリーに属しているレコードだけを保存します。  
**/sendport [<port>]**  
DNS を使用して他の DNS サーバーに再帰的なクエリを送信するポート番号 (0x0 0 xffffffff) を指定します。 既定の設定は**0x0**、つまり、ポート番号がランダムに選択されています。  
**/serverlevelplugindll[<Dllpath>]**  
カスタム プラグインのパスを指定します。 ときに*Dllpath*プラグインは、DNS サーバーでホストされるゾーンのローカルですべての範囲外にある名前クエリを解決するには、プラグインの関数の呼び出しの有効な DNS サーバーの完全修飾パス名を指定します。 照会された名前が、プラグインのスコープ外にある場合は、DNS サーバーは、構成されている転送または再帰を使用して名前解決を実行します。 場合*Dllpath*が指定されていない、カスタム プラグインが以前に構成されている場合は、カスタム プラグインを使用する DNS サーバーを停止します。  
**/strictfileparsing [0 | 1]**  
ゾーンの読み込み中にエラーがあるレコードを見つけたときに、DNS サーバーの動作を決定します。  
**0**  
DNS サーバーは、サーバーが、正しくないレコードを検出した場合でも、ゾーンを読み込むことが続行されます。 エラーは、DNS ログに記録されます。 これは、既定の設定です。  
**1**  
DNS サーバーは、ゾーンの読み込みを停止し、DNS ログにエラーが記録します。  
**/updateoptions <RecordValue>**  
指定した種類のレコードの動的更新を禁止します。 1 つ以上のレコードの種類をログに禁止する場合は、16 進数の追加を使用して、値を追加し、合計を入力します。  
**0x0**  
すべてのレコードの種類を制限しません。  
**0x1**  
Authority (SOA) リソース レコードの開始を除外します。  
**0x2**  
ネーム サーバー (NS) リソース レコードを除外します。  
**0x4**  
ネーム サーバー (NS) リソース レコードの委任を除外します。  
**0x8**  
サーバーのホスト レコードを除外します。  
**0x100**  
セキュリティで保護の動的更新中には、authority (SOA) リソース レコードの開始を除外します。  
**0x200**  
セキュリティで保護の動的更新中には、ルート ネーム サーバー (NS) リソース レコードを除外します。  
**0x30F**  
標準の動的更新中には、ネーム サーバー (NS) リソース レコードの authority (SOA) リソース レコード、およびサーバーのホスト レコードの開始を除外します。 セキュリティで保護の動的更新中に、ルート ネーム サーバー (NS) リソース レコードと authority (SOA) リソース レコードの開始を除外します。 により、委任とサーバーの更新をホストします。  
**0x400**  
セキュリティで保護の動的更新中には、委任ネーム サーバー (NS) リソース レコードを除外します。  
**0x800**  
セキュリティで保護の動的更新中には、サーバーのホスト レコードを除外します。  
**0x1000000**  
委任署名者 (DS) のレコードを除外します。  
**0x80000000**  
DNS 動的更新を無効にします。  
**/writeauthorityns [0|1]**  
応答の機関のセクションでは、DNS サーバーがネーム サーバー (NS) リソース レコードを書き込む場合を決定します。  
**0**  
のみの参照の機関のセクションでは、ネーム サーバー (NS) リソース レコードを書き込みます。 この設定は、Rfc 1034、ドメイン名の概念と機能、および Rfc 2181、明確に DNS の仕様に準拠しています。 これは、既定の設定です。  
**1**  
成功したすべての権限のある応答の機関のセクションでは、ネーム サーバー (NS) リソース レコードを書き込みます。  
**/xfrconnecttimeout [<seconds>]**  
プライマリ DNS サーバーをセカンダリ サーバーから転送の応答を待機する秒 (0x0 0 xffffffff) の数を決定します。 既定値は**0x1E** (30 秒)。 タイムアウト値を過ぎると、接続は終了します。  
#### <a name="zone-level-syntax"></a>ゾーン レベルの構文  
```  
dnscmd /config <Parameters>  
```  
#### <a name="dnscmd-config"></a>dnscmd /config  
指定したゾーンの構成を変更します。  
#### <a name="parameters"></a>パラメーター  
**<Parameters>**  
ゾーン名、し、値、オプションの設定を指定します。 パラメーターの値は、この構文を使用します。*ゾーン名パラメーター* [*値*]  
このセクションの残りの部分では、次のパラメーター値が記載されています。  
-   **/aging**  
-   **/allownsrecordsautocreation**  
-   **/allowupdate**  
-   **/forwarderslave**  
-   **/forwardertimeout**  
-   **/norefreshinterval**  
-   **/refreshinterval**  
-   **/securesecondaries**  
**/aging <ZoneName>**  
有効または、特定のゾーンで清掃を無効にします。  
**/allownsrecordsautocreation  <ZoneName> [<Value>]**  
DNS サーバーの名前サーバー (NS) リソース レコード autocreation 設定をオーバーライドします。 このゾーンに登録されていたネーム サーバー (NS) リソース レコードには影響しません。 そのため、する必要があります手動で削除してしない場合。  
**/allowupdate <ZoneName>**  
指定されたゾーンが動的更新を受け入れるかどうかを判断します。  
**/forwarderslave <ZoneName>**  
DNS サーバーを上書き **/isslave**設定します。  
**/forwardertimeout <ZoneName>**  
もう 1 つのフォワーダーを試す前に応答するフォワーダー待ちます DNS ゾーンを秒数を決定します。 この値は、サーバー レベルで設定されている値をオーバーライドします。  
**/norefreshinterval <ZoneName>**  
ゾーンを更新できますを動的に更新なしで指定されたゾーンの DNS レコードの時間間隔を設定します。  
**/refreshinterval <ZoneName>**  
ゾーンを更新は動的に指定されたゾーンの DNS レコードを更新の時間間隔を設定します。  
**/securesecondaries <ZoneName>**  
セカンダリ サーバーは、このゾーンのマスター サーバーからゾーンの更新プログラムを受信することができますを決定します。  
#### <a name="remarks"></a>注釈  
-   ゾーン レベルのパラメーターに対してのみ、ゾーン名を指定する必要があります。  
### <a name="BKMK_4"></a>dnscmd /createbuiltindirectorypartitions  
DNS アプリケーション ディレクトリ パーティションを作成します。 DNS がインストールされているフォレストおよびドメイン レベルでサービスのアプリケーション ディレクトリ パーティションが作成されます。 このコマンドを使用して、削除されたか、作成されていない DNS アプリケーション ディレクトリ パーティションを作成します。 パラメーターなしでは、このコマンドは、ドメインの組み込み DNS ディレクトリ パーティションを作成します。  
#### <a name="syntax"></a>構文  
```  
dnscmd [<ServerName>] /createbuiltindirectorypartitions [/forest] [/alldomains]   
```  
#### <a name="parameters"></a>パラメーター  
**<ServerName>**  
IP アドレス、FQDN、またはホスト名によって表されるを管理する DNS サーバーを指定します。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
**/forest**  
フォレストの DNS ディレクトリ パーティションを作成します。  
**/alldomains**  
フォレスト内のすべてのドメイン DNS パーティションを作成します。  
### <a name="BKMK_5"></a>dnscmd /createdirectorypartition  
DNS アプリケーション ディレクトリ パーティションを作成します。 DNS がインストールされているフォレストおよびドメイン レベルでサービスのアプリケーション ディレクトリ パーティションが作成されます。 この操作は、追加の DNS アプリケーション ディレクトリ パーティションを作成します。  
#### <a name="syntax"></a>構文  
```  
dnscmd [<ServerName>] /createdirectorypartition <PartitionFQDN>  
```  
#### <a name="parameters"></a>パラメーター  
**<ServerName>**  
IP アドレス、FQDN、またはホスト名によって表されるを管理する DNS サーバーを指定します。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
**<PartitionFQDN>**  
作成される DNS アプリケーション ディレクトリ パーティションの FQDN。  
### <a name="BKMK_6"></a>dnscmd /deletedirectorypartition  
既存の DNS アプリケーション ディレクトリ パーティションを削除します。  
#### <a name="syntax"></a>構文  
```  
dnscmd [<ServerName>] /deletedirectorypartition <PartitionFQDN>  
```  
#### <a name="parameters"></a>パラメーター  
**<ServerName>**  
IP アドレス、FQDN、またはホスト名によって表されるを管理する DNS サーバーを指定します。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
**<PartitionFQDN>**  
削除される DNS アプリケーション ディレクトリ パーティションの FQDN。  
### <a name="BKMK_7"></a>dnscmd /directorypartitioninfo  
指定した DNS アプリケーション ディレクトリ パーティションに関する情報を一覧表示します。  
#### <a name="syntax"></a>構文  
```  
dnscmd [<ServerName>] /directorypartitioninfo <PartitionFQDN> [/detail]   
```  
#### <a name="parameters"></a>パラメーター  
**<ServerName>**  
IP アドレス、FQDN、またはホスト名によって表されるを管理する DNS サーバーを指定します。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
**<PartitionFQDN>**  
DNS アプリケーション ディレクトリ パーティションの FQDN。  
**/detail**  
アプリケーション ディレクトリ パーティションのすべての情報を一覧表示します。  
### <a name="BKMK_8"></a>dnscmd /enlistdirectorypartition  
指定されたディレクトリ パーティションのレプリカ セットには、DNS サーバーを追加します。  
#### <a name="syntax"></a>構文  
```  
dnscmd [<ServerName>] /enlistdirectorypartition <PartitionFQDN>  
```  
#### <a name="parameters"></a>パラメーター  
**<ServerName>**  
IP アドレス、FQDN、またはホスト名によって表されるを管理する DNS サーバーを指定します。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
**<PartitionFQDN>**  
DNS アプリケーション ディレクトリ パーティションの FQDN。  
### <a name="BKMK_9"></a>dnscmd /enumdirectorypartitions  
指定されたサーバーの DNS アプリケーション ディレクトリ パーティションを一覧表示します。  
#### <a name="syntax"></a>構文  
```  
dnscmd [<ServerName>] /enumdirectorypartitions [/custom]   
```  
#### <a name="parameters"></a>パラメーター  
**<ServerName>**  
IP アドレス、FQDN、またはホスト名によって表されるを管理する DNS サーバーを指定します。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
**/custom**  
ユーザーが作成したディレクトリ パーティションのみを一覧表示します。  
### <a name="BKMK_10"></a>dnscmd /enumrecords  
DNS ゾーンで指定されたノードのリソース レコードを一覧表示します。  
#### <a name="syntax"></a>構文  
```  
dnscmd [<ServerName>] /enumrecords <ZoneName> <NodeName> [/type <RRtype> <Rrdata>] [/authority] [/glue] [/additional] [/node | /child | /startchild<ChildName>] [/continue | /detail]   
```  
#### <a name="parameters"></a>パラメーター  
**<ServerName>**  
DNS サーバーを管理するを指定します。 は、IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
**/enumrecords**  
指定したゾーン内のリソース レコードを一覧表示します。  
**<ZoneName>**  
リソース レコードが属しているゾーンの名前を指定します。  
**<NodeName>**  
リソース レコードのノードの名前を指定します。  
**/type <RRtype> <Rrdata>**  
一覧表示するリソース レコードの種類と予想されるデータの種類を指定します。  
**<RRtype>**  
一覧表示するリソース レコードの種類を指定します。  
**<Rrdata>**  
予期されるレコードは、データの種類を指定します。  
**/authority**  
権限のあるデータが含まれています。  
**/glue**  
グルー データが含まれています。  
**/additional**  
表示されているリソース レコードに関するすべての追加情報が含まれています。  
**{0}/ノード |/child |/startchild <ChildName>}**  
フィルター処理するか、リソース レコードの表示に情報を追加します。  
**/node**  
指定したノードのリソース レコードのみを一覧表示します。  
**/child**  
指定した子ドメインのリソース レコードのみを一覧表示します。  
**/startchild <ChildName>**  
指定した子ドメインにあるリストを開始します。  
**/continue | /detail**  
返されるデータの表示方法を指定します。  
**/continue**  
それらの型とデータとリソース レコードのみを一覧表示します。  
**/detail**  
リソース レコードに関するすべての情報を一覧表示します。  
#### <a name="sample-usage"></a>サンプルの使用法  
`dnscmd /enumrecords test.contoso.com test /additional`  
### <a name="BKMK_11"></a>dnscmd/enumzones  
指定した DNS サーバー上に存在するゾーンを一覧表示します。  
#### <a name="syntax"></a>構文  
```  
dnscmd [<ServerName>] /enumzones [/primary | /secondary | /forwarder | /stub | /cache | /auto-created] [/forward | /reverse | /ds | /file] [/domaindirectorypartition | /forestdirectorypartition | /customdirectorypartition | /legacydirectorypartition | /directorypartition <PartitionFQDN>]  
```  
#### <a name="parameters"></a>パラメーター  
**<ServerName>**  
IP アドレス、FQDN、またはホスト名によって表されるを管理する DNS サーバーを指定します。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
**/primary | /secondary | /forwarder | /stub | /cache | /auto-created**  
フィルターを表示するゾーンの種類:  
**/primary**  
標準プライマリ ゾーンまたは active directory 統合ゾーンのいずれかであるすべてのゾーンを一覧表示します。  
**/secondary**  
標準のすべてのセカンダリ ゾーンを一覧表示します。  
**/forwarder**  
別の DNS サーバーに未解決のクエリを転送するゾーンを一覧表示します。  
**/stub**  
スタブ ゾーンをすべて一覧表示します。  
**/cache**  
キャッシュに読み込まれるゾーンのみを一覧表示します。  
**/auto-created**  
DNS サーバーのインストール時に自動的に作成されたゾーンを一覧表示します。  
**/forward | /reverse | /ds | /file**  
表示するゾーンの種類の追加のフィルターを指定します。  
**/**  
リストは前方参照ゾーンです。  
**/reverse**  
リストは逆引き参照ゾーンです。  
**/ds**  
active directory 統合ゾーンを一覧表示します。  
**/file**  
ファイルで提供されるゾーンを一覧表示します。  
**/domaindirectorypartition**  
ドメイン ディレクトリ パーティションに格納されているゾーンを一覧表示します。  
**/forestdirectorypartition**  
フォレスト DNS アプリケーション ディレクトリ パーティションに格納されているゾーンを一覧表示します。  
**/customdirectorypartition**  
ユーザー定義のアプリケーション ディレクトリ パーティションに格納されているすべてのゾーンを一覧表示します。  
**/legacydirectorypartition**  
ドメイン ディレクトリ パーティションに格納されているすべてのゾーンを一覧表示します。  
**/directorypartition <PartitionFQDN>**  
指定されたディレクトリ パーティションに格納されているすべてのゾーンを一覧表示します。  
#### <a name="remarks"></a>注釈  
-   **Enumzones**パラメーターは、ゾーンの一覧でフィルターとして機能します。 フィルターが指定されていない場合は、ゾーンの完全な一覧が返されます。 フィルターを指定すると、返されるゾーンの一覧にそのフィルターの条件を満たすゾーンのみが含まれます。  
#### <a name="example"></a>例  
参照してください[例 2。DNS サーバーでゾーンの完全な一覧を表示](https://technet.microsoft.com/library/cc784399(v=ws.10).aspx)または[例 3。DNS サーバーの自動作成ゾーンの一覧を表示](https://technet.microsoft.com/library/cc784399(v=ws.10).aspx)します。  
### <a name="BKMK_25a"></a>dnscmd /exportsettings  
DNS サーバーの構成の詳細を一覧表示するテキスト ファイルを作成します。 テキスト ファイルの名前は DnsSettings.txt します。 サーバーの %systemroot%\system32\dns ディレクトリにあります。  
#### <a name="syntax"></a>構文  
```  
dnscmd [<ServerName>] /exportsettings   
```  
#### <a name="parameters"></a>パラメーター  
**<ServerName>**  
を管理する DNS サーバーの指定は、ローカル コンピューターの構文、IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
#### <a name="remarks"></a>注釈  
-   ファイルの情報を使用することができますを**dnscmd/exportsettings**構成の問題のトラブルシューティングを行うように構成する複数のサーバーが同じまたは作成します。  
### <a name="BKMK_12"></a>dnscmd /info  
指定したサーバーのレジストリの DNS セクションから設定が表示されます。**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DNS\Parameters**  
#### <a name="syntax"></a>構文  
```  
dnscmd [<ServerName>] /info [<Setting>]  
```  
#### <a name="parameters"></a>パラメーター  
**<ServerName>**  
IP アドレス、FQDN、またはホスト名によって表されるを管理する DNS サーバーを指定します。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
**<Setting>**  
あるすべての設定、**情報**返すコマンドを個別に指定することができます。 設定が指定されていない場合は、一般的な設定のレポートが返されます。  
#### <a name="remarks"></a>注釈  
-   このコマンドは、DNS サーバー レベルのレジストリ設定を表示します。 ゾーン レベルのレジストリ設定を表示するには、使用、 [zoneinfo](#BKMK_26)コマンド。 このコマンドで表示可能な設定の一覧を表示するには、次を参照してください。、 [config](#BKMK_3)説明します。  
#### <a name="example"></a>例  
参照してください[例 4。DNS サーバーから IsSlave 設定を表示する](https://technet.microsoft.com/library/cc784399(v=ws.10).aspx)または[例 5。DNS サーバーから Recursiontimeout 設定を表示する](https://technet.microsoft.com/library/cc784399(v=ws.10).aspx)します。  
### <a name="BKMK_29a"></a>dnscmd/ipvalidate  
IP アドレスが機能している DNS サーバーまたは DNS サーバーがフォワーダー、ルート ヒントのサーバー、または特定のゾーンのマスター サーバーとして機能するかどうかを識別するかどうかをテストします。  
#### <a name="syntax"></a>構文  
```  
dnscmd [<ServerName>] /ipvalidate <Context> [<ZoneName>] [[<IPaddress>]]  
```  
#### <a name="parameters"></a>パラメーター  
**<ServerName>**  
を管理する DNS サーバーの指定は、ローカル コンピューターの構文、IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
**<Context>**  
実行するテストの種類を指定します。 次のテストのいずれかを指定できます。  
-   **/dnsservers**コンピューターを指定したアドレスに DNS サーバーが機能していることをテストします。  
-   **/forwarders**指定したアドレスがフォワーダとして機能できる DNS サーバーを識別することをテストします。  
-   **/roothints**指定したアドレスがルート ヒントのネーム サーバーとして機能できる DNS サーバーを識別することをテストします。  
-   **/zonemasters**テスト用のマスター サーバーの DNS サーバーを指定したアドレスに識別*ZoneName*します。  
**<ZoneName>**  
ゾーンを識別します。 このパラメーターを使用して、 **/zonemasters**パラメーター。  
**<IPaddress>**  
コマンドをテストする IP アドレスを指定します。  
#### <a name="sample-usage"></a>サンプルの使用法  
<pre>dnscmd dnssvr1.contoso.com /ipvalidate /dnsservers 10.0.0.1 10.0.0.2  
dnscmd dnssvr1.contoso.com /ipvalidate /zonemasters corp.contoso.com 10.0.0.2</pre>  
### <a name="BKMK_13"></a>dnscmd /nodedelete  
指定されたホストのすべてのレコードを削除します。 ### 構文```  
dnscmd [<ServerName>]/nodedelete <ZoneName> <NodeName> [/tree] [/f] ```  
#### Parameters  
**<ServerName>**  
IP アドレス、FQDN、またはホスト名によって表されるを管理する DNS サーバーを指定します。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
**<ZoneName>**  
ゾーンの名前を指定します。  
**<NodeName>**  
削除するノードのホスト名を指定します。  
**/tree**  
すべての子レコードを削除します。  
**/f**  
確認を求めずに、コマンドを実行します。 ### 例を参照してください[例 6: ノードからレコードを削除](https://technet.microsoft.com/library/cc784399(v=ws.10).aspx)します。  
### <a name="BKMK_14"></a>dnscmd /recordadd  
DNS サーバーで指定されたゾーンにレコードを追加します。 ### 構文```  
dnscmd [<ServerName>]/recordadd <ZoneName> <NodeName> <RRtype> <Rrdata> ```  
#### Parameters  
**<ServerName>**  
を管理する DNS サーバーの指定は、ローカル コンピューターの構文、IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
**<ZoneName>**  
レコードが存在するゾーンを指定します。  
**<NodeName>**  
ゾーンでは、特定のノードを指定します。  
**<RRtype>**  
追加するレコードの種類を指定します。  
**<Rrdata>**  
予想されるデータの種類を指定します。  
> [!NOTE]  
レコードを追加するときに、正しいデータ型とデータ形式を使用することを確認します。 リソース レコードの種類と適切なデータ型の一覧は、次を参照してください。[リソース レコード リファレンス](https://technet.microsoft.com/library/cc758321(v=ws.10).aspx)します。 ### サンプルの使用法
<pre>dnscmd dnssvr1.contoso.com /recordadd test A 10.0.0.5  
dnscmd /recordadd test.contoso.com test MX 10 mailserver.test.contoso.com</pre>  
### <a name="BKMK_15"></a>dnscmd /recorddelete  
指定されたゾーンからリソース レコードを削除します。 ### 構文```  
dnscmd <ServerName>/recorddelete <ZoneName> <NodeName> <RRtype> <Rrdata>[/f] ```  
#### Parameters  
**<ServerName>**  
> IP アドレス、FQDN、またはホスト名によって表されるを管理する DNS サーバーを指定します。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
**<ZoneName>**  
リソース レコードが存在するゾーンを指定します。  
**<NodeName>**  
ホストの名前を指定します。  
**<RRtype>**  
削除するリソース レコードの種類を指定します。  
**<Rrdata>**  
予想されるデータの種類を指定します。  
**/f**  
確認を求めずにコマンドを実行します:-このコマンドが、削除するリソース レコードの種類について、明確に限定する必要がありますノードが 1 つ以上のリソース レコードを持てないためです。 データ型を指定するリソース レコードのデータの種類を指定しない場合は、指定されたノードの場合は、その特定のデータ型を持つすべてのレコードが削除されます。 ### サンプルの使用法 `dnscmd /recorddelete test.contoso.com test MX 10 mailserver.test.contoso.com`  
### <a name="BKMK_16"></a>dnscmd /resetforwarders  
選択するか、DNS サーバーがローカルで解決できないときに DNS クエリを転送する IP アドレスをリセットします。 ### 構文```  
dnscmd [<ServerName>]/resetforwarders [<IPaddress> [、<IPaddress>]...][/タイムアウト<timeOut>] [/slave |/noslave] ```  
#### Parameters  
**<ServerName>**  
IP アドレス、FQDN、またはホスト名によって表されるを管理する DNS サーバーを指定します。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
**<IPaddress>**  
DNS サーバーが解決されていないクエリを転送する IP アドレスを一覧表示します。  
* */タイムアウト <timeOut>**  
DNS サーバーがフォワーダーからの応答を待機する秒数を設定します。 既定では、この値は 5 秒です。  
**/slave|/noslave**  
クエリを解決するのには、フォワーダーが失敗した場合、DNS サーバーが独自の反復的なクエリを実行するかどうかを決定します。  
**/slave**  
DNS サーバーがクエリを解決するのには、フォワーダーが失敗した場合、独自の反復的なクエリを実行するを防ぎます。  
**/noslave**  
クエリを解決するのには、フォワーダーが失敗した場合は、独自の反復的なクエリを実行する DNS サーバーを使用できます。 これは、既定の設定です。 ### 解説 - 既定では、DNS サーバーを反復的なクエリ実行、クエリを解決できない場合にします。 -IP アドレスの設定を使用して、 **resetforwarders**コマンドは、指定された IP アドレスの DNS サーバーの再帰的なクエリを実行する DNS サーバーを実行します。 フォワーダーで、クエリが解決しない場合、DNS サーバーは、独自の反復的なクエリを実行できます。 場合、 **/スレーブ**パラメーターを使うと、DNS サーバーが独自の反復的なクエリを実行していません。 つまり、DNS サーバーが一覧で、DNS サーバーのみに未解決のクエリを転送および、そのフォワーダーが解決しない場合、反復的なクエリは試行しません。 DNS サーバーのフォワーダーとして 1 つの IP アドレスを設定する方が効率的になります。 使用することができます、 **resetforwarders**を外部接続を持つ 1 つの DNS サーバーに、未解決のクエリを転送するように、ネットワーク内の内部サーバーのコマンド。 -2 回、そのサーバーに転送しようとする DNS サーバーを原因、フォワーダーの IP アドレスを 2 回一覧表示します。 ### サンプルの使用法
<pre>dnscmd dnssvr1.contoso.com /resetforwarders 10.0.0.1 /timeout 7 /slave  
dnscmd dnssvr1.contoso.com /resetforwarders /noslave</pre>  
### <a name="BKMK_17"></a>dnscmd /resetlistenaddresses  
DNS クライアントの要求をリッスンするサーバーの IP アドレスを指定します。 ### 構文```  
dnscmd [<ServerName>]/resetlistenaddresses [<listenaddress>] ```  
#### Parameters  
**<ServerName>**  
IP アドレス、FQDN、またはホスト名によって表されるを管理する DNS サーバーを指定します。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
**<listenaddress>**  
DNS クライアントの要求をリッスンする DNS サーバーの IP アドレスを指定します。 リッスンするアドレスが指定されていない場合、サーバー上のすべての IP アドレスはクライアント要求をリッスンします。 ### 解説 - 既定では、DNS サーバー上のすべての IP アドレスをリッスン クライアント DNS 要求。 ### サンプルの使用法 `dnscmd dnssvr1.contoso.com /resetlistenaddresses 10.0.0.1`  
### <a name="BKMK_18"></a>dnscmd /startscavenging  
指定した DNS サーバーに古いリソース レコードの即時に検索を試行する DNS サーバーに指示します。 ### 構文```  
dnscmd [<ServerName>]/startscavenging ```  
#### Parameter  
**<ServerName>**  
IP アドレス、FQDN、またはホスト名によって表されるを管理する DNS サーバーを指定します。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。 ### 解説 - このコマンドが正常に完了、清掃を直ちに開始します。 -次の前提条件が満たされている場合を除き、、清掃を開始するコマンドが正常に完了が表示されたらが、清掃を行うは開始できません:-両方のサーバーとゾーンの清掃が有効にします。 -ゾーンが開始されます。 リソース レコードでは、タイムスタンプがあります。 -サーバーの清掃を有効にする方法については、次を参照してください。、 **scavenginginterval**でサーバー レベルの構文でパラメーター、 [config](#BKMK_3)セクション。 -ゾーンの清掃を有効にする方法については、次を参照してください。、**エージング**でゾーン レベルの構文の下のパラメーター、 [config](#BKMK_3)セクション。 -一時停止されているゾーンを開始する方法については、次を参照してください。、 [zoneresume](#BKMK_35)セクション。 -リソース レコードのタイムスタンプを確認する方法については、次を参照してください。、 [ageallrecords](#BKMK_1)セクション。 かどうか、清掃を行う失敗、警告メッセージは表示されません。 ### サンプルの使用法 `dnscmd dnssvr1.contoso.com /startscavenging`  
### <a name="BKMK_19"></a>dnscmd /statistics  
表示または指定された DNS サーバーのデータを消去します。 ### 構文```  
dnscmd [<ServerName>]/statistics [<StatID>] []、[クリア] ```  
#### Parameters  
**<ServerName>**  
IP アドレス、FQDN、またはホスト名によって表されるを管理する DNS サーバーを指定します。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
**<StatID>**  
統計情報を表示する統計情報の組み合わせを指定します。 Id 番号を使用して、統計情報を識別します。 統計の ID 番号が指定されていない場合のすべての統計を表示します。  
指定できる番号と対応する統計情報を表示するの一覧を次には。  
**00000001**  
time  
**00000002**  
クエリ (query)  
**00000004**  
クエリ 2  
**00000008**  
Recurse  
**00000010**  
マスタ  
**00000020**  
セカンダリ  
**00000040**  
WINS  
**00000100**  
更新  
**00000200**  
SkwanSec  
**00000400**  
ds  
**00010000**  
メモリ  
**00100000**  
PacketMem  
**00040000**  
Dbase  
**00080000**  
[レコード]  
**00200000**  
NbstatMem  
**/clear**  
0 に指定した統計カウンターをリセットします。 ### 解説 -、**統計**が起動または再開時にコマンドに DNS サーバーで開始するカウンターが表示されます。 ### 例については[例 7。DNS サーバーの時間の統計情報の表示](https://technet.microsoft.com/library/cc784399(v=ws.10).aspx)または[例 8。DNS サーバーの NbstatMem 統計情報の表示](https://technet.microsoft.com/library/cc784399(v=ws.10).aspx)します。  
### <a name="BKMK_20"></a>dnscmd /unenlistdirectorypartition  
指定されたディレクトリ パーティションのレプリカ セットから、DNS サーバーを削除します。 ### 構文```  
dnscmd [<ServerName>]/unenlistdirectorypartition <PartitionFQDN> ```  
#### Parameters  
**<ServerName>**  
IP アドレス、FQDN、またはホスト名によって表されるを管理する DNS サーバーを指定します。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
**<PartitionFQDN>**  
削除される DNS アプリケーション ディレクトリ パーティションの FQDN。  
### <a name="BKMK_21"></a>dnscmd /writebackfiles  
変更については、DNS サーバーのメモリをチェック、永続的ストレージに書き込みます。 ### 構文```  
dnscmd [<ServerName>]/writebackfiles [<ZoneName>] ```  
#### Parameters  
**<ServerName>**  
IP アドレス、FQDN、またはホスト名によって表されるを管理する DNS サーバーを指定します。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
**<ZoneName>**  
更新するゾーンの名前を指定します。 ### 解説 -、 **writebackfiles**コマンドは、すべてのダーティ ゾーンまたは指定されたゾーンを更新します。 永続的ストレージに書き込まれていないメモリ内の変更がある場合に、ゾーンがダーティです。 これは、すべてのゾーンを確認するサーバー レベルの操作です。 この操作で 1 つのゾーンを指定するか、使用することができます、 [zonewriteback](#BKMK_37)操作。 ### サンプルの使用法 `dnscmd dnssvr1.contoso.com /writebackfiles`  
### <a name="BKMK_22"></a>dnscmd/zoneadd  
DNS サーバーにゾーンを追加します。 ### 構文```  
dnscmd [<ServerName>]/zoneadd <ZoneName> <Zonetype> [/dp <FQDN>|{/ドメイン |/エンタープライズ | レガシ/}] ```  
#### Parameters  
**<ServerName>**  
IP アドレス、FQDN、またはホスト名によって表されるを管理する DNS サーバーを指定します。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
**<ZoneName>**  
ゾーンの名前を指定します。  
**<Zonetype>**  
作成するゾーンの種類を指定します。 各ゾーンの種類では、他の必要なパラメーターがあります。  
**/dsprimary**  
active directory 統合ゾーンを作成します。  
* */プライマリ/file <FileName>**  
標準のプライマリ ゾーンを作成し、ゾーン情報を格納するファイルの名前を指定します。  
* */セカンダリ<MasterIPaddress>[<MasterIPaddress>...]**  
標準のゾーンのセカンダリを作成します。  
* */スタブ<MasterIPaddress>[<MasterIPaddress>...] ファイル <FileName>**  
ファイルに格納されたスタブ ゾーンを作成します。  
**/dsstub <MasterIPaddress> [<MasterIPaddress>...]**  
active directory 統合スタブ ゾーンを作成します。  
**/forwarder <MasterIPaddress> [<MasterIPaddress>]... /file <FileName>**  
作成されたゾーンが別の DNS サーバーに未解決のクエリを転送することを指定します。  
**/dsforwarder**  
作成した active directory 統合ゾーンが別の DNS サーバーに未解決のクエリを転送することを指定します。  
**/dp <FQDN> {/domain | /enterprise | /legacy}**  
ゾーンの格納先となるディレクトリ パーティションを指定します。  
**<FQDN>**  
ディレクトリ パーティションの FQDN を指定します。  
**/domain**  
ドメイン ディレクトリ パーティションにゾーンを格納します。  
**/enterprise**  
エンタープライズ ディレクトリ パーティションにゾーンを格納します。  
**/legacy**  
従来のディレクトリ パーティションにゾーンを格納します。 ### 解説 - のゾーンの種類を指定する **/forwarder**または **/dsforwarder**条件付き転送を実行するゾーンを作成します。 ### サンプルの使用法
<pre>dnscmd dnssvr1.contoso.com /zoneadd test.contoso.com /dsprimary  
dnscmd dnssvr1.contoso.com /zoneadd secondtest.contoso.com /secondary 10.0.0.2</pre>  
### <a name="BKMK_23"></a>dnscmd /zonechangedirectorypartition  
指定されたゾーンが存在するディレクトリ パーティションを変更します。 ### 構文```  
dnscmd [<ServerName>]/zonechangedirectorypartition <ZoneName>] {[<NewPartitionName>] |[<Zonetype>] } ```  
#### Parameters  
**<ServerName>**  
IP アドレス、FQDN、またはホスト名によって表されるを管理する DNS サーバーを指定します。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
**<ZoneName>**  
ゾーンが存在する現在のディレクトリ パーティションの FQDN。  
**<NewPartitionName>**  
ゾーンに移動されるディレクトリ パーティションの FQDN です。  
**<Zonetype>**  
ゾーンに移動されるディレクトリ パーティションの種類を指定します。  
**/domain**  
組み込みのドメイン ディレクトリ パーティションにゾーンに移動します。  
**/forest**  
組み込みのフォレスト ディレクトリ パーティションにゾーンに移動します。  
**/legacy**  
ゾーンを active directory ドメイン コント ローラーの前に作成されるディレクトリ パーティションに移動します。 これらのディレクトリ パーティションでは、ネイティブ モードは必要ありません。  
### <a name="BKMK_24"></a>dnscmd /zonedelete  
指定されたゾーンを削除します。 ### 構文```  
dnscmd [<ServerName>] するか<ZoneName>[/dsdel] [/f] ```  
#### Parameters  
**<ServerName>**  
IP アドレス、FQDN、またはホスト名によって表されるを管理する DNS サーバーを指定します。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
**<ZoneName>**  
削除するゾーンの名前を指定します。  
**/dsdel**  
AD DS からゾーンを削除します。  
**/f**  
確認を求めずにコマンドを実行します。 ### 例を参照してください[例 9: DNS サーバーからゾーンを削除](https://technet.microsoft.com/library/cc784399(v=ws.10).aspx)します。  
### <a name="BKMK_25"></a>dnscmd /zoneexport  
指定されたゾーンのリソース レコードを一覧表示するテキスト ファイルを作成します。 ### 構文 'dnscmd [<ServerName>]/zoneexport <ZoneName> <ZoneExportFile>' ### パラメーター * *<ServerName>**  
を管理する DNS サーバーの指定は、ローカル コンピューターの構文、IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
**<ZoneName>**  
ゾーンの名前を指定します。  
**<ZoneExportFile>**  
作成するファイルの名前を指定します。 ### 解説 -、 **zoneexport**操作は、トラブルシューティングのために、active directory 統合ゾーンのリソース レコードのファイルを作成します。 既定では、このコマンドが作成したファイルは %systemroot%/System32/Dns ディレクトリに既定では DNS ディレクトリに配置されます。 ### 例を参照してください[例 10。ゾーン リソース レコードの一覧をファイルにエクスポート](https://technet.microsoft.com/library/cc784399(v=ws.10).aspx)します。  
### <a name="BKMK_26"></a>dnscmd /zoneinfo  
指定されたゾーンのレジストリのセクションから設定が表示されます * * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DNS\Parameters\Zones\\<ZoneName>* * ### 構文```  
dnscmd [<ServerName>]/zoneinfo <ZoneName> [<Setting>。] ```  
#### Parameters  
**<ServerName>**  
IP アドレス、FQDN、またはホスト名によって表されるを管理する DNS サーバーを指定します。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
**<ZoneName>**  
ゾーンの名前を指定します。  
**<Setting>**  
個別にあるすべての設定を指定できます、 **zoneinfo**コマンドを返します。 設定を指定しない場合は、すべての設定が返されます。 ### 解説 -、 **zoneinfo**コマンドでは、レベルは、DNS ゾーンではレジストリ設定を表示します。 * * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DNS\Parameters\Zones\\<ZoneName>* *。 、サーバー レベルのレジストリ設定を表示するには使用、[情報](#BKMK_12)コマンド。 、このコマンドで表示できる設定の一覧を表示するには次を参照してください。、 [config](#BKMK_3)コマンド。 ### 例を参照してください[例 11。レジストリから RefreshInterval 設定を表示する](https://technet.microsoft.com/library/cc784399(v=ws.10).aspx)または[例 12。レジストリから設定をエージング表示](https://technet.microsoft.com/library/cc784399(v=ws.10).aspx)します。  
### <a name="BKMK_27"></a>dnscmd/zonepause  
クエリ要求を無視し、指定されたゾーンを一時停止します。 ### 構文```  
dnscmd [<ServerName>]/zonepause <ZoneName> ```  
#### Parameters  
**<ServerName>**  
IP アドレス、FQDN、またはホスト名によって表されるを管理する DNS サーバーを指定します。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
**<ZoneName>**  
一時停止するゾーンの名前を指定します。 ### ゾーンの再開しが一時停止された後に使用できるように、使用するには、解説 -、 [zoneresume](#BKMK_35)コマンド。 ### サンプルの使用法 `dnscmd dnssvr1.contoso.com /zonepause test.contoso.com`  
### <a name="BKMK_28"></a>dnscmd /zoneprint  
ゾーンのレコードを一覧表示します。 ### 構文```  
dnscmd [<ServerName>]/zoneprint <ZoneName> ```  
#### Parameters  
**<ServerName>**  
を管理する DNS サーバーの指定は、ローカル コンピューターの構文、IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
**<ZoneName>**  
一覧表示するゾーンを識別します。  
### <a name="BKMK_30"></a>dnscmd /zonerefresh  
セカンダリ DNS ゾーンをマスター ゾーンの更新を強制します。 ### 構文```  
dnscmd <ServerName>/zonerefresh <ZoneName> ```  
#### Parameters  
**<ServerName>**  
IP アドレス、FQDN、またはホスト名によって表されるを管理する DNS サーバーを指定します。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
**<ZoneName>**  
更新するゾーンの名前を指定します。 ### 解説 -、 **zonerefresh** authority (SOA) リソース レコードのマスター サーバーのスタートでは、バージョン番号のチェックを強制的にコマンド。 マスター サーバーのバージョン番号が、セカンダリ サーバーのバージョン番号よりも高い場合は、セカンダリ サーバーを更新するゾーンの転送が開始されます。 バージョン番号、同じである場合は、ゾーン転送は行われません。 -強制チェックは、15 分ごとで、既定で発生します。 既定値を変更するには、使用、 **dnscmd config refreshinterval**コマンド。 ### サンプルの使用法 `dnscmd dnssvr1.contoso.com /zonerefresh test.contoso.com`  
### <a name="BKMK_31"></a>dnscmd/zonereload  
コピーは、そのソースからの情報をゾーンです。 ### 構文```  
dnscmd <ServerName>/zonereload <ZoneName> ```  
#### Parameters  
**<ServerName>**  
IP アドレス、FQDN、またはホスト名によって表されるを管理する DNS サーバーを指定します。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
**<ZoneName>**  
再読み込みするゾーンの名前を指定します。 ### 解説 - ゾーンが active directory 統合の場合、AD DS から、再度読み込まれます。 -ファイルから、ゾーンが標準のファイルに格納されたゾーンの場合を再読み込みします。 ### サンプルの使用法 `dnscmd dnssvr1.contoso.com /zonereload test.contoso.com`  
### <a name="BKMK_32"></a>dnscmd/zoneresetmasters  
セカンダリ ゾーンのゾーン転送の情報を提供するマスター サーバーの IP アドレスをリセットします。 ### 構文```  
dnscmd <ServerName>/zoneresetmasters <ZoneName> []、[ローカル] [<IPaddress> [<IPaddress>]...] ```  
#### Parameters  
**<ServerName>**  
IP アドレス、FQDN、またはホスト名によって表されるを管理する DNS サーバーを指定します。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
**<ZoneName>**  
再読み込みするゾーンの名前を指定します。  
**/local**  
ローカル マスター一覧を設定します。 このパラメーターは、active directory 統合ゾーンに対して使用されます。  
**<IPaddress>**  
セカンダリ ゾーンのマスター サーバーの IP アドレス。 ### 解説 - この値はもともと、セカンダリ ゾーンの作成時に設定されます。 使用して、 **zoneresetmasters**セカンダリ サーバーでコマンド。 マスタ DNS サーバーで設定されている場合は、この値を指定しても効果はありません。 ### サンプルの使用法
<pre>dnscmd dnssvr1.contoso.com /zoneresetmasters test.contoso.com 10.0.0.1  
dnscmd dnssvr1.contoso.com /zoneresetmasters test.contoso.com /local</pre>  
### <a name="BKMK_33"></a>dnscmd /zoneresetscavengeservers  
指定されたゾーンの清掃を行うサーバーの IP アドレスを変更します。 ### 構文```  
dnscmd [<ServerName>]/zoneresetscavengeservers <ZoneName> [<IPaddress> [<IPaddress>]...] ```  
#### Parameters  
**<ServerName>**  
を管理する DNS サーバーの指定は、ローカル コンピューターの構文、IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
**<ZoneName>**  
清掃するゾーンを識別します。  
**<IPaddress>**  
清掃を行うを実行できるサーバーの IP アドレスを一覧表示します。 このパラメーターを省略した場合、このゾーンをホストするすべてのサーバーは、清掃を行うことができます。 ### 解説 - 既定では、ゾーンをホストするすべてのサーバーがそのゾーンの清掃を行います。 場合は、ゾーンは、1 つ以上の DNS サーバーでホストされているが、ゾーンの清掃回数を削減する、このコマンドを使用できます。 の DNS サーバーでこのコマンドによって影響を受けるゾーン清掃を有効にする必要があります。 ### サンプルの使用法 `dnscmd dnssvr1.contoso.com /zoneresetscavengeservers test.contoso.com 10.0.0.1 10.0.0.2`  
### <a name="BKMK_34"></a>dnscmd /zoneresetsecondaries  
ゾーン転送の要求時にマスター サーバーが応答するセカンダリ サーバーの IP アドレスの一覧を指定します。 ### 構文```  
dnscmd [<ServerName>]/zoneresetsecondaries <ZoneName> {/noxfr |/nonsecure |/securens |/securelist <SecurityIPaddresses>} {/nonotify | 通知/|/notifylist <NotifyIPaddresses>} ```  
#### Parameters  
**<ServerName>**  
IP アドレス、FQDN、またはホスト名によって表されるを管理する DNS サーバーを指定します。 場合、パラメーターを省略すると、ローカル サーバーが使用されます。  
**<ZoneName>**  
そのセカンダリ サーバーがゾーンの名前を示すをリセットします。  
**/noxfr | /nonsecure | /securens | /securelist <SecurityIPaddresses>**  
すべてまたは一部の更新を要求するセカンダリ サーバーのみが更新プログラムを取得するかどうかを指定します。  
**/noxfr**  
ゾーン転送が許可されないことを指定します。  
**/nonsecure**  
すべてのゾーン転送要求を許可されたことを指定します。  
**/securens**  
ゾーンのネーム サーバー (NS) リソース レコードに記載されているサーバーのみが転送を許可されているを指定します。  
**/securelist**  
サーバーの一覧にのみゾーン転送を許可されたことを指定します。 このパラメーターの後に、IP アドレスまたはマスター サーバーを使用するアドレスを指定する必要があります。  
**<SecurityIPaddresses>**  
マスター サーバーからゾーン転送を受信する IP アドレスを一覧表示します。 このパラメーターでのみ使用、 **/securelist**パラメーター。  
**/nonotify | /notify | /notifylist <NotifyIPaddresses>**  
特定のセカンダリ サーバーにのみ変更通知が送信されることを指定します。  
**/nonotify**  
セカンダリ サーバーに変更通知が送信されていないことを指定します。  
**/notify**  
すべてのセカンダリ サーバーへの変更通知が送信されることを指定します。  
**/notifylist**  
サーバーの一覧のみを変更通知が送信されることを指定します。 このコマンドの後に、IP アドレスまたはマスター サーバーを使用するアドレスを指定する必要があります。  
**<NotifyIPaddresses>**  
IP アドレスまたはまたは通知を送信する変更を複数のセカンダリ サーバーのアドレスを指定します。 この一覧でのみ使用、 **/notifylist**パラメーター。 ### 解説 - 使用、 **zoneresetsecondaries**コマンドをマスター サーバーへの応答方法ゾーン転送要求のセカンダリ サーバーからを指定します。 ### サンプルの使用法
<pre>dnscmd dnssvr1.contoso.com /zoneresetsecondaries test.contoso.com /noxfr /nonotify  
dnscmd dnssvr1.contoso.com /zoneresetsecondaries test.contoso.com /securelist 11.0.0.2</pre>  
### <a name="BKMK_29"></a>dnscmd /zoneresettype  
ゾーンの種類を変更します。 ### 構文```  
dnscmd [<ServerName>]/zoneresettype <ZoneName> <Zonetype> [//overwrite_mem |/overwrite_ds] ```  
#### Parameters  
**<ServerName>**  
を管理する DNS サーバーの指定は、ローカル コンピューターの構文、IP アドレス、FQDN、またはホスト名で表されます。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
**<ZoneName>**  
ゾーンの種類の変更を識別します。  
**<Zonetype>**  
作成するゾーンの種類を指定します。 各種類では、他の必要なパラメーターがあります。  
**/dsprimary**  
active directory 統合ゾーンを作成します。  
* */プライマリ/file <FileName>**  
標準プライマリ ゾーンを作成します。  
**/secondary <MasterIPaddress> [,<MasterIPaddress>...]**  
標準のゾーンのセカンダリを作成します。  
* */スタブ<MasterIPaddress>[、<MasterIPaddress>...] ファイル <FileName>**  
ファイルに格納されたスタブ ゾーンを作成します。  
**/dsstub <MasterIPaddress>[,<MasterIPaddress>...]**  
active directory 統合スタブ ゾーンを作成します。  
* */フォワーダー <MasterIPaddress[,<MasterIPaddress>].../ファイル<FileName>**  
作成されたゾーンが別の DNS サーバーに未解決のクエリを転送することを指定します。  
**/dsforwarder**  
作成した active directory 統合ゾーンが別の DNS サーバーに未解決のクエリを転送することを指定します。  
**/overwrite_mem | /overwrite_ds**  
既存のデータを上書きする方法を指定します。  
**/overwrite_mem**  
AD DS 内のデータから DNS データが上書きされます。  
**/overwrite_ds**  
AD DS の既存のデータを上書きします。 ### 解説 - ゾーン設定を入力として **/dsforwarder**条件付き転送を実行するゾーンを作成します。 ### サンプルの使用法
<pre>dnscmd dnssvr1.contoso.com /zoneresettype test.contoso.com /primary /file test.contoso.com.dns  
dnscmd dnssvr1.contoso.com /zoneresettype second.contoso.com /secondary 10.0.0.2</pre>  
### <a name="BKMK_35"></a>dnscmd/zoneresume  
一時停止されている指定されたゾーンを開始します。 ### 構文```  
dnscmd <ServerName>/zoneresume <ZoneName> ```  
#### Parameters  
**<ServerName>**  
IP アドレス、FQDN、またはホスト名によって表されるを管理する DNS サーバーを指定します。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
**<ZoneName>**  
再開するゾーンの名前を指定します。 ### Remarks - このオペレーションを使用するには逆に、 [zonepause](#BKMK_27)操作。 ### サンプルの使用法 `dnscmd dnssvr1.contoso.com /zoneresume test.contoso.com`  
### <a name="BKMK_36"></a>dnscmd/zoneupdatefromds  
AD DS から指定された active directory 統合ゾーンを更新します。 ### 構文```  
dnscmd <ServerName>/zoneupdatefromds <ZoneName> ```  
#### Parameters  
**<ServerName>**  
IP アドレス、FQDN、またはホスト名によって表されるを管理する DNS サーバーを指定します。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
**<ZoneName>**  
更新するゾーンの名前を指定します。 ### 解説 - active directory 統合ゾーン実行この更新プログラム既定で 5 分ごと。 このパラメーターを変更するには、使用、 **dnscmd config dspollinginterval**コマンド。 ### サンプルの使用法 `dnscmd dnssvr1.contoso.com /zoneupdatefromds`  
### <a name="BKMK_37"></a>dnscmd /zonewriteback  
指定されたゾーンに関連する変更の DNS サーバーのメモリをチェック、永続的ストレージに書き込みます。 ### 構文```  
dnscmd <ServerName>/zonewriteback <ZoneName> ```  
#### Parameters  
**<ServerName>**  
IP アドレス、FQDN、またはホスト名によって表されるを管理する DNS サーバーを指定します。 このパラメーターを省略した場合は、ローカル サーバーが使用されます。  
**<ZoneName>**  
更新するゾーンの名前を指定します。 ### 解説 - これは、ゾーン レベルの操作です。 DNS サーバー上のすべてのゾーンを更新することができます、 [writebackfiles](#BKMK_21)操作。 ### サンプルの使用法 `dnscmd dnssvr1.contoso.com /zonewriteback test.contoso.com`  
