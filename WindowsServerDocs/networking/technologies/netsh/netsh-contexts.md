---
title: Netsh コマンドの構文、コンテキスト、形式
description: このトピックを使用すると、netsh コンテキストおよびサブコンテキストを入力し、netsh 構文とコマンドの書式を理解するのに方法と Windows Server 2016 または Windows 10 を実行しているローカルおよびリモートのコンピューターでの netsh コマンドを実行するのに方法について説明します。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 8cb9b59f-0255-4261-b49a-562c5ea50ee0
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: adb77d841ba4d69b0d36bc7f19d4707638530c97
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823693"
---
# <a name="netsh-command-syntax-contexts-and-formatting"></a>Netsh コマンドの構文、コンテキスト、形式

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックを使用すると、netsh コンテキストおよびサブコンテキストを入力し、netsh 構文とコマンドの書式を理解するのに方法と、ローカルおよびリモート コンピューターでの netsh コマンドを実行するのに方法について説明します。

Netsh は、表示または現在実行中のコンピューターのネットワーク構成を変更することができるようにするコマンド ライン スクリプト ユーティリティです。 Netsh コマンドは、netsh プロンプトからコマンドを入力して実行できるし、バッチ ファイルまたはスクリプトで使用できます。 Netsh コマンドを使用して、リモート コンピューターとローカル コンピューターを構成できます。

また、指定したコンピューターに対して一連のコマンドをバッチ モードで実行できるスクリプト機能も備えています。 netsh では、構成スクリプトをテキスト ファイルに保存して、アーカイブとして保管したり、他のコンピューターの構成に利用したりできます。

## <a name="netsh-contexts"></a>Netsh コンテキスト

その他のオペレーティング システムのコンポーネントを使用して動的な対話 Netsh\-リンク ライブラリ\(DLL\)ファイル。 

各 netsh ヘルパー DLL が広範なセットと呼ばれる機能を提供する*コンテキスト*、ネットワーク サーバーの役割または機能に固有のコマンドのグループであります。 これらのコンテキストでは、構成を提供して、1 つまたは複数のサービス、ユーティリティ、またはプロトコルのサポートを監視しての netsh 機能を拡張します。 たとえば、Dhcpmon.dll コンテキストおよび構成し、DHCP サーバーの管理に必要なコマンドのセットで netsh を提供します。

### <a name="obtain-a-list-of-contexts"></a>コンテキストの一覧を取得します。

Windows Server 2016 または Windows 10 を実行するコンピューターでコマンド プロンプトまたは Windows PowerShell のいずれかを開くことで、netsh コンテキストの一覧を取得できます。 コマンドを入力して**netsh** ENTER キーを押します。 型 **/でしょうか。**、し、ENTER キーを押します。

