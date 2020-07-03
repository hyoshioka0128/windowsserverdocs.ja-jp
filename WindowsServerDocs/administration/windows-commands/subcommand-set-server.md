---
title: サブコマンドの設定-サーバー
description: Windows 展開サービスサーバーの設定を構成したサブコマンドのセットサーバーのリファレンス記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: da55c29d-a94a-4d73-877b-af480f906ca0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 26920f8e501d1f802e18bbce7bc3980955d23e0a
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85936984"
---
# <a name="subcommand-set-server"></a>サブコマンド: セット サーバー

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows 展開サービス サーバーの設定を構成します。

## <a name="syntax"></a>構文
```
wdsutil [Options] /Set-Server [/Server:<Server name>]
    [/Authorize:{Yes | No}]
    [/RogueDetection:{Yes | No}]
    [/AnswerClients:{All | Known | None}]
    [/Responsedelay:<time in seconds>]
    [/AllowN12forNewClients:{Yes | No}]
    [/ArchitectureDiscovery:{Yes | No}]
    [/resetBootProgram:{Yes | No}]
    [/DefaultX86X64Imagetype:{x86 | x64 | Both}]
    [/UseDhcpPorts:{Yes | No}]
    [/DhcpOption60:{Yes | No}]
    [/RpcPort:<Port number>]
    [/PxepromptPolicy
        [/Known:{OptIn | Noprompt | OptOut}]
        [/New:{OptIn | Noprompt | OptOut}]
    [/BootProgram:<Relative path>]
         /Architecture:{x86 | ia64 | x64}
    [/N12BootProgram:<Relative path>]
         /Architecture:{x86 | ia64 | x64}
    [/BootImage:<Relative path>]
         /Architecture:{x86 | ia64 | x64}
    [/PreferredDC:<DC Name>]
    [/PreferredGC:<GC Name>]
    [/PrestageUsingMAC:{Yes | No}]
    [/NewMachineNamingPolicy:<Policy>]
    [/NewMachineOU]
         [/type:{Serverdomain | Userdomain | UserOU | Custom}]
         [/OU:<Domain name of OU>]
    [/DomainSearchOrder:{GCOnly | DCFirst}]
    [/NewMachineDomainJoin:{Yes | No}]
    [/OSCMenuName:<Name>]
    [/WdsClientLogging]
         [/Enabled:{Yes | No}]
         [/LoggingLevel:{None | Errors | Warnings | Info}]
    [/WdsUnattend]
         [/Policy:{Enabled | Disabled}]
         [/CommandlinePrecedence:{Yes | No}]
         [/File:<path>]
             /Architecture:{x86 | ia64 | x64}
    [/AutoaddPolicy]
         [/Policy:{AdminApproval | Disabled}]
         [/PollInterval:{time in seconds}]
         [/MaxRetry:{Retries}]
         [/Message:<Message>]
         [/RetentionPeriod]
             [/Approved:<time in days>]
             [/Others:<time in days>]
    [/AutoaddSettings]
         /Architecture:{x86 | ia64 | x64}
         [/BootProgram:<Relative path>]
         [/ReferralServer:<Server name>
         [/WdsClientUnattend:<Relative path>]
         [/BootImage:<Relative path>]
         [/User:<Owner>]
         [/JoinRights:{JoinOnly | Full}]
         [/JoinDomain:{Yes | No}]
    [/BindPolicy]
         [/Policy:{Include | Exclude}]
         [/add]
              /address:<IP or MAC address>
              /addresstype:{IP | MAC}
         [/remove]
              /address:<IP or MAC address>
              /addresstype:{IP | MAC}
    [/RefreshPeriod:<time in seconds>]
    [/BannedGuidPolicy]
         [/add]
              /Guid:<GUID>
         [/remove]
             /Guid:<GUID>
    [/BcdRefreshPolicy]
         [/Enabled:{Yes | No}]
         [/RefreshPeriod:<time in minutes>]
    [/Transport]
         [/ObtainIpv4From:{Dhcp | Range}]
             [/start:<start IP address>]
             [/End:<End IP address>]
         [/ObtainIpv6From:Range]
             [/start:<start IP address>]
             [/End:<End IP address>]
         [/startPort:<start Port>
             [/EndPort:<start Port>
        [/Profile:{10Mbps | 100Mbps | 1Gbps | Custom}]
        [/MulticastSessionPolicy]
             [/Policy:{None | AutoDisconnect | Multistream}]
                 [/Threshold:<Speed in KBps>]
                 [/StreamCount:{2 | 3}]
                 [/Fallback:{Yes | No}]
        [/forceNative]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
|[承認]、[: {[はい] (& a) #124 文字です。No}]|動的ホスト制御プロトコル (DHCP) でこのサーバーを承認するかどうかを指定します。|
|[/RogueDetection: {[はい] (& a) #124 文字です。No}]|有効または DHCP 承認されていない検出を無効にします。|
|[/AnswerClients: {All と #124 文字です。正常および #124 文字です。None}]|どのクライアントがこのサーバーは応答を指定します。 この値を [**既知**] に設定すると、コンピューターは、Windows 展開サービスサーバーによって応答される前に、Active Directory ドメインサービス (AD DS) で事前登録されている必要があります。|
|[/Responsedelay: <time in seconds> ]|起動クライアントに応答する前に、サーバーが待機する時間数。 この設定は、事前設定されたコンピューターには適用されません。|
|[/Allown12fornewclients: {Yes &#124; No}]|Windows Server 2008 では、不明なクライアントが F12 キーを押してネットワークブートを開始する必要がないことを指定します。 既知のクライアントが指定されているブート プログラムを受信するか、または、指定しない場合、ブート プログラム指定アーキテクチャです。<p>Windows Server 2008 R2 では、このオプションは次のコマンドに置き換えられました: wdsutil/Set-Server/PxepromptPolicy/New: Noprompt|
|[/ArchitectureDiscovery: {[はい] (& a) #124 文字です。No}]|有効またはアーキテクチャの検出を無効にします。 これには、そのアーキテクチャを正しくブロードキャストしない x64 ベースのクライアントの検出が容易になります。|
|[/resetBootProgram: {Yes &#124; No}]|クライアントが F12 キーの押下を必要とせず起動したばかりのブート パスが消去されるかどうかを決定します。|
|[/Defaultx86x64imagetype: {x86 &#124; x64 &#124; 両方}]|ブート イメージのコントロールは、x64 ベースのクライアントに表示されます。|
|[/UseDhcpPorts: {[はい] (& a) #124 文字です。No}]|指定 TCP ポート 67 で PXE サーバーは、DHCP のポートにバインドしようとする必要があります、かどうか。 DHCP と Windows 展開サービスを同じコンピューターで実行している場合このオプションを設定する必要があります **いいえ** 、ポートを利用し、設定するには、DHCP サーバーを有効にする、 **/DhcpOption60** パラメーターを **はい**します。 この値は、の既定の設定 **はい**します。|
|[/DhcpOption60: {[はい] (& a) #124 文字です。No}]|PXE サポートのために、DHCP オプション 60 を構成するかどうかを指定します。 DHCP と Windows 展開サービスを同じサーバーで実行している場合は、このオプションを設定 **はい** し、設定、 **/UseDhcpPorts** オプションを **いいえ**します。 この値は、の既定の設定 **いいえ**します。|
|[/RpcPort:<Port number>]|クライアント要求を使用する TCP ポート番号を指定します。|
|[/PxepromptPolicy]|構成方法既知 (事前設定された) し、新しいクライアントが PXE ブートを開始します。 このオプションは、Windows Server 2008 R2 のみに適用されます。 次のオプションを使用して設定を設定します。<p>-[/既知: {OptIn&#124;OptOut&#124;Noprompt}]-事前設定されたクライアントのポリシーを設定します。<br />-[/New: {OptIn&#124;OptOut&#124;Noprompt}]-新しいクライアントのポリシーを設定します。<p>**OptIn** 手段は、クライアントが PXE ブートするためにキーを押す必要があります、それ以外の場合がフォールバックして、次のブート デバイスです。<p>**Noprompt**は、クライアントが常に PXE ブートであることを意味します。<p>**OptOut** 、Esc キーが押されていない限り、クライアントが PXE ブートすることを意味します。|
|[/BootProgram:<Relative path>]/アーキテクチャ: {x86 & #124; ia64 & #124; x64}|RemoteInstall フォルダー内のブートプログラムへの相対パス ( **boot\x86\pxeboot.n12**など) を指定し、ブートプログラムのアーキテクチャを指定します。|
|[/N12BootProgram:<Relative path>]/アーキテクチャ: {x86 & #124; ia64 & #124; x64}|F12 キーを押すことを必要としないブート プログラムへの相対パスを指定します (たとえば、 **boot\x86\pxeboot.n12**)、ブート プログラムのアーキテクチャを指定するとします。|
|[/ブート イメージ:<Relative path>]/アーキテクチャ: {x86 & #124; ia64 & #124; x64}|ブート イメージを起動するクライアントを受信する必要があり、ブート イメージのアーキテクチャを指定の相対パスを指定します。 これは、アーキテクチャごとに指定できます。|
|[/PreferredDC:<DC Name>]|Windows 展開サービスが使用するドメイン コント ローラーの名前を指定します。 NetBIOS 名または FQDN を指定できます。|
|[/PreferredGC:<GC Name>]|Windows 展開サービスが使用するグローバル カタログ サーバーの名前を指定します。 NetBIOS 名または FQDN を指定できます。|
|[/PrestageUsingMAC: {[はい] (& a) #124 文字です。No}]|かどうか、AD DS でコンピューター アカウントを作成するときに、Windows 展開サービスなく使用する MAC アドレスの GUID/UUID コンピューターを識別するためを指定します。|
|[/NewMachineNamingPolicy:<Policy>]|クライアント用のコンピューター名を生成するときに使用する形式を指定します。 に使用する形式の詳細については、 <policy> mmc スナップインでサーバーを右クリックし、[**プロパティ**] をクリックして、[**ディレクトリサービス**] タブを表示します。たとえば、 **/NewMachineNamingPolicy:% 61Username% # のよう**になります。|
|[/NewMachineOU]|クライアント コンピューターのアカウントを作成するために使用を AD DS の場所を指定します。 次のオプションを使用して場所を指定します。<p>-[/type: Serverdomain &#124; Userdomain &#124; Userdomain &#124; カスタム] 場所の種類を指定します。 **Serverdomain**は、Windows 展開サービスサーバーと同じドメインにアカウントを作成します。 **Userdomain**は、インストールを実行するユーザーと同じドメインにアカウントを作成します。 **UserOU** インストールを実行するユーザーの組織単位にアカウントを作成します。 **カスタム** カスタムの場所を指定することができます (の値を指定する必要がありますも **/OU** このオプションを使用して)。<br />-[/OU: <Domain name of OU> ]- **/type**オプションに**カスタム**を指定した場合、このオプションでは、コンピューターアカウントを作成する組織単位を指定します。|
|[/DomainSearchOrder: {GCOnly & #124 文字です。DCFirst}]|AD DS (グローバル カタログまたはドメイン コント ローラー) でコンピューター アカウントを検索するためのポリシーを指定します。|
|[/NewMachineDomainJoin: {[はい] (& a) #124 文字です。No}]|インストール中に、AD DS に既に事前登録されていないコンピューターをドメインに参加する必要があるかどうかを指定します。 既定の設定は **[はい]** です。|
|[/WdsClientLogging]|サーバーのログ記録レベルを指定します。<p>-[/有効にします。 {[はい] (& a) #124 文字です。No}] - 有効または、Windows 展開サービス クライアントのアクションのログ記録を無効にします。<br />-[/LoggingLevel: {なしと #124 文字です。エラーと #124 文字です。警告と #124 文字です。Info} - は、ログ記録レベルを設定します。 **[なし]** ログ記録を無効にすることと同じです。 **エラー** ログの最下位レベルは、エラーのみを記録することを示します。 **警告** 警告およびエラーの両方が含まれています。 **情報** 最高レベルのログ記録は、エラー、警告、および情報イベントが含まれています。|
|[/WdsUnattend]|これらの設定は、Windows 展開サービス クライアントの無人インストールの動作を制御します。 次のオプションを使用して設定を設定します。<p>-[/ポリシー: {有効になっている (& a) #124 文字です。無効になっている}] - 無人インストールを使用するかどうかを指定します。<br />-[/CommandlinePrecedence: {[はい] (& a) #124 文字です。No}] -、Autounattend.xml ファイル (存在する場合、クライアント上) または/Unattend オプションを使用して Windows 展開サービス クライアントに直接渡された無人セットアップ ファイルを使用するかイメージ無人セットアップ ファイルではなくクライアントのインストール中に指定します。 既定の設定は [**いいえ**] です。<br />-[/File:<Relative path> /Architecture: {x86 & #124; ia64 & #124; x64}]-ファイル名、パス、および無人セットアップ ファイルのアーキテクチャを指定します。|
|[/Autoaddpolicy]|これらの設定は、自動追加ポリシーを制御します。 次のオプションを使用して設定を定義します。<p>-[/ポリシー: {AdminApproval & #124 文字です。無効になっている}] - **AdminApprove** により、管理者をコンピューターの一覧を確認し、承認または拒否必要に応じて、各要求を保留中のキューに追加するすべての不明なコンピューターです。 **無効になっている** 不明なコンピューターが、サーバーを起動しようとしたときに、追加のアクションが実行しないことを示しています。<br />-[/PollInterval: {時間 (秒)}]-ネットワークブートプログラムが Windows 展開サービスサーバーをポーリングする間隔 (秒) を指定します。<br />-[/MaxRetry: <Number>]-ネットワーク ブート プログラムが Windows 展開サービス サーバーをポーリングする回数を指定します。 この値は、 **/PollInterval**と共に、管理者がコンピューターを承認または拒否するまでの待ち時間を指定します。この時間が経過すると、タイムアウトします。たとえば、 **Maxretry**値が10で、 **PollInterval** vlue が60の場合、クライアントはサーバーを10回ポーリングする必要があることを示しています。これは、試行が60秒間待機していることを示します。 そのため、クライアントは、10 分 (10 × 60 秒 = 10 分) 後にタイムアウトとします。<br />-[/メッセージ: <Message>]-クライアント ネットワーク ブート プログラム] ダイアログ ページに表示されるメッセージを指定します。<br />-[/RetentionPeriod] - は、コンピューターが自動的に消去される前に、保留中の状態になるまでの日数を指定します。<br />-[承認]、[: <time in days>]-承認済みのコンピュータの保有期間を指定します。 このパラメーターを使用する必要があります、 **/RetentionPeriod** オプション。<br />-[/他のユーザー: <time in days>]-許可されていないコンピューターの保有期間を指定します (拒否または保留中)。 このパラメーターを使用する必要があります、 **/RetentionPeriod** オプション。|
|[/Autoaddsettings]|各コンピューターに適用される既定の設定を指定します。 次のオプションを使用して設定を定義します。<p>-/Architecture: {x86 & #124; ia64 & #124; x64} のアーキテクチャを指定します。<br />-[/BootProgram: <Relative path>]-承認済みのコンピューターに送信されたブート プログラムを指定します。 ブート プログラムが指定されていない場合 (サーバーの指定) と同じコンピューターのアーキテクチャの既定値が使用されます。<br />-[/WdsClientUnattend: <Relative path>]-承認されているクライアントが受け取る必要のある無人セットアップ ファイルに相対パスを設定します。<br />-[/ReferralServer: <Server name>]-クライアントを使用してイメージをダウンロードする Windows 展開サービス サーバーを指定します。<br />-[/ブート イメージ: <Relative path>]-承認されたクライアントは、ブート イメージを指定します。<br />-[/User: <Domain\User &#124; User@Domain>]-コンピューターアカウントオブジェクトのアクセス許可を設定し、指定したユーザーにコンピューターをドメインに参加させるために必要な権限を付与します。<br />-[JoinRights: {JoinOnly & #124 文字です。完全}] で、ユーザーに割り当てられる権限の種類を指定します。 **JoinOnly** 管理者ユーザーでコンピューターをドメインに参加する前に、コンピューター アカウントをリセットする必要があります。 **完全** フル アクセスをコンピューターをドメインに参加させる権限を含む、ユーザーに与えられます。<br />-[/JoinDomain: {[はい] (& a) #124 文字です。No}] - かどうか、コンピューターを参加させるドメインとしてこのコンピューター アカウントを Windows 展開サービスのインストール中に指定します。 既定の設定は **[はい]** です。|
|[/BindPolicy]|リッスンするように PXE プロバイダーのネットワーク インターフェイスを構成します。 次のオプションを使用して、ポリシーを定義します。<p>-[/ポリシー: {含める (& a) #124 文字です。除外}] - インターフェイスの一覧でアドレス、または除外するインターフェイスのバインド ポリシーを設定します。<br />-[/add]-リストにインターフェイスを追加します。 また、/addresstype および/addressも指定する必要があります。<br />-[/remove]-一覧からインターフェイスを削除します。 また、/addresstype および/addressも指定する必要があります。<br />-/address: <IP or MAC address> -追加または削除するインターフェイスの IP アドレスまたは MAC アドレスを指定します。<br />-/addresstype: {IP &#124; MAC}- **/address**オプションで指定されたアドレスの種類を示します。|
|[/RefreshPeriod: <seconds>]|設定の更新サーバーがどのくらいの頻度 (秒) を指定します。|
|[/BannedGuidPolicy]|次のオプションを使用して、禁止されている Guid の一覧を管理します。<p>-[/add]/Guid: <GUID> -指定した guid を、禁止されている guid の一覧に追加します。 この GUID を持つ任意のクライアントは、MAC アドレスによって識別されます。<br />-[/remove]/Guid: <GUID> -指定された guid を禁止されている guid の一覧から削除します。|
|[/BcdRefreshPolicy]|次のオプションを使用して、Bcd ファイルを更新するための設定を構成します。<p>-[/有効: {Yes &#124; No}]-Bcd 更新ポリシーを指定します。 [**有効** **] を [はい]** に設定すると、指定した時間間隔で Bcd ファイルが更新されます。<br />-[/Refreshperiod: <time in minutes> ]-Bcd ファイルを更新する時間間隔を指定します。|
|[/Transport]|次のオプションを構成します。<p><ul><li>[/ObtainIpv4From: {Dhcp & #124 文字です。範囲}] - IPv4 アドレスのソースを指定します。<p><ul><li>[/start: <starting Ipv4 address> ]-IP アドレス範囲の開始を指定します。 このオプションは必須であり、 **/ObtainIpv4From**が**Range**に設定されている場合にのみ有効です。</li><li>[/End: <Ending Ipv4 address>]-IP アドレスの範囲の末尾を指定します。 このオプションは、必要な場合にのみ有効な **/ObtainIpv4From** に設定されている **範囲**します。</li></ul></li><li>[/ObtainIpv6From: 範囲][/start: <start IP address> ][/End: <End IP address> ] IPv6 アドレスのソースを指定します。 このオプションは、Windows Server 2008 R2 にのみ適用され、サポートされている値の範囲。</li><li>[/startPort: <starting port> ]-ポート範囲の開始を指定します。</li><li>[/EndPort: <Ending port>]-ポートの範囲の末尾を指定します。</li><li>[/Profile: {10 mbps (& a) #124; 100 mbps & #124; 1 gbps & #124 文字です。カスタム}] - は、使用するネットワーク プロファイルを指定します。 このオプションは、Windows Server 2008 を実行しているサポートされている forservers のみです。</li><li>[/MulticastSessionPolicy] マルチキャスト転送の設定を構成します。 このコマンドでは、Windows Server 2008 R2 の使用のみです。<p><ul><li>[/ポリシー: {なしと #124 文字です。自動切断 & #124 文字です。複数ストリーム}] には、低速なクライアントの処理方法を決定します。 [なし] は、すべてのクライアントを同じ速度での 1 つのセッションを維持することです。 自動切断は、指定した/Threshold より下にあるすべてのクライアントが切断されますを意味します。 複数ストリームは、クライアントが/StreamCount で指定された複数のセッションに区切られるようにを意味します。</li><li>[/しきい値: <Speed in KBps> ]-/ポリシー: 自動切断では、このオプションによって最小転送速度 (KBps) が設定されます。 この速度より下にあるクライアントがマルチキャスト転送から切断されます。</li><li>[/Streamcount: {2 &#124; 3}][/フォールバック: {Yes &#124; No}]-/ポリシー: 複数ストリームの場合、このオプションはセッションの数を決定します。 2 は、2 つのセッション (高速で低速) 3 は 3 つのセッション (低速、中、高速) を意味します。</li><li>[フォールバック/: {[はい] (& a) #124 文字です。No}] - 切断されているクライアントが (クライアントがサポートされている) 場合は、別のメソッドを使用して転送を続行するかどうかを決定します。 WDS クライアントを使用している場合は、コンピューターのユニキャストへのフォールバック動作します。 Wdsmcast.exe は、フォールバック メカニズムをサポートしていません。 このオプションは、複数ストリームをサポートしていないクライアントにも適用されます。 その場合は、コンピューターは、低速の転送セッションに移動させる代わりに別のメソッドに戻る分類されます。</li></ul></li></ul>|
## <a name="examples"></a>例
4 分の応答の遅延時間での既知クライアントに応答するサーバーを設定するには、次のように入力します。
```
wdsutil /Set-Server /AnswerClients:Known /Responsedelay:4
```
サーバーのブート プログラムとアーキテクチャを設定するには、次のように入力します。
```
wdsutil /Set-Server /BootProgram:boot\x86\pxeboot.n12 /Architecture:x86
```
サーバーのログを有効にするには、次のように入力します。
```
wdsutil /Set-Server /WdsClientLogging /Enabled:Yes /LoggingLevel:Warnings
```
有効にする、サーバーおよびアーキテクチャやクライアントの無人セットアップ ファイルの種類に無人セットアップします。
```
wdsutil /Set-Server /WdsUnattend /Policy:Enabled /File:WDSClientUnattend \unattend.xml /Architecture:x86
```
ブート前実行環境 (PXE) サーバーを、TCP ポート67および60へのバインドを試行するように設定するには、次のように入力します。
```
wdsutil /Set-server /UseDhcpPorts:No /DhcpOption60:Yes
```
## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のキー](command-line-syntax-key.md) 
[サーバーの無効化コマンド](using-the-disable-server-command.md) 
 の使用[Enable Server コマンド](using-the-enable-server-command.md) 
 の使用[Get Server コマンド](using-the-get-server-command.md) 
 の使用[Initialize-Server コマンド](using-the-initialize-server-command.md) 
 の使用[サブコマンド: start-Server](subcommand-start-server.md) 
[サブコマンド: サーバー](subcommand-stop-server.md) 
 の停止[初期化解除サーバーオプション](the-uninitialize-server-option.md)
