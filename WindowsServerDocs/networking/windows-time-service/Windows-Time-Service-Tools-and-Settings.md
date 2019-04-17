---
ms.assetid: 6086947f-f9ef-4e18-9f07-6c7c81d7002c
title: Windows タイム サービスのツールと設定
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking
ms.openlocfilehash: 70b7ee4a9955e023d1664a3c29295a22cd5dc75b
ms.sourcegitcommit: fd6a46b702b235f38d90814dd769106ab37cd61b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/15/2018
---
# <a name="windows-time-service-tools-and-settings"></a>Windows タイム サービスのツールと設定

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012


**このセクションで**  
  
-   [Windows タイム サービスのツール](#w2k3tr_times_tools_dyax)  
  
-   [Windows タイム サービスのレジストリ値](#w2k3tr_times_tools_uhlp)  
  
-   [Windows タイム サービスのグループ ポリシー設定](#w2k3tr_times_tools_vwtt)  
  
-   [Windows タイム サービスによって使用されるネットワーク ポート](#w2k3tr_times_tools_suxb)  
  
-   [関連情報](#w2k3tr_times_tools_qoep)  
  
> [!NOTE]  
> このトピックには、ツールと Windows タイム サービス (W32Time) の設定のみについての情報が含まれています。 If you only want to synchronize time for a domain-joined client computer, see [Configure a client computer for automatic domain time synchronization](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816884%28v%3dws.10%29). Windows タイム サービスを構成する方法に関するその他のトピックは、セクションのトピックの一覧を参照してください。[Windows タイム サービス構成の情報を検索する場所](https://technet.microsoft.com/library/cc773061.aspx)します。  
  
> [!CAUTION]  
> Net time コマンドを使用し、構成や、Windows タイム サービスが実行されているときに設定しないでください。  

Windows XP またはコマンドの Net time 以前を実行している以前のコンピューターにも /querysntp、同期するコンピューターが構成されているが、その NTP サーバーが NTP または AllSync として、コンピューターのタイム クライアントが構成されている場合にのみに使用されるネットワーク タイム プロトコル (NTP) サーバーの名前を表示します。 そのコマンドは廃止されましたので。  
  
ほとんどのドメイン メンバー コンピューターでは、タイム クライアント型の NT5DS で、ドメインの階層からの時間を同期することを意味を持ちます。 一般的なだけの例外は、外部のタイム ソースと時刻を同期するように構成は、通常、フォレスト ルート ドメインのプライマリ ドメイン コントローラー (PDC) エミュレーター操作マスターとして機能するドメイン コントローラーです。 表示するには、タイム クライアント コンピューターの構成の実行 W32tm/query /configuration 以降では、Windows Server 2008、および Windows Vista で管理者特権のコマンド プロンプトからコマンドを読み取り、**種類**コマンドの出力に行。 詳細については、次を参照してください。[Windows タイム サービスのしくみ](https://go.microsoft.com/fwlink/?LinkId=117753)します。 コマンドを実行する**reg クエリ HKLM\SYSTEM\CurrentControlSet\Services\W32Time\Parameters**の値を読み取ると**NtpServer**コマンドの出力にします。  
  
> [!IMPORTANT]  
> Windows Server 2016 では、前に W32Time サービスしない時間の影響を受けやすいアプリケーションのニーズに合わせて設計されました。  ただし、Windows Server 2016 に更新できるようになりましたミリ秒のソリューションを実装する、ドメイン内の正確性。  See [Windows 2016 Accurate Time](accurate-time.md) and  [Support boundary to configure the Windows Time service for high-accuracy environments](https://go.microsoft.com/fwlink/?LinkID=179459) for more information.  
  
## <a name="w2k3tr_times_tools_dyax"></a>Windows タイム サービスのツール  
次のツールは、Windows タイム サービスに関連付けられます。  
  
#### <a name="w32tmexe-windows-time"></a>W32tm.exe: Windows タイム  
**カテゴリ**  

このツールは、Windows XP、Windows Vista、Windows 7、Windows Server 2003、Windows Server 2003 R2、Windows Server 2008、および Windows Server 2008 R2 の既定のインストールの一部としてインストールされます。  
  
**バージョン間の互換性**  
  
このツールは、Windows XP、Windows Vista、Windows 7、Windows Server 2003、Windows Server 2003 R2、Windows Server 2008、および Windows Server 2008 R2 の既定のインストールで動作します。  
  
W32tm.exe を使用すると、Windows タイム サービスの設定を構成します。 タイム サービスの問題の診断にも使用できます。 W32tm.exe は、構成、監視、または Windows タイム サービスのトラブルシューティングの推奨されるコマンド ライン ツールです。  
  
次の表では、W32tm.exe で使用されるパラメーターについて説明します。  
  
**W32tm.exe プライマリ パラメーター**  
  
|パラメーター|説明|  
|-------------|---------------|  
|W32tm/ですか?|W32tm コマンド ラインのヘルプ|  
|W32tm/register|サービスとして実行するタイム サービスを登録し、既定の構成がレジストリに追加します。|  
|W32tm/unregister|タイム サービスの登録を解除し、レジストリからすべての構成情報を削除します。|  
|w32tm/monitor<br /><br />[/domain:<domain name>] [/computers:<name>[、<name>[、<name>...]][/Threads:<num>]|ドメインがでは、監視するドメインを指定します。 ドメイン名を指定しないと、コンピューターとドメインのどちらもオプションが指定されている場合、または場合は、既定のドメインが使用されます。 このオプションを複数回使用可能性があります。<br /><br />コンピューターでは、特定のコンピューターの一覧を監視します。 コンピューター名は、スペースなしで、コンマで区切られます。 名前が付いている場合、"*'、PDC と見なされます。 このオプションを複数回使用可能性があります。<br /><br />スレッド - を同時に分析するコンピューターの数を指定します。 既定値は 3 です。 許容範囲は、1 ~ 50 です。|  
|w32tm /ntte <NT time epoch>|NT のシステム時刻に変換 (10 ^ -7) から 0 h 読みやすい形式、1601 年 1 月 1 - 秒間隔です。|  
|w32tm /ntpte <NTP time epoch>|NTP 時刻に変換 (2 ^-32) 0 h 1-Jan 1900 読みやすい形式の間隔を秒です。|  
|w32tm/resync<br /><br />[/computer:<computer>]<br /><br />[/nowait]<br /><br />[/Rediscover]<br /><br />[/Soft]|そのクロックできるだけ早くすべてのエラーを蓄積された統計情報をスローする同期するコンピューターに指示します。<br /><br />コンピューター:<computer> -必要がありますを再同期するコンピューターを指定します。 指定しない場合、ローカル コンピューターが再同期します。<br /><br />Nowait - 発生再同期化待ちません直ちに戻ります。 それ以外の場合、再同期化を返す前に完了するまで待ちます。<br /><br />再検出 - ネットワーク構成を再検出し、ネットワーク ソースを下げて、再同期します。<br /><br />ソフト - エラーの既存の統計を使用して再同期します。 全く役に、互換性のために提供されています。|  
|w32tm /stripchart<br /><br />/computer:<target><br /><br />[/Period:<refresh>]<br /><br />[/dataonly]<br /><br />[/Samples:<count>]<br/><br/>[/rdtsc]<br/>|このコンピューターや別のコンピューター間のオフセットのストリップのグラフを表示します。<br /><br />コンピューター:<target> -に対してオフセットを測定するコンピューター。<br /><br />期間:<refresh> - 秒単位で、サンプル間の時間。 既定値は、2 秒です。<br /><br />Dataonly - graphics なしデータのみを表示します。<br /><br />サンプル:<count> - 収集<count>し、サンプルを停止します。 指定しない場合、サンプルはまで収集される**ctrl キーを押しながら C**が押されています。<br/><br/>rdtsc: 各サンプルについては、このオプションが印刷と共に RdtscStart、ヘッダーのコンマ区切り値 RdtscEnd、FileTime、RoundtripDelay、テキストの図ではなく NtpOffset します。<br/><ul><li>[RdtscStart – RDTSC (読み取りタイムスタンプ カウンター)](https://en.wikipedia.org/wiki/Time_Stamp_Counter) NTP 要求が生成される直前に値が収集されます。</li><li>RdtscEnd – RDTSC (読み取りタイムスタンプ カウンター) 値を収集しただけで NTP 応答が受信され、処理後にします。</li><li>FileTime – ローカル FILETIME 値の NTP 要求に使用します。</li><li>RoundtripDelay – 時刻は NTP 要求の生成の間の秒経過し、NTP ラウンドト リップの計算に従った計算 NTP 応答を受信したを処理します。</li><li>NTP オフセットの計算に従った NTPOffset – 時間オフセット、ローカル コンピューターと、NTP サーバー間の秒数が計算されます。</li></ul>|
|w32tm /config<br /><br />[/computer:<target>]<br /><br />[/Update]<br /><br />[/manualpeerlist:<peers>]<br /><br />[/syncfromflags:<source>]<br /><br />[/LocalClockDispersion:<seconds>]<br /><br />[/Reliable: ([はい] (& a) #124 文字です NO)]。<br /><br />[/largephaseoffset:<milliseconds>]|コンピューター:<target> -の構成を調整<target>します。 指定しない場合、既定では、ローカル コンピューターです。<br /><br />更新 - タイム サービス構成が変更された原因で、変更を有効にすることを通知します。<br /><br />manualpeerlist:<peers> -手動ピア リストに設定<peers>、これは、DNS や IP アドレスのスペース区切りのリスト。 複数のピアを指定する場合、このオプションは引用符で囲む必要があります。<br /><br />syncfromflags:<source> -どのようなソースから同期する、NTP クライアントを設定します。 <source> これらのキーワードのコンマ区切りのリストを (いない大文字小文字を区別) する必要があります。<br /><br />手動の手動のピアのリストからピアが含まれます。<br /><br />DOMHIER - ドメイン コントローラー (DC) で、ドメインの階層から同期します。<br /><br />LocalClockDispersion:<seconds> -内部の正確性を構成することから時刻を取得できない場合、W32Time が前提としていますクロックがソースを構成します。<br /><br />信頼性の高い: ([はい] (& a) #124 文字です。NO) - 設定されているかどうか、信頼性の高いタイム ソースは、このコンピューター。<br /><br />この設定は、ドメイン コントローラーで有効のみです。<br /><br />[はい] - このコンピューターは、信頼性の高いタイム サービスです。<br /><br />いいえ - このコンピューターは、信頼性の高いタイム サービスではありません。<br /><br />largephaseoffset:<milliseconds> -ローカル時刻の差を設定し、W32Time がスパイクを検討する時間をネットワークです。|  
|w32tm/tz|現在のタイム ゾーン設定を表示します。|  
|w32tm /dumpreg<br /><br />[/Subkey:<key>]<br /><br />[/computer:<target>]|指定されたレジストリ キーに関連付けられている値を表示します。<br /><br />既定のキーは HKLM\System\CurrentControlSet\Services\W32Time<br /><br />(タイム サービスのルート キー)。<br /><br />サブキー:<key> -サブキーに関連付けられている値を表示する<key>既定のキーのします。<br /><br />コンピューター:<target> -コンピューターのレジストリ設定の照会 <target>|  
|w32tm/query [/computer:<target>] {/source & #124;/configuration & #124 です。/Peers & #124;/status} [/verbose]|このパラメーターは、Windows Vista、および Windows Server 2008 の Windows タイム クライアント バージョンで利用可能な最初しました。<br /><br />コンピューターの Windows タイム サービスの情報を表示します。<br /><br />**コンピューター:<target>** -の情報を照会**<target>**します。 指定しない場合、既定値は、ローカル コンピューターにします。<br /><br />**ソース**-タイム ソースを表示します。<br /><br />**構成**-実行時間と、設定が由来の構成を表示します。 詳細出力モード、表示、定義されていないか使用されていない設定が多すぎます。<br /><br />**ピア**-ピアおよびそれらの状態の一覧を表示します。<br /><br />**ステータス**-表示 Windows タイム サービスの状態。<br /><br />**詳細な**-詳細情報を表示する詳細出力モードを設定します。|  
|w32tm/debug {/disable & #124;{/Enable/file:<name> /size:<bytes> /entries:<value> [/truncate]}}|このパラメーターは、Windows Vista、および Windows Server 2008 の Windows タイム クライアント バージョンで利用可能な最初しました。<br /><br />有効にするか、ローカル コンピューターの Windows タイム サービスのプライベート ログを無効にします。<br /><br />**無効にする**-プライベートのログを無効にします。<br /><br />**有効にする**-プライベートのログを有効にします。<br /><br />-   **ファイル:<name>**の絶対ファイル名を指定します。<br />-   **サイズ:<bytes>** -循環ログの最大サイズを指定します。<br />-   **エントリ:<value>** -フラグ、番号で指定されているし、ログに記録する必要があります情報の種類を指定するコンマ区切りのリストが含まれます。 0 ~ 300 が有効です。 番号の範囲は 0-100,103 などの単一の数字だけでなく、有効な 106 します。 値 0 ~ 300 では、すべての情報をログ用です。<br /><br />**切り捨てる**-が存在する場合、ファイルを切り捨てます。|  
  
詳細については**W32tm.exe**、ヘルプとサポート センターでは、Windows XP、Windows Vista、Windows 7、Windows Server 2003、Windows Server 2003 R2、Windows Server 2008、および Windows Server 2008 R2 を参照してください。  
  
## <a name="w2k3tr_times_tools_uhlp"></a>Windows タイム サービスのレジストリ値  
次のレジストリ エントリは、Windows タイム サービスに関連付けられます。  
  
この情報は、トラブルシューティングや、必要な設定が適用されていることの確認で使用するための参照として提供されます。 直接編集しないレジストリ他の手段がない限りをお勧めします。 レジストリに対する変更は検証されません、レジストリ エディターまたは Windows 前に、それらが適用され、その結果、正しくない値を格納できます。 回復不可能なエラーは、システムで、これがあります。  
  
可能であれば、レジストリを直接編集するのではなく、タスクを実行するグループ ポリシーまたは Microsoft 管理コンソール (MMC) など、他の Windows ツールを使用します。 レジストリを編集する必要がある場合、は、細心の注意を使用します。  
  
> [!WARNING]  
> グループ ポリシー オブジェクト (GPO) 設定は既定の対応するレジストリ エントリとは異なるシステム管理用テンプレート ファイル (System.adm) で構成されているプリセット値の一部です。 If you plan to use a GPO to configure any Windows Time setting, be sure that you review [Preset values for the Windows Time service Group Policy settings are different from the corresponding Windows Time service registry entries in Windows Server 2003](https://go.microsoft.com/fwlink/?LinkId=186066). この問題は、Windows Server 2008 R2、Windows Server 2008、Windows Server 2003 R2、および Windows Server 2003 に適用されます。  
  
Windows タイム サービスの多くのレジストリ エントリでは、同じ名前のグループ ポリシー設定と同じです。 グループ ポリシー設定にある同じ名前のレジストリ エントリに対応しています。  
  
>**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\\**

  
このレジストリの場所には、いくつかのレジストリ キーがあります。 Windows の時刻の設定は、これらのキーのすべての値に格納されます。
* [パラメーター](#Parameters)
* [構成](#Configuration)
* [NtpClient](#NtpClient)
* [NtpServer](#NtpServer)
  
> [!NOTE]  
> レジストリの W32Time セクション内の値の多くはによって内部的に使用 W32Time 情報を格納します。 いつでもこれらの値が手動で変更されていない必要があります。 変更しないでくださいのこのセクションで設定するは、設定を理解して、特定の新しい値が期待どおりに動作する場合を除き、します。 次のレジストリ エントリは、下にあります。

>>**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\\**  
  
一部のパラメーターはレジストリ内のクロック刻みに格納され、いくつかは、秒単位です。 変換する時間のクロック刻み (秒)。  
  
-   1 分 = 60 秒  
  
-   1 秒 = 1000 ミリ秒  
  
-   1 ms = 10,000 clock ticks on a Windows system, as described at [DateTime.Ticks Property](https://msdn.microsoft.com/en-us/library/system.datetime.ticks.aspx).  
  
たとえば、5 分になります 5 * 60\ * 1000\ * 10000 = 3000000000 クロック ティック。 

すべてのバージョンには、Windows 7、Windows 8、Windows 10、Windows Server 2008、および Windows Server 2008 R2、Windows Server 2012、Windows Server 2012R2、Windows Server 2016 が含まれます。  いくつかのエントリを新しいバージョンの Windows でのみ利用できます。


#### <a name="Parameters"></a>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\Parameters

|レジストリ エントリ|バージョン|説明|
|------------------------------------|---------------|----------------------------|
|AllowNonstandardModeCombinations|すべての|このエントリは、標準モードの組み合わせがピア間の同期で許可されていることを示します。 ドメイン メンバーの既定値は 1 です。 スタンドアロンのクライアントとサーバーの既定値は 1 です。|
|NtpServer|すべての|このエントリは、1 つ以上の DNS 名または 1 行の IP アドレスで構成されるタイムスタンプは、元のコンピューターの取得先ピアのスペース区切りの一覧を指定します。 各 DNS 名または表示されている IP アドレスは、一意である必要があります。 ドメインに接続されているコンピューターは、公式の米国時間時計より信頼性の高いタイム ソースと同期する必要があります。  <ul><li>0x01 SpecialInterval </li><li>0x02 UseAsFallbackOnly</li><li>0x04 SymmetricActive - For more information about this mode, see [Windows Time Server: 3.3 Modes of Operation](https://go.microsoft.com/fwlink/?LinkId=208012).</li><li>0x08 クライアント</li></ul><br />ドメイン メンバーでこのレジストリ エントリの既定値はありません。 スタンドアロンのクライアントとサーバーに既定値は、time.windows.com、0x1 です。<br /><br />Note: For more information on available NTP Servers, see [Microsoft Knowledge Base article 262680 - A list of the Simple Network Time Protocol (SNTP) time servers that are available on the Internet](https://go.microsoft.com/fwlink/?LinkId=186067)|
|れた|すべての|このエントリは、W32Time で保持されます。 Windows オペレーティング システムで使用される予約済みのデータが含まれているし、この設定への変更が予期しない結果になることができます。 ドメインのメンバーとスタンドアロン クライアントとサーバーの両方でこの DLL の既定の場所は、%windir%\system32\w32time.dll です。  |
|ServiceMain|すべての|このエントリは、W32Time で保持されます。 Windows オペレーティング システムで使用される予約済みのデータが含まれているし、この設定への変更が予期しない結果になることができます。 ドメイン メンバーの既定値は、SvchostEntry_W32Time です。 スタンドアロンのクライアントとサーバーに既定値は、SvchostEntry_W32Time です。  "|
|種類|すべての|このエントリはピアからの同期を受け入れるようになることを示します。  <ul><li>**NoSync**します。 タイム サービスは他のソースと同期されません。</li><li>**NTP します。** タイム サービスの同期がで指定されたサーバーから、 **NtpServer**します。 レジストリ エントリです。</li><li>**NT5DS**します。 タイム サービスは、ドメインの階層から同期します。  </li><li>**AllSync**します。 タイム サービスは、すべての利用可能な同期メカニズムを使用します。  </li></ul>ドメインのメンバー上の既定値は**NT5DS**します。 スタンドアロンのクライアントとサーバーに既定値は**NTP**します。   |

#### <a name="Configuration"></a>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\Config

|レジストリ エントリ|バージョン|説明|
|------------------------------------|---------------|----------------------------|
|AnnounceFlags|すべての|このエントリは、このコンピューターが信頼できるタイム サーバーとしてマークされているかどうかを制御します。 タイム サーバーとしてもマークされている場合を除き、コンピューターは信頼性の高いとマークされていません。<br /> -0x00 タイム サーバーではありません  <br /> -0x01 常にタイム サーバー  <br /> -0x02 自動タイム サーバー  <br /> -0x04 常に信頼できるタイム サーバー  <br /> -0x08 自動の信頼できるタイム サーバー  <br />ドメイン メンバーの既定値は 10 です。 スタンドアロンのクライアントとサーバーの既定値は 10 です。|
|EventLogFlags|すべての|このエントリは、タイム サービスをログに記録されるイベントを制御します。  <br />-時刻のジャンプ: 0x1  <br />-変更を移行元: 0x2  <br />ドメイン メンバーの既定値は 2 です。 スタンドアロンのクライアントとサーバーに既定値は 2 です。  |
|FrequencyCorrectRate|すべての|このエントリは、クロックを修正する速度を制御します。 この値が小さすぎる場合は、クロックが安定しないと、overcorrects します。 値が大きすぎる場合、クロック時間が長いを同期します。 ドメイン メンバーの既定値は 4 です。 スタンドアロンのクライアントとサーバーに既定値は 4 です。  <br /><br />0 は FrequencyCorrectRate レジストリ エントリの値は無効であることに注意してください。 Windows Server 2003、Windows Server 2003 R2、Windows Server 2008、および Windows Server 2008 R2 コンピューターでは、値が 0 に設定されている場合、Windows タイム サービスは自動的にそれを 1 に変更します。  |
|HoldPeriod|すべての|このエントリは、検出のスパイク無効であるためにローカルの時計の同期を迅速に時間を制御します。 スパイクは、その時間を示すタイム サンプルを秒数をオフにし適切なタイム サンプルが一貫して返される後に受け取ったは通常です。 ドメイン メンバーの既定値は 5 です。 スタンドアロンのクライアントとサーバーに既定値は 5 です。  |
|LargePhaseOffset|すべての|このエントリは、時刻より大きいオフセットまたは 10 では、この値に一致することを指定します。<sup>-7</sup>秒がスパイクと見なされます。 大量のトラフィックなど、ネットワーク接続の中断スパイクがあります。 長期間が引き続き発生する場合を除き、スパイクが無視されます。 ドメイン メンバーの既定値は、50000000 です。 スタンドアロンのクライアントとサーバーに既定値は、50000000 です。  |
|LastClockRate|すべての|このエントリは、W32Time で保持されます。 Windows オペレーティング システムで使用される予約済みのデータが含まれているし、この設定への変更が予期しない結果になることができます。 ドメイン メンバーの既定値は、156250 です。 スタンドアロンのクライアントとサーバーに既定値は、156250 です。  |
|LocalClockDispersion|すべての|このエントリは制御場合を想定する必要があります (単位: 秒) 分散だけの時間ソースは、組み込みの CMOS クロックします。 ドメイン メンバーの既定値は 10 です。 スタンドアロンのクライアントとサーバーに既定値は 10 です。|
|MaxAllowedPhaseOffset|すべての|このエントリは、w32time がクロック レートを使用して、コンピューターの時計を調整する (単位: 秒) の [最長オフセットを指定します。 オフセットがこの比率を超えると、W32Time は、コンピューターの時計を直接設定します。 ドメイン メンバーの既定値は、300 です。 スタンドアロンのクライアントとサーバーの既定値は 1 です。  [詳細については、以下をご覧ください](#MaxAllowedPhaseOffset)します。|
|MaxClockRate|すべての|このエントリは、W32Time で保持されます。 Windows オペレーティング システムで使用される予約済みのデータが含まれているし、この設定への変更が予期しない結果になることができます。 ドメイン メンバーの既定値は、155860 です。 スタンドアロンのクライアントとサーバーの既定値は、155860 です。  |
|MaxNegPhaseCorrection|すべての|このエントリは、負の時間の最大の修正をサービスでは、秒単位で指定します。 この値より大きな変更が必要であるサービスによって判断された場合は、代わりに、イベントが記録されます。 特殊なケース: 0 xffffffff 時間修正を常に行うことを意味します。 ドメイン メンバーの既定値は、0 xffffffff です。 スタンドアロンのクライアントとサーバーの既定値は 54,000 (15 時間) です。  |
|MaxPollInterval|すべての|このエントリは、システムのポーリング間隔の許可の log2 秒単位で最大の間隔を指定します。 スケジュールされた間隔] に従ってシステムをポーリングする必要があります、中に、プロバイダーがするように要求されたときに、サンプルを生成する拒否できますを注意してください。 ドメイン コントローラーの既定値は 10 です。 ドメイン メンバーの既定値は、15 です。 スタンドアロンのクライアントとサーバーの既定値は、15 です。  |
|MaxPosPhaseCorrection|すべての|このエントリは、サービスでは、秒単位で最大の正の時間の修正を指定します。 この値より大きな変更が必要であるサービスによって判断された場合は、代わりに、イベントが記録されます。 特殊なケース: 0 xffffffff 時間修正を常に行うことを意味します。 ドメイン メンバーの既定値は、0 xffffffff です。 スタンドアロンのクライアントとサーバーの既定値は 54,000 (15 時間) です。  |
|MinClockRate|すべての|このエントリは、W32Time で保持されます。 Windows オペレーティング システムで使用される予約済みのデータが含まれているし、この設定への変更が予期しない結果になることができます。 ドメイン メンバーの既定値は、155860 です。 スタンドアロンのクライアントとサーバーの既定値は、155860 です。  |
|MinPollInterval|すべての|このエントリは、システムのポーリング間隔の許可の log2 秒単位で最短の間隔を指定します。 システムでサンプルがこれよりも頻繁に要求しないときにプロバイダーは、スケジュールされた間隔の時間帯以外のサンプルを生成することができることに注意してください。 ドメイン コントローラーの既定値は、6 です。 ドメイン メンバーの既定値は 10 です。 スタンドアロンのクライアントとサーバーの既定値は 10 です。  |
|PhaseCorrectRate|すべての|このエントリは、フェーズ エラーを修正する速度を制御します。 小さい値を指定すると、すばやくフェーズ エラーを修正が不安定になるクロックが発生する可能性があります。 値が大きすぎる場合は、フェーズ エラーを解決するに時間がかかります。 <br /><br />ドメイン メンバーの既定値は 1 です。 スタンドアロンのクライアントとサーバーに既定値は、7 です。<br /><br />注: 0 は、PhaseCorrectRate レジストリ エントリの値が無効です。 Windows Server 2003、Windows Server 2003 R2、Windows Server 2008、および Windows Server 2008 R2 コンピューターでは、値が 0 に設定されている場合、Windows タイム サービスに自動的に変更を 1 にされます。  |
|PollAdjustFactor|すべての|このエントリは、システムのポーリング間隔の増減する意思決定を制御します。 値が大きい、エラーを減らすポーリング間隔の原因となる量は小さくなります。 ドメイン メンバーの既定値は 5 です。 スタンドアロンのクライアントとサーバーに既定値は 5 です。 |
|SpikeWatchPeriod|すべての|このエントリが疑わしいオフセットを保持する必要があります時間数を指定します (秒) を正しいと便利です前にします。 ドメイン メンバーの既定値は 900 です。 スタンドアロン クライアントおよびワークステーション上の既定値は 900 です。  |
|TimeJumpAuditOffset|すべての|秒単位で時刻のジャンプ監査しきい値を示す符号なし整数。 タイム サービスは、直接、時計の設定によって、ローカル クロックを調整時間修正は、この値を超える場合は、タイム サービスは監査イベントを記録します。|
|UpdateInterval|すべての|このエントリは、フェーズ補正の調整の間のクロック ティック数を指定します。 ドメイン コントローラーの既定値は 100 です。 ドメイン メンバーの既定値は、30,000 です。 スタンドアロンのクライアントとサーバーの既定値は、360,000 です。  <br /><br />**注:**: UpdateInterval レジストリ エントリの無効な値は 0 です。 Windows Server 2003、Windows Server 2003 R2、Windows Server 2008、および Windows Server 2008 R2 を実行するコンピューターで値が 0 に設定されている場合、Windows タイム サービスに自動的に、1 に変更します。<br /><br />次の 3 つのレジストリ エントリは、W32Time 既定の構成の一部ではないが、増加ログ機能を取得するためにレジストリに追加することができます。 システム イベント ログに記録された情報は、グループ ポリシー オブジェクト エディターで EventLogFlags 設定の値を変更することで変更できます。 既定では、新しいタイム ソースにできることが切り替わるたびに、タイム サービスはイベント ビューアーでログを作成します。<br /><br />**警告**: 一部のグループ ポリシー オブジェクト (GPO) 設定は、対応するとは異なるシステム管理用テンプレート ファイル (System.adm) で構成されているプリセット値の既定のレジストリ エントリ。 If you plan to use a GPO to configure any Windows Time setting, be sure that you review [Preset values for the Windows Time service Group Policy settings are different from the corresponding Windows Time service registry entries in Windows Server 2003](https://go.microsoft.com/fwlink/?LinkId=186066). この問題は、Windows Server 2008 R2、Windows Server 2008、Windows Server 2003 R2、および Windows Server 2003 に適用されます。 |
|UtilizeSslTimeData|Windows 10 ビルド 1511 を投稿します。|1 のエントリは、W32Time が複数の SSL のタイムスタンプを使用してがきわめて低い正確であるクロックをシードすることを示します。|

次のレジストリ エントリは、W32Time ログ記録を有効にするために追加する必要があります。  

|レジストリ エントリ|バージョン|説明|
|------------------------------------|---------------|----------------------------|
|FileLogEntries|すべての|このエントリは、Windows タイムのログ ファイルに作成されるエントリの量を制御します。 既定値は、none、Windows タイムに任意のアクティビティ ログに記録されません。 有効な値は、0 ~ 300 します。 この値では Windows タイムで作成された通常のイベント ログ エントリには影響しません|
|FileLogName|すべての|このエントリは、Windows タイム ログのファイルの名前と場所を制御します。 既定値が空白、および変更されていない限り必要があります**FileLogEntries**を変更します。 有効な値は、完全なパスとファイル名が、Windows タイムをログ ファイルの作成に使用するにです。 この値は、Windows タイムで作成された通常のイベント ログ エントリには影響しません。  |
|FileLogSize|すべての|このエントリは、Windows タイムのログ ファイルの循環ログの動作を制御します。 ときに**FileLogEntries**と**FileLogName**が定義されている場合、このエントリは定義のサイズ (バイト単位) を新しいエントリのログの最も古いエントリを上書きする前に到達するログ ファイルを許可するようにします。 任意の正の数値は、有効なと 3000000 をお勧めします。 この値は、Windows タイムで作成された通常のイベント ログ エントリには影響しません。  |



#### <a name="NtpClient"></a>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpClient

|レジストリ エントリ|バージョン|説明|
|------------------------------------|---------------|----------------------------|
|AllowNonstandardModeCombinations|すべての|このエントリは、標準モードの組み合わせがピア間の同期で許可されていることを示します。 ドメイン メンバーの既定値は 1 です。 スタンドアロンのクライアントとサーバーの既定値は 1 です。|
|CompatibilityFlags|すべての|このエントリは、次の互換性フラグと値を指定します。 <br /><br />-DispersionInvalid: 0x00000001  <br />-IgnoreFutureRefTimeStamp: 0x00000002  <br /> -AutodetectWin2K: 0x80000000  <br />-AutodetectWin2KStage2: 0x40000000  <br /><br />ドメイン メンバーの既定値は 0x80000000 です。 スタンドアロンのクライアントとサーバーの既定値は 0x80000000 です。  |
|CrossSiteSyncFlags|すべての|このエントリは、サービスが、コンピューターのドメインの外部の同期パートナーを選択するかどうかを決定します。 オプションと値は。  <br /><br />-なし: 0  <br />-PdcOnly: 1  <br />-All: 2  <br /><br />NT5DS 値が設定されていない場合、この値は無視されます。 ドメイン メンバーの既定値は 2 です。 スタンドアロンのクライアントとサーバーの既定値は 2 です。  |
|宣言されました。|すべての|このエントリは、タイム プロバイダの DLL の場所を指定します。  <br /><br />ドメインのメンバーとスタンドアロン クライアントとサーバーの両方でこの DLL の既定の場所は、%windir%\system32\w32time.dll です。|
|有効になっています。|すべての|このエントリは、現在のタイム サービスで NtpClient プロバイダーが有効になっているかどうかを示します。  <br /><ul><li>1 を [はい] します。</li><li>いいえ 0</li></ul>ドメイン メンバーの既定値は 1 です。 スタンドアロンのクライアントとサーバーに既定値は 1 です。|
|EventLogFlags|すべての|このエントリは、Windows タイム サービスによって記録されたイベントを指定します。<ul><li>0x1 到達可能性によって変更</li><li>0x2 大規模なサンプルずれ (これは Windows Server 2003、Windows Server 2003 R2、Windows Server 2008、および Windows Server 2008 R2 に該当するのみ)</li></ul>ドメイン メンバーの既定値は、0x1 です。 スタンドアロンのクライアントとサーバーに既定値は、0x1 です。|
|InputProvider|すべての|このエントリは、NtpClient プロバイダーが有効になっているかどうかを示します。  <ul><li>1 を [はい] します。  </li><li>いいえ 0 </li></ul>ドメイン メンバーの既定値は 1 です。 スタンドアロンのクライアントとサーバーに既定値は 1 です。  |
|LargeSampleSkew|すべての|このエントリは、大規模なサンプル スキューを秒単位でログに記録を指定します。 セキュリティと Exchange コミッション (秒) の仕様に準拠して、これは、3 秒に設定する必要があります。 EventLogFlags が大規模なサンプルについて 0x2 ずれ明示的に構成されている場合にのみこの設定のイベントが記録されます。 ドメイン メンバーの既定値は 3 です。 スタンドアロンのクライアントとサーバーに既定値は 3 です。  |
|ResolvePeerBackOffMaxTimes|すべての|このエントリは、待機が繰り返されたときの 2 倍に時間の最大数が、失敗と同期するピアを検索しようとしています。 を指定します。 値が 0 のでは、待機は、常に最低限ことを意味します。 ドメイン メンバーの既定値は、7 です。 スタンドアロンのクライアントとサーバーに既定値は、7 です。 |
|ResolvePeerBackoffMinutes|すべての|このエントリは、(分) と同期するピアの検索を試行する前に、待機する最初の間隔を指定します。 ドメイン メンバーの既定値は、15 です。 スタンドアロンのクライアントとサーバーに既定値は、15 です。  |
|SpecialPollInterval|すべての|このエントリは、手動のピアの秒単位の特別なポーリング間隔を指定します。 0x1 SpecialInterval フラグが有効な場合、W32Time は、ポーリング間隔ではなくこのポーリング間隔を決定オペレーティング システムでします。 ドメイン メンバーの既定値は、3,600 です。 スタンドアロンのクライアントとサーバーに既定値は、604,800 です。<br/><br/>新しいビルド 1702 は、MinPollInterval と MaxPollInterval Config レジストリ値によって SpecialPollInterval が含まれています。|
|SpecialPollTimeRemaining|すべての|このエントリは、W32Time で保持されます。 Windows オペレーティング システムで使用される予約済みのデータが含まれています。 コンピューターが再起動した後、W32Time が再同期するまでの秒の時間を指定します。 この設定への変更には、予期しない結果を可能性があります。 両方のドメインのメンバーとスタンドアロン クライアントとサーバーの既定値を空白のままになります。  |

#### <a name="NtpServer"></a>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpServer

|レジストリ エントリ|バージョン|説明|
|------------------------------------|---------------|----------------------------|
|AllowNonstandardModeCombinations|すべての|このエントリは、標準モードの組み合わせがクライアントとサーバー間の同期で許可されていることを示します。 ドメイン メンバーの既定値は 1 です。 スタンドアロンのクライアントとサーバーの既定値は 1 です。|
|宣言されました。|すべての|このエントリは、タイム プロバイダの DLL の場所を指定します。<br /><br />ドメインのメンバーとスタンドアロン クライアントとサーバーの両方でこの DLL の既定の場所は、%windir%\system32\w32time.dll です。  |
|有効になっています。|すべての|このエントリは、現在のタイム サービスで NtpServer プロバイダーが有効になっているかどうかを示します。 <ul><li>1 を [はい] します。</li><li>いいえ 0</li></ul>ドメイン メンバーの既定値は 1 です。 スタンドアロンのクライアントとサーバーに既定値は 1 です。  |
|InputProvider|すべての|このエントリは、NtpServer プロバイダーが有効になっているかどうかを示します。  <ul><li>1 を [はい] します。  </li><li>いいえ 0 </li></ul>ドメイン メンバーの既定値は 1 です。 スタンドアロンのクライアントとサーバーに既定値は 1 です。  |

#### <a name="MaxAllowedPhaseOffset"></a>MaxAllowedPhaseOffset 情報
W32Time を徐々 にコンピューターの時計を設定するためには、オフセットは MaxAllowedPhaseOffset 値未満にして、同時に、次の等式を満たしている必要があります。  
```  
|CurrentTimeOffset| / (PhaseCorrectRate*UpdateInterval) < SystemClockRate / 2  
``` 
CurrentTimeOffset はミリ秒 = 10,000 クロック ティック Windows システム上で位置のクロック刻みで測定されます。  
  
SystemClockRate と PhaseCorrectRate も、クロック ティック単位で測定されます。 SystemClockRate を取得する、次のコマンドを使用して、クロック ティック秒の数式を使用する時間を秒から変換 * 1000\ * 10000。  
  
```  
W32tm /query /status /verbose  
ClockRate: 0.0156000s  
```  
  
SystemclockRate では、システムの時計の率です。 156000 (秒) を使用して、例として、SystemclockRate は = 0.0156000 1000 * \ * 10000 = 156000 クロック ティック。  
  
MaxAllowedPhaseOffset は秒単位でもあります。 クロック ティックは変換、乗算 MaxAllowedPhaseOffset * 1000\ * 10000 です。  
  
次の 2 つの例を適用する方法を表示します。  
  
**例 1**: 4 分、時間とは異なります (たとえば、な午前 11 時 05 分の時間と、タイム サンプルが、ピアから受信したし、午前 11時 09分が適切であると考えられる)。  
```
phasecorrectRate = 1  
  
UpdateInterval = 30000 (clock ticks)  
  
systemclockRate = 156000 (clock ticks)  
  
MaxAllowedPhaseOffset = 10min = 600 seconds = 600*1000\*10000=6000000000 clock ticks  
  
|currentTimeOffset| = 4mins = 4*60\*1000\*10000 = 2400000000 ticks  
  
Is CurrentTimeOffset < MaxAllowedPhaseOffset?  
  
2400000000 < 6000000000 = TRUE  
```
上記の式が満たしてですか。 
```
(|CurrentTimeOffset| / (PhaseCorrectRate*UpdateInterval) < SystemClockRate / 2)  
  
Is 2,400,000,000 / (30000*1) < 156000/2  
  
Is 100,000 < 78,000  
  
NO/FALSE  
```  
したがって W32tm 設定のクロック戻るすぐにします。  
  
> [!NOTE]  
> この場合、戻さクロック速度が遅い場合は、TRUE で式の結果を得るも、PhaseCorrectRate または updateInterval レジストリ内の値を調整する必要があります。  
  
**例 2**: 3 分、時間とは異なります。  
```  
phasecorrectRate = 1  
  
UpdateInterval = 30000 (clock ticks)  
  
systemclockRate = 156000 (clock ticks)  
  
MaxAllowedPhaseOffset = 10min = 600 seconds = 600*1000\*10000=6000000000 clock ticks  
  
currentTimeOffset = 3mins = 3*60\*1000\*10000 = 1800000000 clock ticks  
  
Is CurrentTimeOffset < MaxAllowedPhaseOffset?  
  
1800000000 < 6000000000 = TRUE  
```  
上記の式が満たしてですか。
```
(|CurrentTimeOffset| / (PhaseCorrectRate*UpdateInterval) < SystemClockRate / 2)  
  
Is 3 mins (1,800,000,000) / (30000*1) < 156000/2  
  
Is 60,000 < 78,000  
  
YES/TRUE  
```  
ここでは、クロックは戻さ速度が遅い。  
  
## <a name="w2k3tr_times_tools_vwtt"></a>Windows タイム サービスのグループ ポリシー設定  
ほとんどの W32Time パラメーターは、グループ ポリシー オブジェクト エディターを使用して構成できます。 これは、信頼性の高いタイム ソースにするには、NTPServer または NTPClient、時刻の同期メカニズムを構成して、コンピューターを構成するコンピューターの構成が含まれます。  
  
> [!NOTE]  
> Windows タイム サービスのグループ ポリシー設定では、Windows Server 2003、Windows Server 2003 R2、Windows Server 2008、および Windows Server 2008 R2 のドメイン コントローラーで構成できます。 でき、Windows Server 2003、Windows Server 2003 R2、Windows Server 2008、および Windows Server 2008 R2 を実行しているコンピューターにのみ適用できます。  
  
設定、グループ ポリシー オブジェクト エディター スナップインで、次の場所で W32Time を構成するために使用するグループ ポリシーを確認することができます。  
  
-   コンピューターの構成 \ 管理 Templates\System\Windows タイム サービス  
  
    構成**グローバル構成設定**次のとおりです。  
  
-   コンピューター構成 \ 管理 Templates\System\Windows タイム Service\Time プロバイダー  
  
    構成**Windows NTP クライアント**設定を次のとおりです。  
  
    有効にする**Windows NTP クライアント**次のとおりです。  
  
    有効にする**Windows NTP サーバー**次のとおりです。  
  
> [!WARNING]  
> グループ ポリシー オブジェクト (GPO) 設定は既定の対応するレジストリ エントリとは異なるシステム管理用テンプレート ファイル (System.adm) で構成されているプリセット値の一部です。 If you plan to use a GPO to configure any Windows Time setting, be sure that you review [Preset values for the Windows Time service Group Policy settings are different from the corresponding Windows Time service registry entries in Windows Server 2003](https://go.microsoft.com/fwlink/?LinkId=186066). この問題は、Windows Server 2008 R2、Windows Server 2008、Windows Server 2003 R2、および Windows Server 2003 に適用されます。  
  
次の表は、Windows タイム サービスと各設定に関連付けられている事前に定義された値に関連付けられているグローバル グループ ポリシー設定を示します。 各設定の詳細については、対応するレジストリ エントリを参照してください。"[Windows タイム サービスのレジストリ値](#w2k3tr_times_tools_uhlp)"このトピックで前述しました。 呼ばれる 1 つの GPO で、次の設定が含まれている**グローバル構成設定**します。  
  
**Windows タイムに関連付けられているグローバル グループ ポリシーの設定**  
  
|グループ ポリシー設定|事前設定の値|  
|------------------------|------------------|  
|AnnounceFlags|10|  
|EventLogFlags|2|  
|FrequencyCorrectRate|4|  
|HoldPeriod|5|  
|LargePhaseOffset|1280000|  
|LocalClockDispersion|10|  
|MaxAllowedPhaseOffset|300|  
|MaxNegPhaseCorrection|54,000 (15 時間)|  
|MaxPollInterval|15|  
|MaxPosPhaseCorrection|54,000 (15 時間)|  
|MinPollInterval|10|  
|PhaseCorrectRate|7|  
|PollAdjustFactor|5|  
|SpikeWatchPeriod|90|  
|UpdateInterval|100|  
  
次の表に、利用可能な設定を**Windows NTP クライアントを構成する**GPO と、Windows タイム サービスに関連付けられている事前設定の値。 各設定の詳細については、対応するレジストリ エントリを参照してください。"[Windows タイム サービスのレジストリ値](#w2k3tr_times_tools_uhlp)"このトピックで前述しました。  
  
**Windows タイムに関連付けられている NTP クライアントのグループ ポリシーの設定**  
  
|グループ ポリシー設定|既定値|  
|------------------------|-----------------|  
|NtpServer|time.windows.com、0x1|  
|種類|既定のオプション:<br /><br />-   **NTP します。** ドメインに参加していないコンピューターで使用します。<br />-   **NT5DS です。** ドメインに参加しているコンピューターで使用します。|  
|CrossSiteSyncFlags|2|  
|ResolvePeerBackoffMinutes|15|  
|ResolvePeerBackoffMaxTimes|7|  
|SpecialPollInterval|3600|  
|EventLogFlags|0|  
  
## <a name="w2k3tr_times_tools_suxb"></a>Windows タイム サービスによって使用されるネットワーク ポート  
Windows タイムには、すべての時間同期通信 UDP ポート 123 の使用を必要とする NTP 仕様が次に示します。 このポートは Windows タイムで予約されているし、予約は常にします。 その時計の同期、コンピューターや、別のコンピューターに時刻を提供するたびに、その通信は、UDP ポート 123 で行われます。  
  
> [!NOTE]  
> 複数のネットワーク アダプター (マルチホーム コンピューターとも呼ばれます) を備えたコンピューターがあれば、選択的にネットワーク アダプターに基づく Windows タイム サービスを有効にすることはできません。  
  
## <a name="w2k3tr_times_tools_qoep"></a>関連情報  
次のリソースには、このセクションに関連する追加の情報が含まれます。  
  
-   RFC *1305* 、IETF RFC データベースで  

