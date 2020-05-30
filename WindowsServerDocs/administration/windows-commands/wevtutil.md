---
title: wevtutil
description: Wevtutil のリファレンストピック。イベントログとパブリッシャーに関する情報を取得できます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d4c791e0-7e59-45c5-aa55-0223b77a4822
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 22195f3a163e1a4123b51d005b0367cc61411651
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222613"
---
# <a name="wevtutil"></a>wevtutil



イベント ログおよびパブリッシャーに関する情報を取得できます。 また、このコマンドを使用して、イベント マニフェストのインストールとアンインストールも実行できます。その他、クエリの実行や、ログのエクスポート、アーカイブ、消去も実行できます。

## <a name="syntax"></a>構文

```
wevtutil [{el | enum-logs}] [{gl | get-log} <Logname> [/f:<Format>]]
[{sl | set-log} <Logname> [/e:<Enabled>] [/i:<Isolation>] [/lfn:<Logpath>] [/rt:<Retention>] [/ab:<Auto>] [/ms:<MaxSize>] [/l:<Level>] [/k:<Keywords>] [/ca:<Channel>] [/c:<Config>]]
[{ep | enum-publishers}]
[{gp | get-publisher} <Publishername> [/ge:<Metadata>] [/gm:<Message>] [/f:<Format>]] [{im | install-manifest} <Manifest>]
[{um | uninstall-manifest} <Manifest>] [{qe | query-events} <Path> [/lf:<Logfile>] [/sq:<Structquery>] [/q:<Query>] [/bm:<Bookmark>] [/sbm:<Savebm>] [/rd:<Direction>] [/f:<Format>] [/l:<Locale>] [/c:<Count>] [/e:<Element>]]
[{gli | get-loginfo} <Logname> [/lf:<Logfile>]]
[{epl | export-log} <Path> <Exportfile> [/lf:<Logfile>] [/sq:<Structquery>] [/q:<Query>] [/ow:<Overwrite>]]
[{al | archive-log} <Logpath> [/l:<Locale>]]
[{cl | clear-log} <Logname> [/bu:<Backup>]] [/r:<Remote>] [/u:<Username>] [/p:<Password>] [/a:<Auth>] [/uni:<Unicode>]
```

### <a name="parameters"></a>パラメーター

