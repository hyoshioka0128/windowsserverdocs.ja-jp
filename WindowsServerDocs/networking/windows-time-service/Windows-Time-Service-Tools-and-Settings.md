---
ms.assetid: 6086947f-f9ef-4e18-9f07-6c7c81d7002c
title: Windows タイム サービスのツールと設定
author: Teresa-Motiv
ms.author: v-tea
ms.date: 02/24/2020
ms.topic: article
ms.prod: windows-server
ms.technology: networking
ms.openlocfilehash: b73b6bf2150b8c97b858f41d7a4864a5d6fd5546
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87182118"
---
# <a name="windows-time-service-tools-and-settings"></a>Windows タイム サービスのツールと設定

> 適用先:Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows 10 以降

このトピックでは、Windows タイム サービス (W32Time) のツールと設定について説明します。

ドメインに参加しているクライアント コンピューターのみの時刻を同期することが必要な場合は、「[ドメイン時刻の自動同期のためにクライアント コンピューターを構成する](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816884%28v%3dws.10%29)」を参照してください。 Windows タイム サービスを構成する方法に関するその他のトピックについては、[Windows タイム サービスの構成情報を見つける方法](windows-time-service-top.md)に関する記事を参照してください。

> [!CAUTION]
> Windows タイム サービスが実行されている場合は、**Net time** コマンドを使用して時間を構成および設定しないでください。
>
> また、Windows XP 以前のバージョンを実行している古いコンピューターでは、**Net time /querysntp** コマンドにより、コンピューターが同期するように構成されているネットワーク タイム プロトコル (NTP) サーバーの名前が表示されますが、その NTP サーバーが使用されるのは、コンピューターのタイム クライアントが NTP または AllSync として構成されている場合のみです。 このコマンドはその後、非推奨となりました。

ほとんどのドメイン メンバー コンピューターのタイム クライアントの種類は NT5DS です。これは、ドメイン階層から時刻が同期されることを意味します。 この唯一の例外としての典型例は、フォレスト ルート ドメインのプライマリ ドメイン コントローラ (PDC) エミュレーター操作マスタとして機能するドメイン コントローラーです。 PDC エミュレーター操作マスタは通常、外部のタイム ソースを使用して時間を同期するように構成されています。 コンピューターのタイム クライアント構成を表示するには (Windows Server 2008 および Windows Vista 以降)、管理者特権でのコマンド プロンプトから **W32tm /query /configuration** コマンドを実行し、コマンドの出力の **Type** 行を参照します。 詳細については、「[Windows タイム サービスのしくみ](How-the-Windows-Time-Service-Works.md)」を参照してください。 さらに、**reg query HKLM\SYSTEM\CurrentControlSet\Services\W32Time\Parameters** コマンドを実行し、コマンドの出力で **NtpServer** の値を参照できます。

> [!IMPORTANT]
> Windows Server 2016 より前では、W32Time サービスは、精密な時間管理を必要とするアプリケーションのニーズを満たすように設計されていませんでした。 しかし、Windows Server 2016 の更新プログラムにより、1 ミリ秒の精度を実現するソリューションをドメインに実装できるようになりました。 詳細については、[Windows 2016 の正確な時刻](accurate-time.md)および[高精度の環境向けに Windows タイム サービスを構成するためのサポート範囲](support-boundary.md)に関する記事を参照してください。

## <a name="windows-time-service-tools"></a>Windows タイム サービス ツール

Windows タイム サービスには次のツールが関連付けられています。

### <a name="w32tmexe-windows-time"></a>W32tm.exe:Windows タイム

**カテゴリ**

このツールは、Windows (windows XP 以降のバージョン) と Windows Server (Windows Server 2003 以降のバージョン) の既定のインストールに含まれています。

**バージョンの互換性**

このツールは、Windows (windows XP 以降のバージョン) と Windows Server (Windows Server 2003 以降のバージョン) の既定のインストールで動作します。

W32tm.exe を使用して、Windows タイム サービスの設定を構成し、タイム サービスの問題を診断できます。 W32tm.exe は、Windows タイム サービスを構成、監視、またはトラブルシューティングするために推奨されるコマンド ライン ツールです。

次の表では、W32tm.exe で使用できるパラメーターについて説明します。

**W32tm.exe の主なパラメーター**

