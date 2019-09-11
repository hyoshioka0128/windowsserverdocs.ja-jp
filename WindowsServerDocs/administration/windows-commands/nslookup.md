---
title: nslookup
description: 'Windows コマンドに関するトピック * * * *- '
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
ms.openlocfilehash: 84e3e9ee920f458ca775dd7b76d892f10ba2f992
ms.sourcegitcommit: ee8e0b217be6f6b2532ee7265fb4be00c106e124
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70878117"
---
# <a name="nslookup"></a>nslookup

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ドメインネームシステム (DNS) インフラストラクチャの診断に使用できる情報を表示します。 このツールを使用する前に、DNS のしくみについて理解しておく必要があります。 Nslookup コマンドラインツールは、TCP/IP プロトコルがインストールされている場合にのみ使用できます。
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

|                       パラメーター                       |                                                                                                         説明                                                                                                         |
|-------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   [nslookup exit コマンド](nslookup-exit-command.md)   |                                                                                                     **Nslookup**を終了します。                                                                                                     |
| [nslookup finger コマンド](nslookup-finger-command.md) |                                                                                  現在のコンピューター上の finger サーバーに接続します。                                                                                   |
|           [nslookup help](nslookup-help.md)           |                                                                                    **Nslookup**サブコマンドの簡単な概要を表示します。                                                                                    |
|             [nslookup ls](nslookup-ls.md)             |                                                                                             DNS ドメインの情報を一覧表示します。                                                                                             |
|        [nslookup lserver](nslookup-lserver.md)        |                                                                                   指定された DNS ドメインに既定のサーバーを変更します。                                                                                   |
|           [nslookup root](nslookup-root.md)           |                                                                     DNS ドメイン名空間のルートに対して、既定のサーバーをサーバーに変更します。                                                                     |
|         [nslookup server](nslookup-server.md)         |                                                                                   指定された DNS ドメインに既定のサーバーを変更します。                                                                                   |
|            [nslookup set](nslookup-set.md)            |                                                                              参照の機能に影響する構成設定を変更します。                                                                               |
|        [nslookup set all](nslookup-set-all.md)        |                                                                                  構成設定の現在の値を出力します。                                                                                   |
|      [nslookup set class](nslookup-set-class.md)      |                                                                     クエリクラスを変更します。 クラスは、情報のプロトコルグループを指定します。                                                                     |
|         [nslookup set d2](nslookup-set-d2.md)         |                                                                     完全デバッグモードをオンまたはオフにします。 すべてのパケットのすべてのフィールドが出力されます。                                                                      |
|      [nslookup set debug](nslookup-set-debug.md)      |                                                                                               デバッグモードをオンまたはオフにします。                                                                                               |
|                 nslookup/set defname                 |                                            単一のコンポーネント参照要求に既定の DNS ドメイン名を追加します。 1つのコンポーネントは、ピリオドを含まないコンポーネントです。                                            |
|     [nslookup set domain](nslookup-set-domain.md)     |                                                                                 既定の DNS ドメイン名を、指定された名前に変更します。                                                                                  |
|                 nslookup/set ignore                  |                                                                                              パケットの切り捨てエラーを無視します。                                                                                              |
|       [nslookup set port](nslookup-set-port.md)       |                                                                          既定の TCP/UDP DNS ネームサーバーポートを、指定された値に変更します。                                                                           |
|  [nslookup set querytype](nslookup-set-querytype.md)  |                                                                                       クエリのリソースレコードの種類を変更します。                                                                                       |
|    [nslookup set recurse](nslookup-set-recurse.md)    |                                                                    DNS ネームサーバーに情報がない場合に他のサーバーを照会するように指示します。                                                                    |
|      [nslookup set retry](nslookup-set-retry.md)      |                                                                                                 再試行回数を設定します。                                                                                                 |
|       [nslookup set root](nslookup-set-root.md)       |                                                                                    クエリに使用するルートサーバーの名前を変更します。                                                                                    |
|     [nslookup set search](nslookup-set-search.md)     | 応答が受信されるまで、DNS ドメインの検索リスト内の DNS ドメイン名を要求に追加します。 これは、セットと参照要求に少なくとも1つのピリオドが含まれている場合に適用されますが、末尾にピリオドは付きません。 |
|   [nslookup set srchlist](nslookup-set-srchlist.md)   |                                                                                    既定の DNS ドメイン名と検索一覧を変更します。                                                                                     |
|    [nslookup set timeout](nslookup-set-timeout.md)    |                                                                           要求への応答を待機する秒数の初期値を変更します。                                                                           |
|       [nslookup set type](nslookup-set-type.md)       |                                                                                       クエリのリソースレコードの種類を変更します。                                                                                       |
|         [nslookup set vc](nslookup-set-vc.md)         |                                                                     サーバーに要求を送信するときに、仮想回線を使用するかどうかを指定します。                                                                      |
|           [nslookup view](nslookup-view.md)           |                                                                          前の**ls**サブコマンドの出力を並べ替えて一覧表示します。                                                                          |

