---
title: nslookup
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 41516932-7833-434a-aa92-b4cf0f9a7ef7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b3c20855befbe71413fa8fdb44925b8b634c0c11
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841653"
---
# <a name="nslookup"></a>nslookup

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ドメイン ネーム システム (DNS) インフラストラクチャの診断に使用できる情報を表示します。 このツールを使用する前に、DNS の動作方法を理解する必要があります。 Nslookup コマンド ライン ツールは、TCP/IP プロトコルがインストールされている場合にのみ使用できます。
## <a name="syntax"></a>構文
```
nslookup [<-SubCommand ...>] [{<computerTofind> | -<Server>}]
nslookup /exit
nslookup /finger [<UserName>] [{[>] <FileName>|[>>] <FileName>}]
nslookup /{help | ?}
nslookup /ls [<Option>] <DNSDomain> [{[>] <FileName>|[>>] <FileName>}]
nslookup /lserver <DNSDomain> 
nslookup /root 
nslookup /server <DNSDomain>
nslookup /set <KeyWord>[=<Value>]
nslookup /set all 
nslookup /set class=<Class>
nslookup /set [no]d2
nslookup /set [no]debug
nslookup /set [no]defname
nslookup /set domain=<DomainName>
nslookup /set [no]ignore
nslookup /set port=<Port>
nslookup /set querytype=<ResourceRecordtype>
nslookup /set [no]recurse
nslookup /set retry=<Number>
nslookup /set root=<RootServer>
nslookup /set [no]search
nslookup /set srchlist=<DomainName>[/...]
nslookup /set timeout=<Number>
nslookup /set type=<ResourceRecordtype>
nslookup /set [no]vc
nslookup /view <FileName>
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[nslookup exit コマンド](nslookup-exit-command.md)|終了**nslookup**します。|
|[nslookup 指コマンド](nslookup-finger-command.md)|現在のコンピューターに本の指のサーバーに接続します。|
|[nslookup のヘルプ](nslookup-help.md)|簡単な概要を表示します。 **nslookup**サブコマンドします。|
|[nslookup %.*ls](nslookup-ls.md)|DNS ドメインの情報を一覧表示します。|
|[nslookup lserver](nslookup-lserver.md)|指定された DNS ドメインには、既定のサーバーを変更します。|
|[nslookup ルート](nslookup-root.md)|DNS ドメインの名前空間のルートのサーバーに既定のサーバーを変更します。|
|[nslookup サーバー](nslookup-server.md)|指定された DNS ドメインには、既定のサーバーを変更します。|
|[nslookup セット](nslookup-set.md)|影響する構成設定を変更する方法の参照関数。|
|[nslookup のすべての設定](nslookup-set-all.md)|構成設定の現在の値を出力します。|
|[nslookup set クラス](nslookup-set-class.md)|クエリ クラスを変更します。 クラスには、情報のプロトコルのグループを指定します。|
|[nslookup set d2](nslookup-set-d2.md)|完全なデバッグ モードを有効または無効にします。 すべてのパケットのすべてのフィールドが出力されます。|
|[nslookup デバッグの設定](nslookup-set-debug.md)|デバッグ モードを有効または無効にします。|
|nslookup /set defname|1 つのコンポーネント参照の要求には、既定の DNS ドメイン名を追加します。 1 つのコンポーネントは、ピリオドを含まないコンポーネントです。|
|[nslookup でドメインを設定](nslookup-set-domain.md)|既定の DNS ドメイン名を指定した名前に変更します。|
|nslookup /set ignore|パケット データ切り捨てによるエラーを無視します。|
|[nslookup ポートを設定します。](nslookup-set-port.md)|指定された値には、既定の TCP または UDP の DNS 名サーバー ポートを変更します。|
|[nslookup querytype を設定します。](nslookup-set-querytype.md)|クエリのリソース レコードの種類を変更します。|
|[nslookup recurse の設定](nslookup-set-recurse.md)|情報があるない場合は、他のサーバーを照会する DNS ネーム サーバーに指示します。|
|[nslookup 再試行の設定](nslookup-set-retry.md)|再試行の回数を設定します。|
|[nslookup ルートの設定](nslookup-set-root.md)|クエリに使用されるルート サーバーの名前を変更します。|
|[nslookup セットの検索](nslookup-set-search.md)|応答が受信されるまでは、ドメインの DNS 検索リスト内の DNS ドメイン名、要求に追加します。 これは、セット、検索要求を少なくとも 1 つのピリオドを含めるときに適用されますが、末尾のピリオドで終わらない。|
|[nslookup srchlist を設定します。](nslookup-set-srchlist.md)|既定の DNS ドメイン名と検索一覧を変更します。|
|[nslookup のタイムアウトを設定します。](nslookup-set-timeout.md)|初期要求に応答を待機する秒数を変更します。|
|[nslookup の種類を設定します。](nslookup-set-type.md)|クエリのリソース レコードの種類を変更します。|
|[nslookup set vc](nslookup-set-vc.md)|またはを使用して、サーバーへの要求を送信するときに、仮想回線を使用しないことを指定します。|
|[nslookup ビュー](nslookup-view.md)|並べ替えを前の出力を一覧表示 **%.*ls**サブコマンドまたはコマンド。|
## <a name="remarks"></a>注釈
-   場合*computerTofind* IP アドレスしクエリが A または PTR のリソース レコードの種類、コンピューターの名前が返されます。 場合*computerTofind*名前は、末尾期間、DNS ドメイン名が名前に追加の既定値はありません。 この動作は、次の状態によって異なります**設定**サブコマンド:**ドメイン**、 **srchlist**、 **defname**、および **。検索**します。
-   代わりにハイフン (-) を入力する場合*computerTofind*、コマンド プロンプトが変更**nslookup**対話型モード。
-   コマンドラインの長さは 256 文字未満である必要があります。
-   **nslookup**が 2 つのモード: 対話型と対話します。
    データの 1 つだけを検索する必要がある場合は、非対話型モードを使用します。 最初のパラメーターの名前または検索するコンピューターの IP アドレスを入力します。 2 番目のパラメーターの名前または名前の DNS サーバーの IP アドレスを入力します。 2 番目の引数を省略した場合**nslookup**既定の DNS ネーム サーバーを使用します。
    1 つ以上のデータを検索する必要がある場合は、対話型モードを使用できます。 最初のパラメーターと名前、または 2 番目のパラメーターの DNS ネーム サーバーの IP アドレスのハイフン (-) を入力します。 または、両方のパラメーターを省略し、 **nslookup**既定の DNS ネーム サーバーを使用します。 対話モードでの作業に関するヒントを次に示します。
    -   対話型コマンドをいつでもでも中断、CTRL キーを押しながら B キーを押します。
    -   終了するには次のように入力します。**終了**します。
    -   コンピューター名として組み込みのコマンドを処理する前に、エスケープ文字 (\\)。
    -   認識されないコマンドは、コンピューター名として解釈されます。
-   ルックアップ要求が失敗した場合、 **nslookup**エラー メッセージを出力します。 次の表には、考えられるエラー メッセージが一覧表示します。
    |**エラー メッセージ**|**説明**|
    |-----------|----------|
    |`timed out`|サーバーは、一定の時間と再試行回数の後に、要求に応答しませんでした。 タイムアウト期間を設定することができます、**タイムアウト設定**サブコマンドします。 再試行の回数を設定することができます、**セット再試行**サブコマンドします。|
    |`No response from server`|サーバー コンピューターの DNS ネーム サーバーが実行されていません。|
    |`No records`|DNS ネーム サーバーには、コンピューターの現在のクエリの種類のリソース レコードはありませんが、コンピューター名が無効です。 クエリの種類を指定した、**設定 querytype**コマンド。|
    |`Nonexistent domain`|コンピューター名または DNS ドメイン名が存在しません。|
    |`Connection refused`<br /><br />- または -<br /><br />`Network is unreachable`|DNS ネーム サーバーまたは本の指のサーバーへの接続を確立できませんでした。 このエラーは一般的に発生します **%.*ls**と**指**要求。|
    |`Server failure`|DNS ネーム サーバーは、そのデータベースの内部に矛盾を検出し、有効な応答を返しませんでした。|
    |`Refused`|DNS ネーム サーバーは、要求の処理を拒否されました。|
    |`format error`|DNS ネーム サーバーは、要求パケットの形式が正しくなかったことを検出します。 エラーの可能性が**nslookup**します。|
-   詳細については、 **nslookup**コマンドと DNS では、次のリソースを参照してください。
    -   Lee、T.、Davies、j.2000. *Microsoft Windows 2000 TCP/IP Protocols and Services のテクニカル リファレンス*します。 ワシントン州レドモンド:Microsoft のキーを押します。
    -   Albitz、P.、Loukides、M. C. Liu とします。 2001. *DNS および BIND、Fourth edition*します。 ◆ セグ:O ' reilly、associates、inc.
    -   Larson、M. C. Liu とします。 2001. *Windows 2000 で DNS*します。 ◆ セグ:O ' reilly、associates、inc.
#### <a name="examples"></a>例
各コマンドライン オプションは、コマンドの名前と、場合によっては、等号 (=)、および値ですぐに後にハイフン (-) で構成されます。 たとえば、ホスト (コンピューター) の情報や初期タイムアウトを 10 秒に既定のクエリの種類を変更する次のように入力します: **nslookup-querytype = hinfo-timeout = 10。**
## <a name="see-also"></a>関連項目
[コマンドライン構文キー](command-line-syntax-key.md)