|パラメーター |説明 |
| --- | --- |
|**w32tm /?** |W32tm のコマンドラインのヘルプを表示します |
|**w32tm /register** |タイム サービスをサービスとして実行するように登録し、レジストリに既定の構成情報を追加します。 |
|**w32tm /unregister** |タイム サービスの登録を解除し、その構成情報をすべてレジストリから削除します。 |
|**w32tm /monitor [/domain:\<*domain name*>] [/computers:\<*name*>[,\<*name*>[,\<*name*>...]]] [/threads:\<*num*>]** |Windows タイム サービスを監視します。<p>**/domain**:監視するドメインを指定します。 ドメイン名が指定されていない場合、または **/domain** と **/computers** のどちらのオプションも指定されていない場合は、既定のドメインが使用されます。 このオプションは複数回使用される場合があります。<p>**/computers**:指定されたコンピューターの一覧を監視します。 コンピューター名はコンマで区切り、スペースは使用しません。 名前にプレフィックス **\*** が付いている場合は、PDC として扱われます。 このオプションは複数回使用される場合があります。<p>**/threads**:同時に分析するコンピューターの数を指定します。 既定値は 3 です。 許容範囲は 1 から 50 です。 |
|**w32tm /ntte \<NT *time epoch*>** |Windows NT のシステム時刻 (0h 1-Jan 1601 から始まり 10<sup>-7</sup> 秒間隔で計測される) を、読み取り可能な形式に変換します。 |
|**w32tm /ntpte \<NTP *time epoch*>** |NTP 時刻 (0h 1-Jan 1900 から始まり 2<sup>-32</sup> 秒間隔で計測される) を、読み取り可能な形式に変換します。 |
|**w32tm /resync [/computer:\<*computer*>] [/nowait] [/rediscover] [/soft]** |蓄積したエラー統計をすべて削除して、直ちに時刻を再同期するようにコンピュータに指示します。<p>**/computer:\<*computer*>** :再同期する必要があるコンピューターを指定します。 指定しない場合、ローカル コンピューターが再同期されます。<p>**/nowait**: 同期の再実行を待たずにすぐに返します。 指定がない場合は、同期の再実行の完了を待ってから返します。<p>**/rediscover**:ネットワーク構成を再検出し、ネットワーク ソースを再検出してから、再同期します。<p>**/soft**:既存のエラー統計を使って再同期します。 互換性のために用意されたもので、あまり有効ではありません。 |
|**w32tm /stripchart /computer:\<*target*> [/period:\<*refresh*>] [/dataonly] [/samples:\<*count*>] [/rdtsc]** |このコンピュータと別のコンピュータ間のオフセットのストリップ チャートを表示します。<p>**/computer:\<*target*>** :オフセットを計測するターゲット コンピュータです。<p>**/period:\<*refresh*>** :サンプルを収集する秒単位の間隔です。 既定値は 2 秒です。<p>**/dataonly**:データのみを表示し、グラフィックは表示しません。<p>**/samples:\<*count*>** :\<*count*> 個のサンプルを収集してから停止します。 指定しない場合、**Ctrl + C** が押されるまでサンプルが収集されます。<br/><br/>**/rdtsc**:各サンプルについて、このオプションはテキスト グラフィックではなく、**RdtscStart**、**RdtscEnd**、**FileTime**、**RoundtripDelay**、および **NtpOffset** のヘッダーと共にコンマ区切り値を出力します。<br/><ul><li>**RdtscStart**:NTP 要求が生成される直前に収集された [RDTSC (読み取りタイム スタンプ カウンター)](https://en.wikipedia.org/wiki/Time_Stamp_Counter) 値。</li><li>**RdtscEnd**:NTP 応答の受信と処理の直後に収集された RDTSC 値。</li><li>**FileTime**:NTP 要求で使用されるローカル FILETIME 値。</li><li>**RoundtripDelay**:NTP ラウンドトリップ計算に従って計算された、NTP 要求の生成から受信された NTP 応答の処理までの経過時間 (秒単位)。</li><li>**NTPOffset**:NTP オフセット計算に従って計算された、ローカル コンピューターと NTP サーバーの間の時間オフセット (秒単位)。</li></ul> |
|**w32tm /config [/computer:\<*target*>] [/update] [/manualpeerlist:\<*peers*>] [/syncfromflags:\<*source*>] [/LocalClockDispersion:\<*seconds*>] [/reliable:(YES\|NO)] [/largephaseoffset:\<*milliseconds*>]** |**/computer:\<*target*>** :\<*target*> の構成を調整します。 指定しない場合、既定値はローカル コンピューターです。<p>**/update**:タイム サービスに構成が変更されたことを通知し、変更を有効にします。<p>**/manualpeerlist:\<*peers*>** :手動ピアの一覧を \<*peers*> に設定します。これは DNS または IP アドレス、あるいはその両方をスペースで区切った一覧です。 複数のピアを指定する場合は、このオプションを引用符で囲む必要が あります。<p>**/syncfromflags:\<*source*>** :NTP クライアントの同期元であるソースを設定します。 \<*source*> は、次のキーワードのコンマ区切りの一覧である必要があります (大文字と小文字は区別されません)。<ul><li>**MANUAL**:手動ピアの一覧からピアを追加します。</li><li>**DOMHIER**:ドメイン階層内のドメイン コントローラー (DC) から同期を取ります。</li></ul>**/LocalClockDispersion:\<*seconds*>** :構成されたソースから時間を取得できない場合に W32Time が想定する内部クロックの精度を構成します。<p>**/reliable:(YES\|NO)** :このコンピュータが信頼性の高いタイム ソースであるかどうかを設定します。 この設定はドメイン コントローラーでのみ有効です。<ul><li>**YES**:このコンピュータは信頼性の高いタイム サービスです。</li><li>**NO**:このコンピュータは信頼性の高いタイム サービスではありません。</li></ul>**/largephaseoffset:\<*milliseconds*>** : W32Time がスパイクと見なすローカルおよびネットワーク時刻の時間差を設定します。 |
|**w32tm /tz** |現在のタイムゾーン設定を表示します。 |
|**w32tm /dumpreg [/subkey:\<*key*>] [/computer:\<*target*>]** |指定されたレジストリ キーと関連付けられた値を表示します。<p>既定のキーは **HKLM\System\CurrentControlSet\Services\W32Time** (タイム サービスのルート キー) です。<p>**/subkey:\<*key*>** :既定のキーのサブキー <key> と関連付けられた値を表示します。<p>**/computer:\<*target*>** :コンピューター \<*target*> のレジストリ設定に関してクエリを実行します |
|**w32tm /query [/computer:\<*target*>] {/source \| /configuration \| /peers \| /status} [/verbose]** |コンピューターの Windows タイム サービス情報を表示します。 このパラメーターは、Windows Vista および Windows Server 2008 の Windows タイム クライアントで最初に使用できるようになりました。<p>**/computer:\<*target*>** :\<*target*> の情報に関してクエリを実行します。 指定しない場合、既定値はローカル コンピューターです。<p>**/source**:タイム ソースを表示します。<p>**/configuration**:実行時間の構成と、設定の取得元を表示します。 詳細モードでは、未定義または未使用の設定も表示します。<p>**/peers**:ピアとその状態の一覧を表示します。<p>**/status**:Windows タイム サービスの状態を表示します。<p>**/verbose**:詳細モードを設定して詳細情報を表示します。 |
|**w32tm /debug {/disable \| {/enable /file:\<*name*> /size:/<*bytes*> /entries:\<*value*> [/truncate]}}** |ローカル コンピューターの Windows タイム サービスのプライベート ログを有効または無効にします。 このパラメーターは、Windows Vista および Windows Server 2008 の Windows タイム クライアントで最初に使用できるようになりました。<p>**/disable**:プライベート ログを無効にします。<p>**/enable**:プライベート ログを有効にします。<ul><li>**file:\<*name*>** :絶対ファイル名を指定します。</li><li>**size:\<*bytes*>** :循環ログの最大サイズを指定します。</li><li>**entries:\<*value*>** :ログに記録する情報の種類を指定するフラグの一覧を数値で指定し、コンマで区切って指定します。 有効な数値は 0 から 300 です。 単一の数値に加えて、0-100,103,106 などの数値の範囲も有効です。 値を 0-300 に指定すると、すべての情報がログに記録されます。</li></ul>**/truncate**:ファイルを切り捨てます (存在する場合)。 |

**W32tm.exe** の詳細については、[Windows ヘルプ](https://support.microsoft.com/hub/4338813/windows-help?os=windows-10)を参照してください。

**例**

ローカルの Windows タイム クライアントが ntpserver.contoso.com および clock.adatum.com という名前の 2 つの異なるタイムサーバーを指すように設定する場合は、コマンド ラインで次のコマンドを入力し、Enter キーを押します。

```cmd
w32tm /config /manualpeerlist:"ntpserver.contoso.com clock.adatum.com" /syncfromflags:manual /update
```

外部時刻同期のためにインターネットで使用できる有効な NTP サーバーの一覧については、「[インターネット上で利用可能な簡易ネットワーク タイム プロトコル (SNTP) タイム サーバーの一覧](https://go.microsoft.com/fwlink/?linkid=60401)」を参照してください。

CONTOSOW1 というホスト名を持つ Windows ベースのクライアント コンピューターから Windows タイム クライアント構成を確認する場合は、次のコマンドを実行します。

```cmd
W32tm /query /computer:contosoW1 /configuration
```

このコマンドの出力は、Windows タイム クライアント用に設定された構成パラメーターの一覧です。

> [!IMPORTANT]
> [Windows Server 2016 では、RFC 仕様に合わせて時間同期アルゴリズムが改善](https://aka.ms/WS2016Time)されました。 そのため、ローカル Windows タイム クライアントが複数のピアを指すように設定する場合は、3 つ以上の異なるタイム サーバーを準備することを強くお勧めします。
>
> タイム サーバーが 2 つのみの場合は、**UseAsFallbackOnly** フラグ (0x2) を指定して、いずれかの優先順位を下げます。 たとえば、clock.adatum.com よりも ntpserver.contoso.com を優先させる場合は、次のコマンドを実行します。
> ```cmd
> w32tm /config /manualpeerlist:"ntpserver.contoso.com,0x8 clock.adatum.com,0xa" /syncfromflags:manual /update
> ```
> 指定したフラグの意味については、["HKLM\SYSTEM\CurrentControlSet\Services\W32Time\Parameters" サブキー エントリ](#parameters)を参照してください。

## <a name="using-group-policy-to-configure-the-windows-time-service"></a>Windows タイム サービスを構成するためのグループ ポリシーの使用

Windows タイム サービスは、いくつかの構成プロパティをレジストリ エントリとして格納します。 グループ ポリシー オブジェクトを使用して、この情報の大部分を構成することができます。 たとえば、GPO を使用して、コンピューターを NTPServer または NTPClient として構成すること、時刻の同期メカニズムを構成すること、またはコンピューターを信頼性の高いタイム ソースとして構成することができます。

> [!NOTE]
> Windows タイム サービスのグループ ポリシー設定は、Windows Server 2003、Windows Server 2003 R2、Windows Server 2008、および Windows Server 2008 R2 のドメイン コントローラーで構成でき、Windows Server 2003、Windows Server 2003 R2、Windows Server 2008、および Windows Server 2008 R2 を実行しているコンピューターにのみ適用できます。

Windows では、**Computer Configuration\Administrative Templates\System\Windows Time Service** にある W32Time.admx 管理用テンプレート ファイルに Windows タイム サービスのポリシー情報が格納されます。 ここにはポリシーがレジストリに定義する構成情報が格納され、これらのレジストリエントリを使用して Windows タイム サービスのレジストリ エントリが構成されます。 その結果、グループ ポリシーによって定義された値によって、レジストリの Windows タイム サービス セクションの既存の値が上書きされます。

> [!IMPORTANT]
> GPO のプリセット設定の中には、対応する既定のレジストリ エントリとは異なるものがあります。 GPO を使用して Windows タイム設定を構成する場合は、[Windows タイムサービスのグループ ポリシー設定のプリセット値が、Windows Server 2003 の対応する Windows タイム サービスのレジストリ エントリと異なること](https://go.microsoft.com/fwlink/?LinkId=186066)を確認してください。 この問題は、Windows Server 2008 R2、Windows Server 2008、Windows Server 2003 R2、および Windows Server 2003 に当てはまります。

たとえば、**Windows NTP クライアントを構成する**ポリシーのポリシー設定を編集するとします。

変更内容は、管理用テンプレートの次の場所に保存されます。

> **コンピュータの構成\管理用テンプレート\システム\Windows タイム サービス\タイム プロバイダー\Windows NTP クライアントを構成する**

Windows では、次のサブキーの下にあるレジストリのポリシー領域にこれらの設定が読み込みます。

> **HKLM\Software\Policies\Microsoft\W32time\TimeProviders\NtpClient**

その後、Windows では、ポリシー設定を使用して、次のサブキーの下の関連する Windows タイム サービス レジストリ エントリが構成されます。

> **HKLM\SYSTEM\CurrentControlSet\Services\W32Time\Time Providers\NTPClient\\**

次の表に、Windows タイムサービス用に構成できるポリシーと、それらのポリシーによって影響を受けるレジストリ サブキーの一覧を示します。

> [!NOTE]
> グループ ポリシー設定を削除すると、Windows ではレジストリのポリシー領域から対応するエントリが削除されます。

|ポリシー<sup>1</sup> |レジストリの場所<sup>2、</sup> <sup>3</sup> |
| --- | --- |
|グローバル構成設定 |W32Time<br />W32Time\Config<br />W32Time\Parameters |
|タイム プロバイダー\Windows NTP クライアントを構成する |W32Time\TimeProviders\NtpClient |
|タイム プロバイダー\Windows NTP クライアントを有効にする |W32Time\TimeProviders\NtpClient |
|タイム プロバイダー\Windows NTP サーバーを有効にする |W32Time\TimeProviders\NtpServer |

> <sup>1</sup> カテゴリ パス:**Computer Configuration\Administrative Templates\System\Windows Time Service**
> <sup>2</sup> サブキー:**HKLM\SOFTWARE\Policies\Microsoft**
> <sup>3</sup> サブキー:**HKLM\SYSTEM\CurrentControlSet\Services**

## <a name="enabling-w32time-logging"></a>W32Time ログの有効化

次の 3 つのレジストリ エントリは、W32Time の既定の構成の一部ではありませんが、高いログ記録機能を得るためにレジストリに追加できます。 システム イベント ログに記録された情報は、グループ ポリシー オブジェクト エディターの **EventLogFlags** 設定の値を変えることによって変更できます。 既定では、タイム サービスは、新しいタイム ソースに切り替えるたびにイベントをログに記録します。

W32Time ログを有効にするには、次のレジストリ エントリを追加する必要があります。

|レジストリ エントリ |バージョン |説明 |
| --- | --- | --- |
|**FileLogEntries** |すべてのバージョン |Windows タイム ログ ファイルで作成されるエントリの数を制御します。 既定値は none で、この場合は Windows タイム アクティビティがログに記録されません。 有効な値は **0** から **300** です。 この値は、Windows タイムによって通常作成されるイベント ログ エントリには影響しません |
|**FileLogName** |すべてのバージョン |Windows タイム ログの場所とファイル名を制御します。 既定値は空白です。これは、**FileLogEntries** が変更されない限り変更しないでください。 有効な値は、Windows タイムがログ ファイルの作成に使用する完全なパスとファイル名です。 この値は、Windows タイムによって通常作成されるイベント ログ エントリには影響しません。 |
|**FileLogSize** |すべてのバージョン |Windows タイム ログ ファイルの循環ログの動作を制御します。 **FileLogEntries** および **FileLogName** が定義されている場合、エントリは、最も古いログ エントリを新しいエントリで上書きするまでに、ログ ファイルが増大できるサイズをバイト単位で定義します。 この設定には、**1000000** 以上の値を使用してください。 この値は、Windows タイムによって通常作成されるイベント ログ エントリには影響しません。 |

## <a name="configuring-how-windows-time-service-resets-the-computer-clock"></a>Windows タイム サービスがコンピューターの時計をリセットする方法の構成

W32Time でコンピューターの時計を段階的に設定するには、オフセットが **MaxAllowedPhaseOffset** 値より小さく、次の式を同時に満たす必要があります。

- Windows Server 2016 以降のバージョン:

  > |**CurrentTimeOffset**| &divide; (16 &times; **PhaseCorrectRate** &times; **pollIntervalInSeconds**) &le; **SystemClockRate** &divide; 2

- Windows Server 2012 R2 以前のバージョン:

  > |**CurrentTimeOffset**| &divide; (**PhaseCorrectRate** &times; **UpdateInterval**) &le; **SystemClockRate** &divide; 2

**CurrentTimeOffset** 値はクロック ティックで測定されます。Windows システムでは 1 ミリ秒 = 10,000 クロック ティックです。

**SystemClockRate** および **PhaseCorrectRate** もクロック ティックで測定されます。 **SystemClockRate** の値を取得するには、次のコマンドを使用し、*秒* &times; 1,000 &times; 10,000 の式を使用して、秒からクロック ティックに変換します。

```cmd
W32tm /query /status /verbose
ClockRate: 0.0156000s
```

**SystemClockRate** は、システム上のクロック レートを示します。 例として 156,000 秒を使用した場合、**SystemClockRate** 値は 0.0156000 &times; 1,000 &times; 10,000 = 156,000 クロック ティックとなります。

**MaxAllowedPhaseOffset** も秒単位で測定されます。 クロック ティックに変換するには、**MaxAllowedPhaseOffset** &times; 1,000 &times; 10,000 のように乗算します。

次の例は、Windows Server 2012 R2 またはそれ以前のバージョンを使用する場合に、これらの計算を適用する方法を示しています。

**例 1:時間が 4 分ずれている場合**

表示されている時刻が 11:05 で、ピアから受け取った正しいと思われるタイム サンプルが 11:09 だとします。

> **PhaseCorrectRate** = 1
>
> **UpdateInterval** = 30,000 クロック ティック
>
> **SystemClockRate** = 156,000 クロック ティック
>
> **MaxAllowedPhaseOffset** = 10 分 = 600 秒 = 600 &times; 1,000 &times; 10,000 = 6,000,000,000 クロック ティック
>
> |**CurrentTimeOffset**|= 4 分 = 4 &times; 60 &times; 1,000 &times; 10,000 = 2,400,000,000 クロック ティック
>
> **CurrentTimeOffset** &le; **MaxAllowedPhaseOffset** ですか?
>
> 2,400,000,000 &le; 6,000,000,000:TRUE

このとき、上記の式が満たされていますか?

> (|**CurrentTimeOffset**| &divide; (**PhaseCorrectRate** &times; **UpdateInterval**) &le; **SystemClockRate** &divide; 2)

2,400,000,000 / (30,000 &times; 1) &le; 156,000 &divide; 2 ですか?

80,000 &le; 78,000:FALSE

したがって、W32tm は直ちに時計の設定を戻します。

> [!NOTE]
> この場合、時計の設定をゆっくりと戻すには、レジストリの **PhaseCorrectRate** または **UpdateInterval** の値も調整して、式の結果が **TRUE** になるようにする必要があります。

**例 2:時間が 3 分ずれている場合**

> **PhaseCorrectRate** = 1
>
> **UpdateInterval** = 30,000 クロック ティック
>
> SystemClockRate = 156,000 クロック ティック
>
> **MaxAllowedPhaseOffset** = 10 分 = 600 秒 = 600 &times; 1,000 &times; 10,000 = 6,000,000,000 クロック ティック
>
> |**CurrentTimeOffset**|= 3 分 = 3 &times; 60 &times; 1,000 &times; 10,000 = 1,800,000,000 クロック ティック
>
> |**CurrentTimeOffset**| &le; **MaxAllowedPhaseOffset** ですか?
>
> 1,800,000,000 &le; 6,000,000,000:TRUE

このとき、上記の式が満たされていますか?

> (|**CurrentTimeOffset**| &divide; (**PhaseCorrectRate** &times; **UpdateInterval**) &le; **SystemClockRate** &divide; 2)
>
> 3 分 &times; (1,800,000,000) &divide; (30,000 &times; 1) &le; 156,000 &divide; 2 ですか?
>
> 60,000 &le; 78,000:TRUE

この場合、時計の設定はゆっくりと戻されます。

## <a name="reference-windows-time-service-registry-entries"></a>参照 :Windows タイム サービスのレジストリ エントリ

> [!WARNING]
> これらのレジストリ エントリの情報は、トラブルシューティングを行うとき、または必要な設定が適用されていることを確認するときに使用するための参照用に提供されています。 レジストリの W32Time セクションの値の多くは、情報を格納するために W32Time によって内部的に使用されます。 これらの値は手動で変更しないでください。 レジストリに対する変更は、レジストリ エディターまたは Windows による検証は行われずに適用されます。 レジストリに無効な値が含まれていると、Windows で回復不能なエラーが発生することがあります。

Windows タイム サービスでは、次のレジストリ サブキーの下に情報が格納されます。

- [**HKLM\SYSTEM\CurrentControlSet\Services\W32Time\Config**](#config)
- [**HKLM\SYSTEM\CurrentControlSet\Services\W32Time\Parameters**](#parameters)
- [**HKLM\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpClient**](#ntpclient)
- [**HKLM\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpServer**](#ntpserver)

また、トラブルシューティング目的で、[ログを構成するためにエントリを追加する](#enabling-w32time-logging)ことができます。

次の表で、"すべてのバージョン" とは、Windows 7、Windows 8、Windows 10、Windows Server 2008 と Windows Server 2008 R2、Windows Server 2012 と Windows Server 2012 R2、Windows Server 2016、および Windows Server 2019 を含む Windows のバージョンを指します。 一部のエントリは、最近の Windows バージョンでのみ使用できます。

> [!NOTE]
> レジストリ内の一部のパラメーターはクロック ティック単位で測定されますが、秒単位で測定されるものもあります。 時刻をクロック ティックから秒に変換するには、次の変換係数を使用します。
> - 1 分 = 60 秒
> - 1 秒 = 1000 ミリ秒
> - 1 ミリ秒 = 10,000 クロック ティック (Windows システムの場合。「[DateTime.Ticks プロパティ](https://docs.microsoft.com/dotnet/api/system.datetime.ticks)」を参照)。
>
> たとえば、5分は 5 &times; 60 &times; 1000 &times; 10000 = 3,000,000,000 クロック ティックになります。

### <a name="hklmsystemcurrentcontrolsetservicesw32timeconfig-subkey-entries"></a><a id="config"></a>"HKLM\SYSTEM\CurrentControlSet\Services\W32Time\Config" サブキー エントリ

|レジストリ エントリ |バージョン |説明 |
| --- | --- | --- |
|**AnnounceFlags** |すべてのバージョン |このコンピューターが信頼性の高いタイム サーバーとしてマークされているかどうかを制御します。 コンピューターは、タイム サーバーとしてもマークされていない限り、信頼性の高いサーバーとしてマークされません。<ul><li>**0x00**: タイム サーバーではありません</li><li>**0x01**: 常にタイム サーバーです</li><li>**0x02**: 自動タイム サーバー</li><li>**0x04**: 常に信頼できるタイム サーバーです</li><li>**0x08**: 信頼できる自動タイム サーバーです</li></ul><br />ドメイン メンバーに対する既定値は **10** です。 スタンドアロン クライアントとサーバーに対する既定値は **10** です。 |
|**ChainDisable** | |チェーン メカニズムを無効にするかどうかを制御します。 チェーンを無効にした場合 (値を 0 に設定した場合)、読み取り専用ドメイン コントローラー (RODC) は任意のドメイン コントローラーと同期できますが、RODC にパスワードがキャッシュされていないホストは RODC と同期できません。 この設定はブール値で、既定値は **0** です。|
|**ChainEntryTimeout** | |チェーン テーブルのエントリが期限切れと見なされるまでこのテーブルに残る最長時間を指定します。 期限切れになったエントリは、次の要求または応答が処理されるときに削除される可能性があります。 既定値は **16** (秒) です。 |
|**ChainLoggingRate** | |チェーン試行の成功と失敗の回数を示すイベントをイベント ビューアーのシステム ログに記録する頻度を制御します。 既定値は **30** (分) です。 |
|**ChainMaxEntries** | |チェーン テーブルで許容されるエントリ数の上限を制御します。 チェーン テーブルがいっぱいになり、削除できる期限切れのエントリもない場合は、着信要求が破棄されます。 既定値は **128** (エントリ) です。 |
|**ChainMaxHostEntries** | |チェーン テーブルの特定のホストに許容されるエントリ数の上限を制御します。 既定値は **4** (エントリ) です。 |
|**ClockAdjustmentAuditLimit** |Windows Server 2016 バージョン 1709 以降のバージョン、Windows 10 バージョン 1709 以降のバージョン |ターゲット コンピューターの W32time サービス イベント ログに記録される最小のローカル クロック調整を指定します。 既定値は **800** (百万分率 - PPM) です。 |
|**ClockHoldoverPeriod** |Windows Server 2016 バージョン 1709 以降のバージョン、Windows 10 バージョン 1709 以降のバージョン |通常、システム クロックがタイム ソースと同期せずに正確さを保つことができる最大秒数を示します。 W32time がすべての入力ブロバイダーから新しいサンプルを取得することなくこの時間が経過した場合、W32time はタイム ソースの再検出を開始します。 既定:7,800 秒。 |
|**EventLogFlags** |すべてのバージョン |タイム サービスがログに記録するイベントを制御します。<ul><li>**0x1**: 時刻のジャンプ</li><li>**0x2**: ソース変更</li></ul>ドメイン メンバーに対する既定値は **2** です。 スタンドアロン クライアントとサーバーに対する既定値は **2** です。 |
|**FrequencyCorrectRate** |すべてのバージョン |クロックを修正するレートを制御します。 この値が小さすぎる場合、クロックは安定せず過度に修正されます。 値が大きすぎる場合、クロックの同期に時間がかかります。 ドメイン メンバーに対する既定値は **4** です。 スタンドアロン クライアントとサーバーに対する既定値は **4** です。<p>**注:** <br />**FrequencyCorrectRate** レジストリ エントリでは、ゼロは無効な値です。 Windows Server 2003、Windows Server 2003 R2、Windows Server 2008、および Windows Server 2008 R2 コンピューターでは、この値が **0** に設定されている場合、Windows タイム サービスによって自動的に **1** に変更されます。 |
|**HoldPeriod** |すべてのバージョン |ローカル クロックを迅速に同期するためにスパイク検出を無効にする期間を制御します。 スパイクとは、時刻が数秒ずれていることを示すタイム サンプルであり、通常は十分な数のタイム サンプルが一貫して返された後に受信されます。 ドメイン メンバーに対する既定値は **5** です。 スタンドアロン クライアントとサーバーに対する既定値は **5** です。 |
|**LargePhaseOffset** |すべてのバージョン |時間オフセットがこの値 (10<sup>-7</sup> 秒単位) 以上である場合にスパイクとみなします。 大量のトラフィックなどのネットワークの中断によって、スパイクが発生することがあります。 スパイクは、長期間継続しない限り無視されます。 ドメイン メンバーに対する既定値は **50000000** です。 スタンドアロン クライアントとサーバーに対する既定値は **50000000** です。 |
|**LastClockRate** |すべてのバージョン |W32Time によって管理されます。 これには Windows オペレーティング システムで使用される予約済みのデータが含まれています。この設定を変更すると、予期しない結果が発生する可能性があります。 ドメイン メンバーに対する既定値は **156250** です。 スタンドアロン クライアントとサーバーに対する既定値は **156250** です。 |
|**LocalClockDispersion** |すべてのバージョン |唯一のタイム ソースが組み込みの CMOS クロックである場合に想定する必要のある分散 (秒単位) を制御します。 ドメイン メンバーに対する既定値は **10** です。 スタンドアロン クライアントとサーバーに対する既定値は **10** です。 |
|**MaxAllowedPhaseOffset** |すべてのバージョン |W32Time がクロック レートを使用してコンピューターの時計を調整する場合の最大オフセット (秒単位) を指定します。 オフセットがこのレートを超えると、W32Time はコンピューターの時計を直接設定します。 ドメイン メンバーに対する既定値は **300** です。 スタンドアロン クライアントとサーバーに対する既定値は **1** です。 詳細については、「[Windows タイム サービスがコンピューターの時計をリセットする方法の構成](#configuring-how-windows-time-service-resets-the-computer-clock)」を参照してください。 |
|**MaxClockRate** |すべてのバージョン |W32Time によって管理されます。 これには Windows オペレーティング システムで使用される予約済みのデータが含まれています。この設定を変更すると、予期しない結果が発生する可能性があります。 ドメイン メンバーに対する既定値は **155860** です。 スタンドアロン クライアントとサーバーに対する既定値は **155860** です。 |
|**MaxNegPhaseCorrection** |すべてのバージョン |サービスが行う最大の負の時間修正を秒単位で指定します。 サービスでこの値より大きい変更が必要であると判断された場合は、代わりにイベントをログに記録します。<p>**注:**<br />**0xFFFFFFFF** 値は特殊なケースです。 この値は、サービスが常に時刻を修正することを意味します。<p>ドメイン メンバーに対する既定値は **0xFFFFFFFF** です。 スタンドアロン クライアントとサーバーに対する既定値は **54,000** (15 時間) です。|
|**MaxPollInterval** |すべてのバージョン |システムのポーリング間隔として許容される最大間隔を log2 秒単位で指定します。 システムはスケジュールされた間隔に従ってポーリングを行う必要がありますが、プロバイダーはサンプルを生成するよう要求された場合、それを拒否できます。 ドメイン コントローラーに対する既定値は **10** です。 ドメイン メンバーに対する既定値は **15** です。 スタンドアロン クライアントとサーバーに対する既定値は **15** です。 |
|**MaxPosPhaseCorrection** |すべてのバージョン |サービスが行う最大の正の時間修正を秒単位で指定します。 サービスでこの値より大きい変更が必要であると判断された場合は、代わりにイベントをログに記録します。<p>**注:**<br />**0xFFFFFFFF** 値は特殊なケースです。 この値は、サービスが常に時刻を修正することを意味します。<p>ドメイン メンバーに対する既定値は **0xFFFFFFFF** です。 スタンドアロン クライアントとサーバーに対する既定値は **54,000** (15 時間) です。 |
|**MinClockRate** |すべてのバージョン |W32Time によって管理されます。 これには Windows オペレーティング システムで使用される予約済みのデータが含まれています。この設定を変更すると、予期しない結果が発生する可能性があります。 ドメイン メンバーに対する既定値は **155860** です。 スタンドアロン クライアントとサーバーに対する既定値は **155860** です。 |
|**MinPollInterval** |すべてのバージョン |システムのポーリング間隔として許容される最小間隔を log2 秒単位で指定します。 システムによってこの間隔よりも頻繁にサンプルを要求されることはありませんが、プロバイダーはスケジュールされた間隔とは別のタイミングでサンプルを生成できることに注意してください。 ドメイン コントローラーに対する既定値は **6** です。 ドメイン メンバーに対する既定値は **10** です。 スタンドアロン クライアントとサーバーに対する既定値は **10** です。 |
|**PhaseCorrectRate** |すべてのバージョン |フェーズ エラーを修正するレートを制御します。 小さい値を指定すると、フェーズ エラーが迅速に修正されますが、クロックが不安定になる可能性があります。 値が大きすぎる場合は、フェーズ エラーの修正に時間がかかります。<p>ドメイン メンバーに対する既定値は **1** です。 スタンドアロン クライアントとサーバーに対する既定値は **7** です。<p>**注:**<br />**PhaseCorrectRate** レジストリ エントリでは、ゼロは無効な値です。 Windows Server 2003、Windows Server 2003 R2、Windows Server 2008、および Windows Server 2008 R2 コンピューターでは、この値が **0** に設定されている場合、Windows タイム サービスによって自動的に **1** に変更されます。 |
|**PollAdjustFactor** |すべてのバージョン |システムのポーリング間隔を増減する決定を制御します。 値が大きいほど、ポーリング間隔が減少する原因となるエラーの量が少なくなります。 ドメイン メンバーに対する既定値は **5** です。 スタンドアロン クライアントとサーバーに対する既定値は **5** です。 |
|**RequireSecureTimeSyncRequests** |Windows 8 およびそれ以降のバージョン |古い認証プロトコルを使用する時間同期要求に対して DC が応答するかどうかを制御します。 有効に (**1** に設定) する場合、DC は古いプロトコルを使用する要求には応答しません。 この設定はブール値で、既定値は **0** です。 |
|**SpikeWatchPeriod** |すべてのバージョン |疑わしいオフセットが正当として受け入れられるまでに保持される必要がある時間 (秒単位) を指定します。 ドメイン メンバーに対する既定値は **900** です。 スタンドアロン クライアントとワークステーションに対する既定値は **900** です。 |
|**TimeJumpAuditOffset** |すべてのバージョン |時刻のジャンプの監査しきい値を秒単位で示す符号なし整数。 タイム サービスがクロックを直接設定してローカル クロックを調整したとき、時間修正がこの値よりも大きい場合、タイム サービスは監査イベントをログに記録します。 |
|**UpdateInterval** |すべてのバージョン |フェーズ修正の調整間のクロック ティック数を指定します。 ドメイン コントローラーに対する既定値は **100** です。 ドメイン メンバーに対する既定値は **30,000** です。 スタンドアロン クライアントとサーバーに対する既定値は **360,000** です。<p>**注:**<br />**UpdateInterval** レジストリ エントリでは、ゼロは無効な値です。 Windows Server 2003、Windows Server 2003 R2、Windows Server 2008、および Windows Server 2008 R2 を実行中のコンピューターでは、この値が **0** に設定されている場合、Windows タイム サービスによって自動的に **1** に変更されます。|
|**UtilizeSslTimeData** |Windows 10 ビルド 1511 より後のバージョンの Windows |値 **1** は、W32Time で複数の SSL タイムスタンプが使用され、極めて不正確なクロックがシードされることを示します。 |

### <a name="hklmsystemcurrentcontrolsetservicesw32timeparameters-subkey-entries"></a><a id="parameters"></a>"HKLM\SYSTEM\CurrentControlSet\Services\W32Time\Parameters" サブキー エントリ

| レジストリ エントリ | バージョン | 説明 |
| --- | --- | --- |
|**AllowNonstandardModeCombinations** |すべてのバージョン |ピア間の同期で非標準モードの組み合わせが許可されることを示します。 ドメイン メンバーに対する既定値は **1** です。 スタンドアロン クライアントとサーバーに対する既定値は **1** です。 |
|**NtpServer** |すべてのバージョン |コンピューターでのタイムスタンプの取得元になる、スペースで区切られたピアのリストを指定します。これは、1 行に 1 つ以上の DNS 名または IP アドレスで構成されます。 リストされる各 DNS 名または IP アドレスは一意である必要があります。 ドメインに接続されているコンピューターは、正式な米国の時刻など、より信頼性の高いタイム ソースと同期する必要があります。  <ul><li>0x01 SpecialInterval </li><li>0x02 UseAsFallbackOnly</li><li>0x04 SymmetricActive:このモードの詳細については、「[Windows タイムサーバー:3.3 動作モード](https://go.microsoft.com/fwlink/?LinkId=208012)」を参照してください。</li><li>0x08 Client</li></ul><br />ドメイン メンバーには、このレジストリ エントリの既定値はありません。 スタンドアロン クライアントとサーバーに対する既定値は time.windows.com,0x1 です。<p>**注:**<br />使用できる NTP サーバーの詳細については、KB 262680 の「[インターネット上で利用可能な簡易ネットワーク タイム プロトコル (SNTP) タイム サーバーの一覧](https://support.microsoft.com/help/262680/a-list-of-the-simple-network-time-protocol-sntp-time-servers-that-are)」を参照してください。 |
|**ServiceDll** |すべてのバージョン |W32Time によって管理されます。 これには Windows オペレーティング システムで使用される予約済みのデータが含まれています。この設定を変更すると、予期しない結果が発生する可能性があります。 ドメイン メンバーとスタンドアロン クライアントおよびサーバーの両方において、この DLL の既定の場所は、%windir%\System32\W32Time.dll です。 |
|**ServiceMain** |すべてのバージョン |W32Time によって管理されます。 これには Windows オペレーティング システムで使用される予約済みのデータが含まれています。この設定を変更すると、予期しない結果が発生する可能性があります。 ドメイン メンバーに対する既定値は **SvchostEntry_W32Time** です。 スタンドアロン クライアントとサーバーに対する既定値は **SvchostEntry_W32Time** です。 |
|**Type** |すべてのバージョン |どのピアからの同期を受け入れるかを示します。  <ul><li>**NoSync**: タイム サービスは他のソースと同期しません。</li><li>**NTP**: タイム サービスは、**NtpServer** レジストリ エントリで指定されたサーバーと同期します。</li><li>**NT5DS**: タイム サービスはドメイン階層から同期します。  </li><li>**AllSync**: タイム サービスは、使用可能なすべての同期メカニズムを使用します。  </li></ul>ドメイン メンバーに対する既定値は **NT5DS** です。 スタンドアロン クライアントとサーバーに対する既定値は **NTP** です。 |

### <a name="hklmsystemcurrentcontrolsetservicesw32timetimeprovidersntpclient-subkey-entries"></a><a id="ntpclient"></a>"HKLM\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpClient" サブキー エントリ

|レジストリ エントリ |バージョン |説明 |
| --- | --- | --- |
|**AllowNonstandardModeCombinations** |すべてのバージョン |ピア間の同期で非標準モードの組み合わせが許可されることを示します。 ドメイン メンバーに対する既定値は **1** です。 スタンドアロン クライアントとサーバーに対する既定値は **1** です。|
|**CompatibilityFlags** |すべてのバージョン |次の互換性フラグと値を指定します。<ul><li>**0x00000001** - DispersionInvalid</li><li>**0x00000002** - IgnoreFutureRefTimeStamp</li><li>**0x80000000** - AutodetectWin2K</li><li>**0x40000000** - AutodetectWin2KStage2</li></ul>ドメイン メンバーに対する既定値は **0x80000000** です。 スタンドアロン クライアントとサーバーに対する既定値は **0x80000000** です。 |
|**CrossSiteSyncFlags** |すべてのバージョン |サービスがコンピューターのドメイン外の同期パートナーを選択するかどうかを決定します。 オプションと値は次のとおりです。<ul><li>**0** - None</li><li>**1** - PdcOnly</li><li>**2** - All</li></ul>Type が NT5DS に設定されていない場合、この値は無視されます。 ドメイン メンバーに対する既定値は **2** です。 スタンドアロン クライアントとサーバーに対する既定値は **2** です。 |
|**DllName** |すべてのバージョン |タイム プロバイダーの DLL の場所を指定します。<p>ドメイン メンバーとスタンドアロン クライアントおよびサーバーの両方において、この DLL の既定の場所は、 **%windir%\System32\W32Time.dll** です。 |
|**Enabled** |すべてのバージョン |現在のタイム サービスで NtpClient プロバイダーが有効になっているかどうかを示します。<ul><li>**1** - はい</li><li>**0** - いいえ</li></ul>ドメイン メンバーに対する既定値は **1** です。 スタンドアロン クライアントとサーバーに対する既定値は **1** です。|
|**EventLogFlags** |すべてのバージョン |Windows タイム サービスによってログに記録されるイベントを指定します。<ul><li>**0x1** - 到達可能性の変更</li><li>**0x2** - 大きいサンプル スキュー (これは Windows Server 2003、Windows Server 2003 R2、Windows Server 2008、および Windows Server 2008 R2 のみに当てはまります)</li></ul>ドメイン メンバーに対する既定値は **0x1** です。 スタンドアロン クライアントとサーバーに対する既定値は **0x1** です。|
|**InputProvider** |すべてのバージョン |NtpServer から時刻情報を取得する InputProvider として NtpClient を有効にするかどうかを示します。 NtpServer は、ローカル クロックを同期するのに役立つタイム サンプルを返すことによって、ネットワーク上のクライアント時間要求に応答するタイム サーバーです。 <ul><li>**1** - はい</li><li>**0** - いいえ</li></ul>ドメイン メンバーとスタンドアロン クライアントの両方に対する既定値は **1** です。 |
|**LargeSampleSkew** |すべてのバージョン |ログ記録の大きいサンプル スキューを秒単位で指定します。 証券取引委員会 (SEC) の仕様に準拠するには、これは 3 秒に設定する必要があります。 この設定では、**EventLogFlags** が 0x2 の大きいサンプル スキューについて明示的に構成されている場合のみ、イベントがログに記録されます。 ドメイン メンバーに対する既定値は 3 です。 スタンドアロン クライアントとサーバーに対する既定値は 3 です。 |
|**ResolvePeerBackOffMaxTimes** |すべてのバージョン |同期するピアの検索に繰り返し失敗した場合に待機間隔を 2 倍にするための最大回数を指定します。 値が 0 の場合、待機間隔が常に最小値であることを意味します。 ドメイン メンバーに対する既定値は **7** です。 スタンドアロン クライアントとサーバーに対する既定値は **7** です。 |
|**ResolvePeerBackoffMinutes** |すべてのバージョン |同期するピアの検索を試行する前に待機する初期間隔を分単位で指定します。 ドメイン メンバーに対する既定値は **15** です。 スタンドアロン クライアントとサーバーに対する既定値は **15** です。  |
|**SpecialPollInterval** |すべてのバージョン |手動ピアのための特別なポーリング間隔を秒単位で指定します。 **SpecialInterval** 0x1 フラグが有効になっている場合、W32Time は、オペレーティング システムによって決定されるポーリング間隔ではなく、このポーリング間隔を使用します。 ドメイン メンバーに対する既定値は **3,600** です。 スタンドアロン クライアントとサーバーに対する既定値は **604,800** です。<br/><br/>ビルド 1703 からは、**SpecialPollInterval** は **MinPollInterval** および **MaxPollInterval** の構成レジストリ値に含まれています。|
|**SpecialPollTimeRemaining** |すべてのバージョン |W32Time によって管理されます。 これには、Windows オペレーティング システムによって使用される予約されたデータが含まれています。 これはコンピューターが再起動した後に W32Time が再同期されるまでの時間を秒単位で指定します。 この設定を変更すると、予期しない結果が発生する可能性があります。 ドメイン メンバーとスタンドアロン クライアントおよびサーバーの両方の既定値は、空白のままになります。 |

### <a name="hklmsystemcurrentcontrolsetservicesw32timetimeprovidersntpserver-subkey-entries"></a><a id="ntpserver"></a>"HKLM\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpServer" サブキー エントリ

|レジストリ エントリ |バージョン |説明 |
| --- | --- | --- |
|**AllowNonstandardModeCombinations** |すべてのバージョン |クライアントとサーバーの間の同期で非標準モードの組み合わせが許可されることを示します。 ドメイン メンバーに対する既定値は **1** です。 スタンドアロン クライアントとサーバーに対する既定値は **1** です。 |
|**DllName** |すべてのバージョン |タイム プロバイダーの DLL の場所を指定します。 ドメイン メンバーとスタンドアロン クライアントおよびサーバーの両方において、この DLL の既定の場所は、 **%windir%\System32\W32Time.dll** です。  |
|**Enabled** |すべてのバージョン |現在のタイム サービスで NtpServer プロバイダーが有効になっているかどうかを示します。 <ul><li>**1** - はい</li><li>**0** - いいえ</li></ul>ドメイン メンバーに対する既定値は **1** です。 スタンドアロン クライアントとサーバーに対する既定値は **1** です。 |
|**InputProvider** |すべてのバージョン |NtpServer から時刻情報を取得する InputProvider として NtpClient を有効にするかどうかを示します。 NtpServer は、ローカル クロックを同期するのに役立つタイム サンプルを返すことによって、ネットワーク上のクライアント時間要求に応答するタイム サーバーです。 <ul><li>**1** - はい</li><li>**0** - いいえ = 0 </li></ul>ドメイン メンバーとスタンドアロン クライアントの両方に対する既定値:1 |

## <a name="reference-pre-set-values-for-the-windows-time-service-gpo-settings"></a>参照 :Windows タイム サービス GPO 設定のプリセット値

次の表に、Windows タイム サービスに関連付けられているグローバル グループ ポリシー設定と、各設定に関連付けられたプリセット値の一覧を示します。 各設定の詳細については、この記事の最初の方にある「[参照 :Windows タイム サービスのレジストリ エントリ](#reference-windows-time-service-registry-entries)」を参照してください。 次の設定は、**グローバル構成設定**と呼ばれる 1 つの GPO に含まれています。

### <a name="pre-set-values-for-global-group-policy-settings"></a>"グローバルグループポリシー" 設定のプリセット値

|グループ ポリシー設定|プリセット値|
| --- | --- |
|**AnnounceFlags**|**10**|
|**EventLogFlags**|**2**|
|**FrequencyCorrectRate**|**4**|
|**HoldPeriod**|**5**|
|**LargePhaseOffset**|**1,280,000**|
|**LocalClockDispersion**|**10**|
|**MaxAllowedPhaseOffset**|**300**|
|**MaxNegPhaseCorrection**|**54,000** (15 時間)|
|**MaxPollInterval**|**15**|
|**MaxPosPhaseCorrection**|**54,000** (15 時間)|
|**MinPollInterval**|**10**|
|**PhaseCorrectRate**|**7**|
|**PollAdjustFactor**|**5**|
|**SpikeWatchPeriod**|**90**|
|**UpdateInterval**|**100**|

### <a name="pre-set-values-for-configure-windows-ntp-client-settings"></a>"Windows NTP クライアントを構成する" 設定のプリセット値

次の表に、**Windows NTP クライアントの構成** GPO についての選択可能な設定、および Windows タイム サービスに関連付けられているプリセット値の一覧を示します。 各設定の詳細については、この記事の最初の方にある「[参照 :Windows タイム サービスのレジストリ エントリ](#reference-windows-time-service-registry-entries)」を参照してください。

|グループ ポリシー設定|プリセット値|
|------------------------|-----------------|
|**NtpServer**|time.windows.com, **0x1**|
|**Type**|既定のオプション:<ul><li>**NTP**: ドメインに参加していないコンピューターで使用します。</li><li>**NT5DS.** ドメインに参加しているコンピューターで使用します。</li></ul>|
|**CrossSiteSyncFlags**|**2**|
|**ResolvePeerBackoffMinutes**|**15**|
|**ResolvePeerBackoffMaxTimes**|**7**|
|**SpecialPollInterval**|**3,600**|
|**EventLogFlags**|**0**|

## <a name="reference-network-ports-that-the-windows-time-service-uses"></a>参照 :Windows タイム サービスが使用するネットワーク ポート

Windows タイムは、すべての時刻同期通信に UDP ポート 123 を使用する必要がある NTP 仕様に従います。 このポートは Windows タイムによって予約されており、常に予約されたままになっています。 コンピューターが時計を同期するか、別のコンピューターに時間を提供するときは常に、その通信は UDP ポート 123 で実行されます。

> [!NOTE]
> 複数のネットワーク アダプターを備えたコンピューター (*マルチホーム* コンピューターとも呼ばれます) がある場合は、ネットワーク アダプターに基づいて Windows タイム サービスを選択的に有効にすることはできません。

## <a name="related-information"></a>関連情報

次のリソースには、このセクションに関連する追加情報が含まれています。

- IETF RFC データベースの RFC *1305*