## <a name="remarks"></a>コメント
- *ComputerTofind*が IP アドレスであり、クエリが A または PTR リソースレコードの種類の場合は、コンピューターの名前が返されます。 *ComputerTofind*が名前で、末尾のピリオドがない場合は、既定の DNS ドメイン名が名前に追加されます。 この動作は、 **set**サブコマンド ( **domain**、 **srchlist**、 **defname**、および**search**) の状態によって異なります。
- *ComputerTofind*の代わりにハイフン (-) を入力すると、コマンドプロンプトが**nslookup**対話モードに変更されます。
- コマンドラインの長さは256文字未満でなければなりません。
- **nslookup**には、対話型と非対話の2つのモードがあります。
  1つのデータだけを検索する必要がある場合は、非対話モードを使用します。 最初のパラメーターとして、検索するコンピューターの名前または IP アドレスを入力します。 2番目のパラメーターには、DNS ネームサーバーの名前または IP アドレスを入力します。 2番目の引数を省略した場合、 **nslookup**では既定の DNS ネームサーバーが使用されます。
  複数のデータを検索する必要がある場合は、対話モードを使用できます。 最初のパラメーターとしてハイフン (-) を入力し、2番目のパラメーターに DNS ネームサーバーの名前または IP アドレスを入力します。 または、両方のパラメーターを省略**すると、** 既定の DNS ネームサーバーが使用されます。 対話モードでの作業に関するヒントを次に示します。
  -   対話型コマンドを中断するには、CTRL + B キーを押します。
  -   終了するには、「 **exit**」と入力します。
  -   組み込みコマンドをコンピューター名として扱うには、その前にエスケープ文字 (\\) を付けます。
  -   認識されないコマンドは、コンピューター名として解釈されます。
- 参照要求が失敗した場合は、 **nslookup**によってエラーメッセージが出力されます。 次の表に、考えられるエラーメッセージを示します。
  |**エラーメッセージ**|**[説明]**|
  |-----------|----------|
  |`timed out`|サーバーは、一定の時間が経過してから特定の回数の再試行を行った後に、要求に応答しませんでした。 タイムアウト期間は、 **set timeout**サブコマンドを使用して設定できます。 再試行の回数は、 **set retry**サブコマンドを使用して設定できます。|
  |`No response from server`|サーバーコンピューターで DNS ネームサーバーが実行されていません。|
  |`No records`|DNS ネームサーバーには、コンピューターの現在のクエリの種類のリソースレコードがありません。ただし、コンピューター名は有効です。 クエリの種類は、 **set querytype**コマンドを使用して指定します。|
  |`Nonexistent domain`|コンピューター名または DNS ドメイン名が存在しません。|
  |`Connection refused`<br /><br />\- または -<br /><br />`Network is unreachable`|DNS ネームサーバーまたはフィンガーサーバーへの接続を確立できませんでした。 このエラーは、通常、 **ls**および**finger**要求で発生します。|
  |`Server failure`|DNS ネームサーバーがデータベース内で内部の不整合を検出したため、有効な回答を返すことができませんでした。|
  |`Refused`|DNS ネームサーバーが要求の処理を拒否しました。|
  |`format error`|DNS ネームサーバーで、要求パケットの形式が正しくないことが検出されました。 **Nslookup**でエラーが発生している可能性があります。|
- **Nslookup**コマンドと DNS の詳細については、次のリソースを参照してください。
  - Lee、T.、Davies、J。2000。 *Microsoft Windows 2000 Tcp/ip プロトコルおよびサービスに関するテクニカルリファレンス*。 ワシントン州レドモンド:Microsoft Press。
  - Albitz、P.、Loukides、m.、および c. Liu。 2001。 *DNS と BIND、第4版*。 カリフォルニア州 Sebastopol:O'Reilly と関連, Inc.
  - Larson、m.、および c. Liu。 2001。 *Windows 2000 の DNS*。 カリフォルニア州 Sebastopol:O'Reilly と関連, Inc.
    #### <a name="examples"></a>使用例
    各コマンドラインオプションは、ハイフン (-) の直後にコマンド名を入力し、場合によっては等号 (=) と値を指定します。 たとえば、既定のクエリの種類をホスト (コンピューター) 情報に変更し、初期タイムアウトを10秒に変更するには、「 **nslookup-querytype = hinfo-timeout = 10** 」と入力します。
    ## <a name="see-also"></a>関連項目
    [コマンド ライン構文の記号](command-line-syntax-key.md)
