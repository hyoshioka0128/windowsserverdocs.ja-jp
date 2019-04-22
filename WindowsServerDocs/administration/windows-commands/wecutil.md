---
title: wecutil
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0c82a6cb-d652-429c-9c3d-0f568c78d54b
author: coreyp-at-msft
ms.author: coreyp
manager: dansimps
ms.openlocfilehash: 50151a322f1ccde2be927de31b0e5c30732b278e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813953"
---
# <a name="wecutil"></a>wecutil



作成してリモート コンピューターから転送されるイベントのサブスクリプションを管理できます。 リモート コンピューターでは、Ws-management プロトコルをサポートする必要があります。 このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。


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

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|{es \| enum サブスクリプション}|存在するすべてのリモート イベント サブスクリプションの名前が表示されます。|
|{gs \| get サブスクリプション} \<Subid > [/f:\<形式 >] [/uni:\<Unicode >]|リモートのサブスクリプションの構成情報が表示されます。 \<Subid > は、サブスクリプションを一意に識別する文字列です。 \<Subid > で指定された文字列と同じでは、 \<SubscriptionId > サブスクリプションを作成するために使用された XML 構成ファイルのタグ。|
|{gr \| get subscriptionruntimestatus} \<Subid > [\<Eventsource >...]|サブスクリプションのランタイム状態を表示します。 \<Subid > は、サブスクリプションを一意に識別する文字列です。 \<Subid > で指定された文字列と同じでは、 \<SubscriptionId > サブスクリプションを作成するために使用された XML 構成ファイルのタグ。 \<Eventsource > イベントのソースとして機能するコンピューターを識別する文字列です。 \<Eventsource > 完全修飾ドメイン名、NetBIOS 名、または IP アドレスにする必要があります。|
|{ss\|セット サブスクリプション} \<Subid > [/e: [\<Subenabled >] [/esa:\<アドレス >] [/ese: [\<Srcenabled >] [/aes] [/res] [/解除:\<ユーザー名 >] [/最大:\<パスワード >] [/d:\<Desc >] [/uri:\<Uri >] [/cm:\<Configmode >] [/ex:\<Expires >] [/q:\<クエリ >] [/dia:\<言語 >] [/tn:\<Transportname >] [/tp:\<Transportport >] [/dm:\<Deliverymode >] [/dmi:\<Deliverymax >] [/dmlt:\<Deliverytime >] [/こんにちは:\<ハートビート >] [/cf:\<コンテンツ >] [/l:\<ロケール >] [/ree: [\<Readexist >] [/lf:\<ログ ファイル >] [/pn:\<Publishername >] [/essp:\<Enableport >] [/hn:\<ホスト名 >] [/ct:\<型 >]</br>または</br>{ss\|セット サブスクリプション/c:\<Configfile > [/cun:\<Comusername >/cup:\<Compassword >]|サブスクリプションの構成を変更します。 サブスクリプション ID とサブスクリプションのパラメータを変更する適切なオプションを指定するか、サブスクリプションのパラメータを変更する XML 構成ファイルを指定することができます。|
|{cs\|サブスクリプションの作成} \<Configfile > [/cun:\<ユーザー名 >/cup:\<パスワード >]|リモートのサブスクリプションを作成します。 \<Configfile > サブスクリプションの構成を含む XML ファイルへのパスを指定します。 絶対パスまたは現在のディレクトリに対する相対パスができます。|
|{ds \| delete-subscription} \<Subid>|サブスクリプションを削除し、サブスクリプションのイベント ログにイベントを提供するすべてのイベント ソースからアンサブスク ライブします。 既に受信され、ログ、イベントは削除されません。 \<Subid > は、サブスクリプションを一意に識別する文字列です。 \<Subid > で指定された文字列と同じでは、 \<SubscriptionId > サブスクリプションを作成するために使用された XML 構成ファイルのタグ。|
|{rs\|再試行サブスクリプション} \<Subid > [\<Eventsource >...]|接続を確立し、非アクティブのサブスクリプションにリモートのサブスクリプション要求を送信する場合に再試行します。 すべてのイベント ソースを再アクティブ化しようとしています。 または、イベント ソースを指定します。 無効なソースは再試行されません。 \<Subid > は、サブスクリプションを一意に識別する文字列です。 \<Subid > で指定された文字列と同じでは、 \<SubscriptionId > サブスクリプションを作成するために使用された XML 構成ファイルのタグ。 \<Eventsource > イベントのソースとして機能するコンピューターを識別する文字列です。 \<Eventsource > 完全修飾ドメイン名、NetBIOS 名、または IP アドレスにする必要があります。|
|{qc\|クイック-config} [/q: [\<Quiet >]|サブスクリプションを作成および再起動を維持できるように、Windows イベント コレクター サービスを構成します。 これには、次の手順が含まれています。</br>1. それ以外の場合は、ForwardedEvents チャネルを有効にします。</br>2. Windows イベント コレクター サービス開始の遅延に設定します。</br>3.実行されていない場合は、Windows イベント コレクター サービスを開始します。|

## <a name="options"></a>オプション

|オプション|説明|
|------|-----------|
|/f:\<形式 >|表示される情報の形式を指定します。 \<形式 > 小文字にすることができます。 場合<Format>XML では、XML 形式で出力が表示されます。 場合\<形式 > は、小文字の名前と値のペアで、出力が表示されます。 既定値は小文字です。|
|/c:\<Configfile >|サブスクリプションの構成を含む XML ファイルへのパスを指定します。 絶対パスまたは現在のディレクトリに対する相対パスができます。 このオプションでのみ使用できます、 **/cun**と **/cup**オプションし、その他のすべてのオプションと相互に排他的です。|
|/e: [\<Subenabled >]|有効またはサブスクリプションを無効にします。 \<Subenabled > true または false にすることができます。 このオプションの既定値は true です。|
|/esa:\<アドレス >|イベント ソースのアドレスを指定します。 \<アドレス > は、完全修飾ドメイン名、NetBIOS 名、またはイベントのソースとして機能するコンピューターを識別する IP アドレスを含む文字列です。 このオプションを使用する必要があります、 **/ese**、 **/aes**、 **/res**、または **/un**と **/up**オプション。|
|/ese: [\<Srcenabled >]|有効または、イベント ソースを無効にします。 \<Srcenabled > true または false にすることができます。 このオプションを使用できる場合だけ、 **/esa**オプションを指定します。 このオプションの既定値は true です。|
|/aes|指定されたイベント ソースを追加、 **/esa**既ににはこれが、サブスクリプションの一部になることがない場合のオプションします。 によってアドレスが指定されている場合、 **/esa**オプションは、サブスクリプションの一部では既に、エラーが報告されます。 このオプションは、場合にのみ使用できますが、 **/esa**オプションを指定します。|
|/res|指定されたイベント ソースを削除、 **/esa**サブスクリプションの一部で既に場合オプションを選択します。 によってアドレスが指定されている場合、 **/esa**オプションは、サブスクリプションの一部ではありません、エラーが報告されます。 このオプションは場合にのみ使用できます **/esa**オプションを指定します。|
|/un:\<ユーザー名 >|指定されたイベント ソースで使用するユーザーの資格情報を指定します、 **/esa**オプション。 このオプションは、場合にのみ使用できますが、 **/esa**オプションを指定します。|
|セットアップ/:\<パスワード >|ユーザーの資格情報に対応するパスワードを指定します。 このオプションは、場合にのみ使用できますが、 **/un**オプションを指定します。|
|/d:\<Desc >|サブスクリプションの説明を提供します。|
|/uri:\<Uri >|サブスクリプションで使用されるイベントの種類を指定します。 \<Uri > は、イベントのソースを一意に識別するイベントのソース コンピューターのアドレスと組み合わせている URI 文字列が含まれています。 サブスクリプション内のすべてのイベント ソース アドレスに URI 文字列が使用されます。|
|/cm:\<Configmode>|構成モードを設定します。 \<Configmode > 次の文字列のいずれかを指定できます。通常、カスタム、MinLatency または MinBandwidth します。 通常、MinLatency、MinBandwidth モードでは、配信モード、配信の最大項目、ハートビートの間隔、および配信の最大待機時間の時間を設定します。 **/Dm**、 **/dmi**、 **/hi**または **/dmlt**オプションがありますのみ、構成モードが Custom に設定されているかどうかを指定します。|
|/ex:\<有効期限が切れる >|サブスクリプションの有効期限が切れる時間を設定します。 \<有効期限が切れる > 標準 XML または ISO8601 の日時形式で定義する必要があります: yyyy、MM-ddThh:mm:ss [.sss] [Z] ここで、T は時刻の区切り記号と Z は UTC 時間を示します。|
|/q:\<クエリ >|サブスクリプションのクエリ文字列を指定します。 形式\<クエリ > 別の URI 値の異なる可能性があり、サブスクリプションのすべてのソースに適用されます。|
|/dia:\<言語 >|クエリ文字列を使用する言語を定義します。|
|/tn:\<Transportname >|リモート イベントのソースへの接続に使用されるトランスポートの名前を指定します。|
|/tp:\<Transportport >|リモート イベント ソースに接続するときに、トランスポートによって使用されるポート番号を設定します。|
|/dm:\<Deliverymode >|配信モードを指定します。 \<Deliverymode > プルまたはプッシュできます。 このオプションは有効な場合、 **/cm**オプションが Custom に設定します。|
|/dmi:\<Deliverymax >|バッチの配信項目の最大数を設定します。 このオプションは有効な場合は **/cm**が Custom に設定します。|
|/dmlt:\<Deliverytime >|イベントのバッチを提供するのには、最大待機時間を設定します。 \<Deliverytime > はミリ秒単位の数です。 このオプションは有効な場合は **/cm**が Custom に設定します。|
|/こんにちは:\<ハートビート >|ハートビートの間隔を定義します。 \<ハートビート > はミリ秒単位の数です。 このオプションは有効な場合は **/cm**が Custom に設定します。|
|/cf:\<Content>|返されるイベントの形式を指定します。 \<コンテンツ > イベントまたは構成情報を指定できます。 値は、構成情報が、イベントにイベントにアタッチ (イベントの説明) など、ローカライズされた文字列が返されます。 既定値は、構成情報です。|
|/l:\<ロケール >|構成情報の形式では、配信、ローカライズされた文字列のロケールを指定します。 \<ロケール > などの言語と国/地域の識別子は、"英語-米国"。 このオプションは有効な場合、 **/cf**オプションが構成情報に設定します。|
|/ree: [\<Readexist >]|サブスクリプションの配信されるイベントを識別します。 \<Readexist > が true または false。 ときに、<Readexist>が true の場合、すべての既存のイベントは、サブスクリプションのイベント ソースから読み取られます。 ときに、<Readexist>が false の場合、(受信) の将来のイベントのみ配信されます。 既定値は true、 **/ree**値のないオプション。 ない場合は **/ree**オプションを指定すると、既定値は false。|
|/lf:\<ログ ファイル >|イベント ソースから受信したイベントの格納に使用されるローカル イベント ログを指定します。|
|/pn:\<Publishername >|パブリッシャーの名前を指定します。 パブリッシャーを所有またはで指定されたログをインポートする必要があります、 **/lf**オプション。|
|/essp:\<Enableport >|ポート番号は、リモート サービスのサービス プリンシパル名を追加する必要がありますを指定します。 \<Enableport > true または false にすることができます。 ポート番号が付加されるとき<Enableport>は true。 ポート番号が追加された場合にいくつかの構成が拒否されているからは、イベント ソースへのアクセスを防ぐために必要があります。|
|/hn:\<ホスト名 >|ローカル コンピューターの DNS 名を指定します。 この名前は、イベントをプッシュ バックするリモートのイベント ソースが使用され、プッシュ サブスクリプションに対してのみ使用する必要があります。|
|/ct:\<型 >|リモート ソースのアクセスの資格情報の種類を設定します。 \<型 > 値は次のいずれかを指定する必要があります。 既定の、ネゴシエート、ダイジェスト、basic または localmachine です。 既定値は。|
|/cun:\<Comusername >|自分のユーザー資格情報がないイベント ソースに使用する共有ユーザー資格情報を設定します。 このオプションは、指定した場合、 **/c**オプションの場合は、構成ファイルからの個々 のイベント ソースは無視されますをユーザー名と UserPassword 設定します。 特定のイベント ソースの別の資格情報を使用する場合は、指定することで、この値を上書きする必要があります、 **/un**と **/up** 別のコマンドラインで特定のイベントソースのオプション**ss**コマンド。|
|/cup:\<Compassword>|共有ユーザー資格情報のユーザーのパスワードを設定します。 ときに\<Compassword > に設定されている * (アスタリスク)、パスワードは、コンソールから読み取り専用です。 ときにこのオプションは有効なのみ、 **/cun**オプションを指定します。|
|/q: [\<quiet >]|構成手順を確認要求かどうかを指定します。 \<Quiet > true または false にすることができます。 場合<Quiet>が true の場合、構成手順が確認を要求していません。 このオプションの既定値は false です。|

## <a name="remarks"></a>注釈

> [!IMPORTANT]
> "RPC サーバーが使用できます、メッセージを受信する場合か。wecutil を実行しようとすると、Windows イベント コレクター (wecsvc) サービスを開始する必要があります。 Wecsvc を開始するには、管理者特権でコマンド プロンプトで net wecsvc に開始します。

-   次の例は、構成ファイルの内容を示しています。  
    ```
    <Subscription xmlns="https://schemas.microsoft.com/2006/03/windows/events/subscription">
    <Uri>https://schemas.microsoft.com/wbem/wsman/1/windows/EventLog</Uri>
    <!-- Use Normal (default), Custom, MinLatency, MinBandwidth -->
    <ConfigurationMode>Normal</ConfigurationMode>
    <Description>Forward Sample Subscription</Description>
    <SubscriptionId>SampleSubscription</SubscriptionId>
    <Query><![CDATA[
    <QueryList>
    <Query Path="Application">
    <Select>*</Select>
    </Query>
    </QueryList>
    ]]></Query>
    <EventSources>
    <EventSource Enabled="true">
    <Address>mySource.myDomain.com</Address>
    <UserName>myUserName</UserName>
    <Password>*</Password>
    </EventSource>
    </EventSources>
    <CredentialsType>Default</CredentialsType>
    <Locale Language="EN-US"></Locale>
    </Subscription>
    ```

## <a name="BKMK_examples"></a>例

Sub1 という名前のサブスクリプションの構成情報を出力します。
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
ランタイム sub1 という名前のサブスクリプションの状態を表示するには。
```
wecutil gr sub1
```
Sub1 WsSelRg2.xml と呼ばれる新しい XML ファイルからをという名前のサブスクリプションの構成を更新します。
```
wecutil ss sub1 /c:%Windir%\system32\WsSelRg2.xml
```
複数のパラメーターを持つ sub2 という名前のサブスクリプションの構成を更新します。
```
wecutil ss sub2 /esa:myComputer /ese /un:uname /up:* /cm:Normal
```
ForwardedEvents ログに mySource.myDomain.com でリモート コンピューターの Windows Vista のアプリケーション イベント ログからイベントを転送するサブスクリプションを作成 (構成ファイルの例については、「解説」を参照してください)。
```
wecutil cs subscription.xml
```
Sub1 という名前のサブスクリプションを削除します。
```
wecutil ds sub1
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)
