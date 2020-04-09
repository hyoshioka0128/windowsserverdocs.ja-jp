---
title: wecutil
description: 「Wecutil の Windows コマンドに関するトピックでは、リモートコンピューターから転送されるイベントのサブスクリプションを作成および管理できます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0c82a6cb-d652-429c-9c3d-0f568c78d54b
author: coreyp-at-msft
ms.author: coreyp
manager: dansimps
ms.openlocfilehash: 2bb397ace7cc99c8b8d6bbed3598346ff2d0801c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80829440"
---
# <a name="wecutil"></a>wecutil



リモートコンピューターから転送されるイベントのサブスクリプションを作成および管理できます。 リモートコンピューターは、WS-MANAGEMENT プロトコルをサポートしている必要があります。 このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。


## <a name="syntax"></a>構文

```
wecutil  [{es | enum-subscription}] 
[{gs | get-subscription} <Subid> [/f:<Format>] [/uni:<Unicode>]] 
[{gr | get-subscriptionruntimestatus} <Subid> [<Eventsource> …]] 
[{ss | set-subscription} [<Subid> [/e:[<Subenabled>]] [/esa:<Address>] [/ese:[<Srcenabled>]] [/aes] [/res] [/un:<Username>] [/up:<Password>] [/d:<Desc>] [/uri:<Uri>] [/cm:<Configmode>] [/ex:<Expires>] [/q:<Query>] [/dia:<Dialect>] [/tn:<Transportname>] [/tp:<Transportport>] [/dm:<Deliverymode>] [/dmi:<Deliverymax>] [/dmlt:<Deliverytime>] [/hi:<Heartbeat>] [/cf:<Content>] [/l:<Locale>] [/ree:[<Readexist>]] [/lf:<Logfile>] [/pn:<Publishername>] [/essp:<Enableport>] [/hn:<Hostname>] [/ct:<Type>]] [/c:<Configfile> [/cun:<Username> /cup:<Password>]]] 
[{cs | create-subscription} <Configfile> [/cun:<Username> /cup:<Password>]] 
[{ds | delete-subscription} <Subid>] 
[{rs | retry-subscription} <Subid> [<Eventsource>…]] 
[{qc | quick-config} [/q:[<Quiet>]]].
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|{es \| 列挙型-サブスクリプション}|存在するすべてのリモートイベントサブスクリプションの名前が表示されます。|
|{gs \| サブスクリプションの取得} \<Subid > [/f:\<形式 >] [/uni:\<Unicode >]|リモートサブスクリプションの構成情報を表示します。 \<Subid > は、サブスクリプションを一意に識別する文字列です。 \<Subid > は、サブスクリプションの作成に使用された XML 構成ファイルの \<SubscriptionId > タグで指定した文字列と同じです。|
|{gr \| get-subscriptionruntimestatus} \<Subid > [\<Eventsource >...]|サブスクリプションのランタイムの状態を表示します。 \<Subid > は、サブスクリプションを一意に識別する文字列です。 \<Subid > は、サブスクリプションの作成に使用された XML 構成ファイルの \<SubscriptionId > タグで指定した文字列と同じです。 \<Eventsource > は、イベントのソースとして機能するコンピューターを識別する文字列です。 Eventsource > \<、完全修飾ドメイン名、NetBIOS 名、または IP アドレスにする必要があります。|
|{ss \| set-subscription} \<Subid > [/e: [\<Subid >]] [/esa:\<アドレス >] [/ese: [\<Srcenabled >]] [/aes] [/res] [/un:\<パスワード >] [/d:\<Desc >] [/uri:\<Uri >] [/:\<Configmode >] [/ex:\<有効期限 >] [/q:\<のクエリ >] [/dia:\<言語 >] [/tn:\<Net-transportname >] [/tp:\<Transportport >] [/dm:\<Deliverymode >] [/dmi:\<deliverymode >] [/] [/のハートビート\<] [/cf: > コンテンツ\<] [/l:\<Locale >] [//lf: [\<Readexist >]] [:\<Logfile >] [/pn:\<Publishername >] [/essp:\<Enableport >] [///ホスト名\<] [/ct: > 型\<]\<\<</br>または</br>{ss \| set-subscription/c:\<Configfile > [/cun:\<Comusername >/カップ:\<Compassword >]|サブスクリプションの構成を変更します。 サブスクリプション ID と、サブスクリプションパラメーターを変更するための適切なオプションを指定できます。また、XML 構成ファイルを指定してサブスクリプションパラメーターを変更することもできます。|
|{cs \| 作成-サブスクリプション} \<Configfile > [/cun:\<ユーザー名 >/カップ:\<パスワード >]|リモートサブスクリプションを作成します。 \<Configfile > は、サブスクリプション構成を含む XML ファイルへのパスを指定します。 絶対パスまたは現在のディレクトリを基準とした相対パスを指定できます。|
|{ds \| 削除-サブスクリプション} \<Subid >|サブスクリプションのイベントログにイベントを配信するすべてのイベントソースからサブスクリプションとアンサブスクライブを削除します。 既に受信してログに記録されているイベントは削除されません。 \<Subid > は、サブスクリプションを一意に識別する文字列です。 \<Subid > は、サブスクリプションの作成に使用された XML 構成ファイルの \<SubscriptionId > タグで指定した文字列と同じです。|
|{rs \| 再試行-サブスクリプション} \<Subid > [\<Eventsource >...]|接続の確立を再試行し、アクティブでないサブスクリプションにリモートサブスクリプション要求を送信します。 すべてのイベントソースまたは指定されたイベントソースの再アクティブ化を試みます。 無効なソースは再試行されません。 \<Subid > は、サブスクリプションを一意に識別する文字列です。 \<Subid > は、サブスクリプションの作成に使用された XML 構成ファイルの \<SubscriptionId > タグで指定した文字列と同じです。 \<Eventsource > は、イベントのソースとして機能するコンピューターを識別する文字列です。 Eventsource > \<、完全修飾ドメイン名、NetBIOS 名、または IP アドレスにする必要があります。|
|{qc \| のクイック構成}[/q: [\<Quiet >]]|Windows イベントコレクターサービスを構成して、再起動によってサブスクリプションが作成され、維持されるようにします。 これには、次の手順が含まれます。</br>1. ForwardedEvents チャネルが無効になっている場合は有効にします。</br>2. 開始を遅延するように Windows イベントコレクターサービスを設定します。</br>3. Windows イベントコレクターサービスが実行されていない場合は、開始します。|

## <a name="options"></a>オプション

|オプション|説明|
|------|-----------|
|/f:\<形式 >|表示される情報の形式を指定します。 \<形式 > は XML または簡潔にすることができます。 <Format> が XML の場合、出力は XML 形式で表示されます。 \<形式 > が簡潔な場合、出力は名前と値のペアで表示されます。 既定値は簡潔です。|
|/c:\<Configfile >|サブスクリプション構成を含む XML ファイルへのパスを指定します。 絶対パスまたは現在のディレクトリを基準とした相対パスを指定できます。 このオプション**は、その他のオプション**と同時に使用 **/cup**することはできません。|
|/e: [\<Subenabled >]|サブスクリプションを有効または無効にします。 \<Subenabled > は true または false にすることができます。 このオプションの既定値は true です。|
|/esa:\<アドレス >|イベントソースのアドレスを指定します。 \<アドレス > は、完全修飾ドメイン名、NetBIOS 名、またはイベントのソースとして機能するコンピューターを識別する IP アドレスを含む文字列です。 このオプションは、 **/ese**、 **/aes**、 **/res**、/ **un** 、および/ **up**オプションと共に使用してください。|
|/ese: [\<Srcenabled >]|イベントソースを有効または無効にします。 \<Srcenabled > には、true または false を指定できます。 このオプションは、 **/esa**オプションが指定されている場合にのみ使用できます。 このオプションの既定値は true です。|
|/aes|サブスクリプションにまだ含まれていない場合は、 **/esa**オプションで指定されたイベントソースを追加します。 **/Esa**オプションで指定されたアドレスが既にサブスクリプションの一部である場合は、エラーが報告されます。 このオプションは、 **/esa**オプションが指定されている場合にのみ使用できます。|
|/res|サブスクリプションに既に含まれている場合は、 **/esa**オプションによって指定されたイベントソースを削除します。 **/Esa**オプションで指定されたアドレスがサブスクリプションの一部ではない場合は、エラーが報告されます。 このオプションは、 **/esa**オプションが指定されている場合にのみ使用できます。|
|/un:\<ユーザー名 >|**/Esa**オプションで指定されたイベントソースで使用するユーザー資格情報を指定します。 このオプションは、 **/esa**オプションが指定されている場合にのみ使用できます。|
|/up:\<パスワード >|ユーザー資格情報に対応するパスワードを指定します。 このオプションは、 **/un**オプションが指定されている場合にのみ使用できます。|
|/d:\<Desc >|サブスクリプションの説明を提供します。|
|/uri:\<Uri >|サブスクリプションによって使用されるイベントの種類を指定します。 \<Uri > には、イベントのソースを一意に識別するために、イベントソースコンピューターのアドレスと組み合わせて使用される URI 文字列が含まれています。 URI 文字列は、サブスクリプション内のすべてのイベントソースアドレスに使用されます。|
|/cm:\<Configmode >|構成モードを設定します。 \<Configmode > には、通常、カスタム、MinLatency、Minlatency 幅のいずれかの文字列を指定できます。 通常、MinLatency、および Minlatency 幅モードでは、配信モード、配信の最大項目数、ハートビート間隔、配信の最大待機時間を設定します。 構成モードが "カスタム" に設定されている場合にのみ、/ **dm**、/ **dmi**、/ **hi** 、/ **dmlt**オプションを指定できます。|
|/ex:\<の有効期限 >|サブスクリプションの有効期限が切れる時刻を設定します。 \<の有効 > 期限は、標準 XML または Yyyy-mm-ddthh: MM: ss [. sss] [Z] の形式で定義する必要があります。ここで T は時刻の区切り記号で、Z は UTC 時刻を示します。|
|/q: クエリの > を\<|サブスクリプションのクエリ文字列を指定します。 \<クエリの > 形式は、URI 値が異なる場合があり、サブスクリプション内のすべてのソースに適用されます。|
|/dia:\<言語 >|クエリ文字列で使用する言語を定義します。|
|/tn:\<Net-transportname >|リモートイベントソースへの接続に使用するトランスポートの名前を指定します。|
|/tp:\<Transportport >|リモートイベントソースへの接続時にトランスポートによって使用されるポート番号を設定します。|
|dm:\<Deliverymode >|配信モードを指定します。 \<Deliverymode > には、プルまたはプッシュを使用できます。 このオプションは、 **/cm**オプションが Custom に設定されている場合にのみ有効です。|
|/dmi:\<Deliverymax >|バッチ配信の項目の最大数を設定します。 このオプションは、 **/cm**が Custom に設定されている場合にのみ有効です。|
|/dmlt:\<Deliverytime >|イベントのバッチ配信の最大待機時間を設定します。 \<Deliverytime > はミリ秒単位の時間です。 このオプションは、 **/cm**が Custom に設定されている場合にのみ有効です。|
|/こんにちは:\<ハートビート >|ハートビートの間隔を定義します。 \<のハートビート > はミリ秒数です。 このオプションは、 **/cm**が Custom に設定されている場合にのみ有効です。|
|/cf:\<コンテンツ >|返されるイベントの形式を指定します。 \<コンテンツ > には、イベントまたは RenderedText を指定できます。 値が RenderedText の場合、イベントに添付されたローカライズされた文字列 (イベントの説明など) と共にイベントが返されます。 既定値は RenderedText です。|
|/l:\<ロケール >|RenderedText 形式でローカライズされた文字列を配信するためのロケールを指定します。 \<Locale > は言語と国/地域識別子 (EN-US など) です。 このオプションは、 **/cf**オプションが RenderedText に設定されている場合にのみ有効です。|
|/Readexist: [\<>]|サブスクリプションに対して配信されるイベントを識別します。 \<Readexist > には true または false を使用できます。 <Readexist> が true の場合、すべての既存のイベントがサブスクリプションのイベントソースから読み込まれます。 <Readexist> が false の場合、将来の (到着している) イベントのみが配信されます。 既定値は、 **////** オプションの値が指定されていない場合に true になります。 **/** のオプションを指定しない場合、既定値は false になります。|
|/lf:\<ログファイル >|イベントソースから受信したイベントを格納するために使用されるローカルイベントログを指定します。|
|/pn:\<Publishername >|発行元の名前を指定します。 **/Lf**オプションで指定されたログを所有またはインポートするパブリッシャーである必要があります。|
|/essp:\<Enableport >|リモートサービスのサービスプリンシパル名にポート番号を追加する必要があることを指定します。 \<Enableport > は true または false にすることができます。 <Enableport> が true の場合は、ポート番号が付加されます。 ポート番号を追加すると、イベントソースへのアクセスが拒否されるのを防ぐために、一部の構成が必要になる場合があります。|
|/hn:\<ホスト名 >|ローカルコンピューターの DNS 名を指定します。 この名前は、イベントをプッシュするためにリモートイベントソースによって使用されます。プッシュサブスクリプションの場合にのみ使用する必要があります。|
|/ct:\<の種類 >|リモートソースアクセスの資格情報の種類を設定します。 \<Type > は、default、negotiate、digest、basic、または localmachine のいずれかの値にする必要があります。 既定値は default です。|
|/cun:\<Comusername >|独自のユーザー資格情報を持たないイベントソースに使用する共有ユーザー資格情報を設定します。 このオプションを **/c**オプションと共に指定した場合、構成ファイルからの個々のイベントソースのユーザー名と UserPassword の設定は無視されます。 特定のイベントソースに対して別の資格情報を使用する場合は、別の**ss**コマンドのコマンドラインで特定のイベントソースに対して **/un**オプションと **/up**オプションを指定することによって、この値を上書きする必要があります。|
|/カップ:\<Compassword >|共有ユーザー資格情報のユーザーパスワードを設定します。 \<Compassword > が * (アスタリスク) に設定されている場合は、コンソールからパスワードが読み取られます。 このオプションは、 **/cun**オプションが指定されている場合にのみ有効です。|
|/q: [\<Quiet >]|構成手順で確認を求めるメッセージを表示するかどうかを指定します。 \<Quiet > には、true または false を指定できます。 <Quiet> が true の場合、構成手順によって確認メッセージが表示されません。 このオプションの既定値は false です。|

## <a name="remarks"></a>コメント

> [!IMPORTANT]
> "RPC サーバーは使用できませんか?" というメッセージが表示された場合は、「wecutil を実行しようとすると、Windows イベントコレクターサービス (wecsvc) を開始する必要があります。 Wecsvc を起動するには、管理者特権のコマンドプロンプトで「net start wecsvc」と入力します。

- 次の例は、構成ファイルの内容を示しています。  
  ```
  <Subscription xmlns=https://schemas.microsoft.com/2006/03/windows/events/subscription>
  <Uri>https://schemas.microsoft.com/wbem/wsman/1/windows/EventLog</Uri>
  <!-- Use Normal (default), Custom, MinLatency, MinBandwidth -->
  <ConfigurationMode>Normal</ConfigurationMode>
  <Description>Forward Sample Subscription</Description>
  <SubscriptionId>SampleSubscription</SubscriptionId>
  <Query><![CDATA[
  <QueryList>
  <Query Path=Application>
  <Select>*</Select>
  </Query>
  </QueryList>
  ]]></Query>
  <EventSources>
  <EventSource Enabled=true>
  <Address>mySource.myDomain.com</Address>
  <UserName>myUserName</UserName>
  <Password>*</Password>
  </EventSource>
  </EventSources>
  <CredentialsType>Default</CredentialsType>
  <Locale Language=EN-US></Locale>
  </Subscription>
  ```

## <a name="examples"></a><a name=BKMK_examples></a>例

Sub1 という名前のサブスクリプションの出力構成情報:
```
wecutil gs sub1
```
出力の例:
```
EventSource[0]:
Address: localhost
Enabled: true
Description: Subscription 1
Uri: wsman:microsoft/logrecord/sel
DeliveryMode: pull
DeliveryMaxSize: 16000
DeliveryMaxItems: 15
DeliveryMaxLatencyTime: 1000
HeartbeatInterval: 10000
Locale:
ContentFormat: renderedtext
LogFile: HardwareEvents
```
Sub1 という名前のサブスクリプションの実行時の状態を表示します。
```
wecutil gr sub1
```
次のように、WsSelRg2 という名前の新しい XML ファイルから、sub1 という名前のサブスクリプション構成を更新します。
```
wecutil ss sub1 /c:%Windir%\system32\WsSelRg2.xml
```
複数のパラメーターを使用して、sub2 という名前のサブスクリプション構成を更新します。
```
wecutil ss sub2 /esa:myComputer /ese /un:uname /up:* /cm:Normal
```
MySource.myDomain.com のリモートコンピューターの Windows Vista アプリケーションイベントログから ForwardedEvents ログにイベントを転送するためのサブスクリプションを作成します (構成ファイルの例については、「解説」を参照してください)。
```
wecutil cs subscription.xml
```
Sub1 という名前のサブスクリプションを削除します。
```
wecutil ds sub1
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