Windows Server 2016 Datacenter を実行しているコンピューターでこれらのコマンドの出力例を次に示します。

    PS C:\Windows\system32> netsh
    netsh>/?
    
    The following commands are available:
    
    Commands in this context:
    ..            - Goes up one context level.
    ?             - Displays a list of commands.
    abort         - Discards changes made while in offline mode.
    add           - Adds a configuration entry to a list of entries.
    advfirewall   - Changes to the `netsh advfirewall' context.
    alias         - Adds an alias.
    branchcache   - Changes to the `netsh branchcache' context.
    bridge        - Changes to the `netsh bridge' context.
    bye           - Exits the program.
    commit        - Commits changes made while in offline mode.
    delete        - Deletes a configuration entry from a list of entries.
    dhcpclient    - Changes to the `netsh dhcpclient' context.
    dnsclient     - Changes to the `netsh dnsclient' context.
    dump          - Displays a configuration script.
    exec          - Runs a script file.
    exit          - Exits the program.
    firewall      - Changes to the `netsh firewall' context.
    help          - Displays a list of commands.
    http          - Changes to the `netsh http' context.
    interface     - Changes to the `netsh interface' context.
    ipsec         - Changes to the `netsh ipsec' context.
    ipsecdosprotection - Changes to the `netsh ipsecdosprotection' context.
    lan           - Changes to the `netsh lan' context.
    namespace     - Changes to the `netsh namespace' context.
    netio         - Changes to the `netsh netio' context.
    offline       - Sets the current mode to offline.
    online        - Sets the current mode to online.
    popd          - Pops a context from the stack.
    pushd         - Pushes current context on stack.
    quit          - Exits the program.
    ras           - Changes to the `netsh ras' context.
    rpc           - Changes to the `netsh rpc' context.
    set           - Updates configuration settings.
    show          - Displays information.
    trace         - Changes to the `netsh trace' context.
    unalias       - Deletes an alias.
    wfp           - Changes to the `netsh wfp' context.
    winhttp       - Changes to the `netsh winhttp' context.
    winsock       - Changes to the `netsh winsock' context.
    
    The following sub-contexts are available:
     advfirewall branchcache bridge dhcpclient dnsclient firewall http interface ipsec ipsecdosprotection lan namespace netio ras rpc trace wfp winhttp winsock
    
    To view help for a command, type the command, followed by a space, and then
     type ?.


### <a name="subcontexts"></a>サブコンテキスト

Netsh コンテキストは、コマンドと呼ばれる追加のコンテキストの両方を含めることができます*サブコンテキスト*します。 たとえば、ルーティングのコンテキスト内で IP と IPv6 のサブコンテキストを変更できます。

コマンドと、netsh プロンプトから、コンテキスト内で使用できるサブコンテキストの一覧を表示するコンテキスト名を入力し、いずれかを入力 **/でしょうか。** または**ヘルプ**します。 たとえば、netsh プロンプトから、ルーティング コンテキストでサブコンテキストと使用できるコマンドの一覧を表示する\(、 **netsh&gt;**\)次のいずれかを入力します。

**ルーティング/でしょうか。**

**ルーティングのヘルプ**

現在のコンテキストから変更することがなく、別のコンテキストでタスクを実行するには、netsh プロンプトから使用するコマンドのコンテキストのパスを入力します。 たとえば、IGMP コンテキストで、netsh プロンプトからの IGMP コンテキストに最初に変更することがなく「ローカル エリア接続」をという名前のインターフェイスを追加する次のように入力します。

**「ローカル エリア接続」startupqueryinterval のインターフェイスを追加する ip igmp ルーティング = 21**

## <a name="running-netsh-commands"></a>Netsh コマンドを実行しています。

Netsh コマンドを実行する必要があります開始する netsh コマンド プロンプトから」と入力して**netsh**し、ENTER キーを押します。 次に、使用するコマンドを格納しているコンテキストに変更することができます。 使用可能なコンテキストでは、インストールされているネットワーク コンポーネントに依存します。 たとえば、入力した**dhcp** netsh プロンプトで ENTER キーを押して、netsh は、DHCP サーバーのコンテキストに変更します。 DHCP がインストールされていない場合は、次のメッセージが表示されます。

**次のコマンドが見つかりませんでした。 dhcp します。**

## <a name="formatting-legend"></a>凡例の書式設定

次の書式設定の凡例を使用して、解釈して、netsh プロンプトまたはバッチ ファイルまたはスクリプトでコマンドを実行するときに、正しい netsh コマンドの構文を使用することができます。

- 内のテキスト*斜体*情報コマンドを入力するときに指定する必要があります。 たとえば、次のコマンドは、という名前のパラメーター*UserName*、実際のユーザー名を入力する必要があります。
- 内のテキスト**太字**情報が表示され、コマンドを入力したとおりに入力する必要があります。
- テキストの省略記号が続く\(.\)をパラメーターでは、コマンドラインで繰り返すことができます。
- テキストは角かっこの間にある [&nbsp;] は省略可能な項目です。
- 中かっこの間にあるテキスト {&nbsp;} パイプで区切られた選択肢を提供する必要がありますを選択する 1 つだけなどの選択肢のセット`{enable|disable}`します。
- 等幅フォントでフォーマットされたテキストは、コードまたはプログラムの出力を示します。

## <a name="running-netsh-commands-from-the-command-prompt-or-windows-powershell"></a>コマンド プロンプトまたは Windows PowerShell からの Netsh コマンドを実行しています。

Netsh コマンド プロンプトまたは Windows PowerShell での入力ネットワーク シェルを起動して、するには、次のコマンドを使用できます。

### <a name="netsh"></a>netsh

Netsh は、ローカルまたはリモートで表示または実行中のコンピューターのネットワーク構成を変更することができるコマンド ライン スクリプト ユーティリティです。 パラメーターを指定せずに使用される**netsh** Netsh.exe コマンド プロンプトを開きます\(つまり**netsh&gt;**\)します。

#### <a name="syntax"></a>構文

**netsh** \[ **-a**&nbsp;*-a エイリアス ファイル名*\] \[ **-c** &nbsp; *コンテキスト* \] \[ **-r**&nbsp;*RemoteComputer* \] \[ **-u** \[ *DomainName\\*  \] *UserName* \] \[ **-p** &nbsp;*パスワード* |  \* \] \[{*NetshCommand* | **-f** &nbsp;*ScriptFile*}\]

#### <a name="parameters"></a>パラメーター

**`-a`**

(省略可能)。 戻ることを指定します、 **netsh**実行した後はプロンプト *-a エイリアス ファイル名*します。

**`AliasFile`**

任意。 1 つまたは複数を含むテキスト ファイルの名前を示す**netsh**コマンド。

**`-c`**

任意。 その netsh を指定した入力を指定します。 **netsh**コンテキスト。

**`Context`**

任意。 指定します、 **netsh**を入力するコンテキスト。 

**`-r`**

任意。 リモート コンピューターで実行するコマンドを追加することを指定します。

>[!IMPORTANT]
>使用するといくつかの netsh コマンド リモートで別のコンピューターに、 **netsh – r**パラメーター、リモート レジストリ サービスは、リモート コンピューターで実行する必要があります。 実行されていない場合、Windows には、"ネットワーク パスが見つかりません"というエラー メッセージが表示されます。

***`RemoteComputer`***

(省略可能)。 構成するリモート コンピューターを指定します。

**`-u`**

任意。 ユーザー アカウントでの netsh コマンドを実行することを指定します。

***`DomainName\\`***

任意。 ユーザー アカウントが配置されているドメインを指定します。 場合、既定値は、ローカル ドメイン*DomainName\\* が指定されていません。

***`UserName`***

(省略可能)。 ユーザー アカウント名を指定します。

**`-p`**

(省略可能)。 ユーザー アカウントのパスワードを指定することを指定します。

***`Password`***

任意。 指定したユーザー アカウントのパスワードを指定します **-u** *UserName*します。

***`NetshCommand`***

(省略可能)。 指定します、 **netsh**を実行するコマンド。

**`-f`**

任意。 終了**netsh**で指定したスクリプトの実行後*ScriptFile*します。

***`ScriptFile`***

(省略可能)。 実行するスクリプトを指定します。

**`/?`**

(省略可能)。 Netsh プロンプトからのヘルプを表示します。

>[!NOTE]
>指定した場合**`-r`** 、別のコマンドに続けて**netsh**リモート コンピューターでコマンドを実行し、Cmd.exe コマンド プロンプトに戻ります。 指定した場合**`-r`** せず、別のコマンド**netsh**リモート モードで開きます。 プロセスの使用と似ています**セット マシン**Netsh コマンド プロンプトでします。 使用すると **`-r`** の現在のインスタンス用のターゲット コンピューターを設定する**netsh**のみです。 終了して再入力した後**netsh**、ローカル コンピューターと、対象コンピューターをリセットします。 実行することができます**netsh**コンピューターを指定することで、リモート コンピューターでコマンドをという名前を WINS に格納されている、UNC 名、DNS サーバー、または IP アドレスが解決するインターネット名。

**Netsh コマンドのパラメーターの文字列値を入力します。**

Netsh コマンドのリファレンスでは、対象の文字列値が必要なパラメーターを含むコマンドがあります。

文字列値が 1 つ以上の単語で構成される文字列値などの文字の間にスペースが含まれている場合は必須、文字列値を引用符で囲みます。 たとえば、という名前のパラメーター**インターフェイス**の文字列値を持つ**ワイヤレス ネットワーク接続**文字列値を囲む引用符を使用します。

**`interface="Wireless Network Connection"`**