|パラメーター|Description|
|---------|-----------|
|{el \| 列挙-ログ}|すべてのログの名前を表示します。|
|{gl \| 取得ログ} \<Logname>[/f: \<Format> ]|指定したログの構成情報を表示します。ログが有効になっているかどうか、ログの現在の最大サイズ制限、およびログが保存されているファイルへのパスが含まれます。|
|{sl \| 設定-ログ} \<Logname>[/e: \<Enabled> ][/i: \<Isolation> ][/lfn: \<Logpath> ][/rt: \<Retention> ][/ab: \<Auto> ][/ミリ秒: \<MaxSize> ][/l: \<Level> ][/k: \<Keywords> ][/ca: \<Channel> ][/c: \<Config> ]|指定されたログの構成を変更します。|
|{ep \| 列挙型-パブリッシャー}|ローカルコンピューター上のイベント発行元を表示します。|
|{gp \| 取得-パブリッシャー} \<Publishername>[/ge: \<Metadata> ][/gm: \<Message> ][/f: \<Format> ]]|指定したイベント発行元の構成情報を表示します。|
|{im \| インストールマニフェスト}\<Manifest>|マニフェストからイベントパブリッシャーとログをインストールします。 イベントマニフェストとこのパラメーターの使用の詳細については、Microsoft 開発者ネットワーク (MSDN) の Web サイト () にある Windows イベントログ SDK を参照してください [https://msdn.microsoft.com](https://msdn.microsoft.com) 。|
|{um \| アンインストールマニフェスト}\<Manifest>|マニフェストからすべての発行元とログをアンインストールします。 イベントマニフェストとこのパラメーターの使用の詳細については、Microsoft 開発者ネットワーク (MSDN) の Web サイト () にある Windows イベントログ SDK を参照してください [https://msdn.microsoft.com](https://msdn.microsoft.com) 。|
|{qe \| } \<Path>[/lf: \<Logfile> ][/sq: \<Structquery> ][/q: \<Query> ][/bm: \<Bookmark> ][/sbm: \<Savebm> ][/rd: \<Direction> ][/f: \<Format> ][/l: \<Locale> ][/c: \<Count> ][/e: \<Element> ]|イベントログ、ログファイル、または構造化されたクエリを使用して、イベントを読み取ります。 既定では、のログ名を指定し \<Path> ます。 ただし、 **/lf**オプションを使用する場合、は \<Path> ログファイルへのパスである必要があります。 **/Sq**パラメーターを使用する場合、は \<Path> 構造化クエリを含むファイルへのパスである必要があります。|
|{gli \| get-loginfo} \<Logname>[/lf: \<Logfile> ]|イベントログまたはログファイルに関するステータス情報を表示します。 **/Lf**オプションが使用されている場合、 \<Logname> はログファイルへのパスです。 **Wevtutil el**を実行すると、ログ名の一覧を取得できます。|
|{epl \| export-log} \<Path> \<Exportfile>[/lf: \<Logfile> ][/sq: \<Structquery> ][/q: \<Query> ][/ow: \<Overwrite> ]|イベントログ、ログファイル、または構造化されたクエリを使用して、指定したファイルにイベントをエクスポートします。 既定では、のログ名を指定し \<Path> ます。 ただし、 **/lf**オプションを使用する場合、は \<Path> ログファイルへのパスである必要があります。 **/Sq**オプションを使用する場合、は \<Path> 構造化クエリを含むファイルへのパスである必要があります。 \<Exportfile>エクスポートされたイベントを格納するファイルへのパスを指定します。|
|{al \| アーカイブ-ログ} \<Logpath>[/l: \<Locale> ]|指定されたログファイルを自己完結型の形式でアーカイブします。 ロケールの名前を持つサブディレクトリが作成され、ロケール固有のすべての情報がそのサブディレクトリに保存されます。 **Wevtutil al**を実行してディレクトリとログファイルを作成した後は、パブリッシャーがインストールされているかどうかにかかわらず、ファイル内のイベントを読み取ることができます。|
|{cl \| 消去ログ} \<Logname> [/bu: \<Backup> ]|指定したイベント ログのイベントを消去します。 **/Bu**オプションを使用すると、消去されたイベントをバックアップできます。|

## <a name="options"></a>オプション

|       オプション       |                                                                                                                                                                                                                                                                 説明                                                                                                                                                                                                                                                                  |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /f\<Format>    |                                                                                                                                                               出力を XML 形式またはテキスト形式のいずれかに指定します。 \<Format>が xml の場合、出力は xml 形式で表示されます。 \<Format>が Text の場合、出力は XML タグなしで表示されます。 既定値は Text です。                                                                                                                                                                |
|   /e:\<Enabled>    |                                                                                                                                                                                                                                         ログを有効または無効にします。 \<Enabled>true または false を指定できます。                                                                                                                                                                                                                                          |
|  /i\<Isolation>   | ログ分離モードを設定します。 \<Isolation>システム、アプリケーション、またはカスタムにすることができます。 ログの分離モードは、ログが同じ分離クラスの他のログとセッションを共有するかどうかを決定します。 システムの分離を指定した場合、ターゲットログは少なくともシステムログとの書き込みアクセス許可を共有します。 アプリケーションの分離を指定した場合、ターゲットログは、少なくともアプリケーションログで書き込みアクセス許可を共有します。 カスタム分離を指定する場合は、 **/ca**オプションを使用してセキュリティ記述子を指定する必要もあります。 |
|  /lfn:\<Logpath>   |                                                                                                                                                                                                           ログファイル名を定義します。 \<Logpath>は、イベントログサービスがこのログのイベントを格納するファイルへの完全パスです。                                                                                                                                                                                                           |
|  rt\<Retention>  |                                                            ログの保持モードを設定します。 \<Retention>true または false を指定できます。 ログの保持モードは、ログが最大サイズに達したときのイベントログサービスの動作を決定します。 イベントログが最大サイズに達し、ログ保持モードが true の場合、既存のイベントは保持され、受信イベントは破棄されます。 ログの保持モードが false の場合、受信イベントはログ内の最も古いイベントを上書きします。                                                             |
|    l\<Auto>     |                                                                                                                                   ログの自動バックアップポリシーを指定します。 \<Auto>true または false を指定できます。 この値が true の場合、ログは最大サイズに達したときに自動的にバックアップされます。 この値が true の場合は、 **/rt**オプションで指定された保有期間も true に設定する必要があります。                                                                                                                                    |
|   orm\<MaxSize>   |                                                                                                                                                                        ログの最大サイズをバイト単位で設定します。 最小ログサイズは1048576バイト (1024 KB) であり、ログファイルは常に 64 KB の倍数であるため、入力した値はそれに応じて丸められます。                                                                                                                                                                         |
|    /l:\<Level>     |                                                                                                                                                                     ログのレベルフィルターを定義します。 \<Level>任意の有効なレベル値を指定できます。 このオプションは、専用セッションを使用するログにのみ適用できます。 レベルフィルターを削除するには、 <Level> を0に設定します。                                                                                                                                                                      |
|   /k\<Keywords>   |                                                                                                                                                                                         ログのキーワードフィルターを指定します。 \<Keywords>有効な64ビットキーワードマスクを指定できます。 このオプションは、専用セッションを使用するログにのみ適用できます。                                                                                                                                                                                         |
|   /ca\<Channel>   |                                                                                                                   イベントログのアクセス許可を設定します。 \<Channel>は、セキュリティ記述子定義言語 (SDDL) を使用するセキュリティ記述子です。 SDDL 形式の詳細については、Microsoft 開発者ネットワーク (MSDN) の Web サイト () を参照してください [https://msdn.microsoft.com](https://msdn.microsoft.com) 。                                                                                                                    |
|    スイッチ\<Config>    |                                                                                                                                  構成ファイルへのパスを指定します。 このオプションを選択すると、で定義されている構成ファイルからログのプロパティが読み取られ \<Config> ます。 このオプションを使用する場合は、パラメーターを指定しないでください <Logname> 。 ログ名は構成ファイルから読み取られます。                                                                                                                                   |
|  /ge\<Metadata>   |                                                                                                                                                                                                                 このパブリッシャーによって発生する可能性のあるイベントのメタデータ情報を取得します。 \<Metadata>true または false を指定できます。                                                                                                                                                                                                                 |
|   /gm\<Message>   |                                                                                                                                                                                                                       数値メッセージ ID ではなく、実際のメッセージを表示します。 \<Message>true または false を指定できます。                                                                                                                                                                                                                        |
|   lf\<Logfile>   |                                                                                                                                                                                  イベントをログまたはログファイルから読み取ることを指定します。 \<Logfile>true または false を指定できます。 True の場合、コマンドのパラメーターはログファイルへのパスです。                                                                                                                                                                                   |
| /sq\<Structquery> |                                                                                                                                                                                構造化されたクエリを使用してイベントを取得することを指定します。 \<Structquery>true または false を指定できます。 True の場合、 <Path> は構造化クエリを含むファイルへのパスです。                                                                                                                                                                                |
|    /q\<Query>     |                                                                                                                                                                     読み取りまたはエクスポートされたイベントをフィルター処理するための XPath クエリを定義します。 このオプションが指定されていない場合は、すべてのイベントが返されるか、エクスポートされます。 このオプションは、 **/sq**が true の場合は使用できません。                                                                                                                                                                     |
|  bm.exe\<Bookmark>   |                                                                                                                                                                                                                                 前のクエリのブックマークを含むファイルへのパスを指定します。                                                                                                                                                                                                                                 |
|   /sbm:\<Savebm>   |                                                                                                                                                                                                             このクエリのブックマークを保存するために使用されるファイルへのパスを指定します。 ファイル名拡張子は .xml にする必要があります。                                                                                                                                                                                                              |
|  /rd\<Direction>  |                                                                                                                                                                                                   イベントを読み取る方向を指定します。 \<Direction>true または false を指定できます。 True の場合、最新のイベントが最初に返されます。                                                                                                                                                                                                   |
|    /l:\<Locale>    |                                                                                                                                                                                          特定のロケールでイベントテキストを出力するために使用されるロケール文字列を定義します。 **/F**オプションを使用してテキスト形式でイベントを出力する場合にのみ使用できます。                                                                                                                                                                                          |
|    スイッチ\<Count>     |                                                                                                                                                                                                                                                  読み取るイベントの最大数を設定します。                                                                                                                                                                                                                                                  |
|   /e:\<Element>    |                                                                                                                                                           XML でイベントを表示するときに、ルート要素を含めます。 \<Element>は、ルート要素内に必要な文字列です。 たとえば、 **/e: root**は、ルート要素のペアを含む XML になり \<root> </root> ます。                                                                                                                                                            |
|  /ow\<Overwrite>  |                                                                                                                                                                 エクスポートファイルを上書きすることを指定します。 \<Overwrite>true または false を指定できます。 True の場合、で指定したエクスポートファイルが <Exportfile> 既に存在すると、確認なしで上書きされます。                                                                                                                                                                 |
|   bu\<Backup>    |                                                                                                                                                                                                      消去されたイベントが格納されるファイルへのパスを指定します。 バックアップファイルの名前には、.evtx 拡張子を含めます。                                                                                                                                                                                                       |
|    r\<Remote>    |                                                                                                                                                                                            リモートコンピューターでコマンドを実行します。 \<Remote>リモートコンピューターの名前を指定します。 **Im**および**um**パラメーターでは、リモート操作はサポートされていません。                                                                                                                                                                                            |
|   /u\<Username>   |                                                                                                                                                                          リモートコンピューターにログオンするための別のユーザーを指定します。 \<Username>ドメイン \ ユーザーまたはユーザーの形式でユーザー名を指定します。 このオプションは、 **/r**オプションが指定されている場合にのみ適用されます。                                                                                                                                                                          |
|   /p\<Password>   |                                                                                                                                               ユーザーのパスワードを指定します。 **/U**オプションを使用していて、このオプションが指定されていない場合 \<Password> 、またはの場合 *、ユーザーはパスワードの入力を求められます。このオプションは、 \* \* /u オプションが指定されている場合にのみ適用さ*れ \* ます。                                                                                                                                                |
|     /a\<Auth>     |                                                                                                                                                                                             リモートコンピューターに接続するための認証の種類を定義します。 \<Auth>既定値、Negotiate、Kerberos、NTLM のいずれかを指定できます。 既定値は Negotiate です。                                                                                                                                                                                              |
|  方向\<Unicode>   |                                                                                                                                                                                                             Unicode で出力を表示します。 \<Unicode>true または false を指定できます。 <Unicode>が true の場合、出力は Unicode になります。                                                                                                                                                                                                             |

## <a name="remarks"></a>解説

-   構成ファイルを sl パラメーターと共に使用する

    構成ファイルは、wevtutil gl/f: xml の出力と同じ形式の XML ファイルです \<Logname> 。 リテンション期間を有効にする構成ファイルの形式を表示するには、自動バックアップを有効にし、アプリケーションログの最大ログサイズを設定します。
    ```
    <?xml version=1.0 encoding=UTF-8?>
    <channel name=Application isolation=Application
    xmlns=https://schemas.microsoft.com/win/2004/08/events>
    <logging>
    <retention>true</retention>
    <autoBackup>true</autoBackup>
    <maxSize>9000000</maxSize>
    </logging>
    <publishing>
    </publishing>
    </channel>
    ```

## <a name="examples"></a>例

すべてのログの名前を一覧表示します。
```
wevtutil el
```
ローカルコンピューター上のシステムログに関する構成情報を XML 形式で表示します。
```
wevtutil gl System /f:xml
```
構成ファイルを使用してイベントログ属性を設定します (構成ファイルの例については、「解説」を参照してください)。
```
wevtutil sl /c:config.xml
```
発行元が発生させるイベントに関するメタデータを含む、Microsoft-Windows イベント発行者に関する情報を表示します。
```
wevtutil gp Microsoft-Windows-Eventlog /ge:true
```
MyManifest xml マニフェストファイルから発行元とログをインストールします。
```
wevtutil im myManifest.xml
```
MyManifest .xml マニフェストファイルから発行元とログをアンインストールします。
```
wevtutil um myManifest.xml
```
アプリケーションログの最新の3つのイベントをテキスト形式で表示します。
```
wevtutil qe Application /c:3 /rd:true /f:text
```
アプリケーションログの状態を表示します。
```
wevtutil gli Application
```
システムログから C:\backup\system0506.evtx にイベントをエクスポートします。
```
wevtutil epl System C:\backup\system0506.evtx
```
C:\admin\backups\a10306.evtx に保存した後、アプリケーションログからすべてのイベントを消去します。
```
wevtutil cl Application /bu:C:\admin\backups\a10306.evtx
```

#### <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
