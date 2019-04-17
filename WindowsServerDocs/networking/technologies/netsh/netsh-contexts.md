---
title: Netsh コマンドの構文、コンテキスト、および書式設定
description: このトピックを使用すると、netsh コンテキストとサブコンテキストを入力し、netsh 構文と、コマンドの書式設定について理解するのに方法と Windows Server 2016 または Windows 10 を実行しているローカルおよびリモート コンピューター上の netsh コマンドを実行するのに方法について説明します。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 8cb9b59f-0255-4261-b49a-562c5ea50ee0
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c7c16674b831431ff5bb1d0172cc2b2a939008f6
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="netsh-command-syntax-contexts-and-formatting"></a>Netsh コマンドの構文、コンテキスト、および書式設定

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用すると、ローカルおよびリモート コンピューター上の netsh コマンドを実行するのに方法と netsh コンテキストとサブコンテキストを入力し、netsh 構文と、コマンドの書式設定について理解するのに方法について説明します。

Netsh は、コマンド ライン スクリプト ユーティリティを表示または現在実行しているコンピューターのネットワーク構成を変更することができます。 Netsh コマンドは netsh プロンプトでコマンドを入力して実行され、バッチ ファイルまたはスクリプトで、使用することができます。 Netsh コマンドを使用してリモート コンピューターおよびローカル コンピューターを構成することができます。

Netsh では、コマンドのグループを指定したコンピューターに対してバッチ モードで実行できるスクリプト機能も提供します。 Netsh、保管したり、他のコンピューターを構成するのには、テキスト ファイルに構成スクリプトを保存することができます。

## <a name="netsh-contexts"></a>Netsh コンテキスト

Netsh では、dynamic\ リンク ライブラリ \(DLL\) ファイルを使用して他のオペレーティング システムのコンポーネントとやり取りします。 

各 netsh ヘルパー DLL が豊富なと呼ばれる機能を提供、*コンテキスト*、ネットワーク サーバーの役割または機能に固有のコマンドのグループです。 これらのコンテキストでは、構成を提供して、1 つ以上のサービス、ユーティリティ、またはプロトコルのサポートを監視しての netsh 機能を拡張します。 たとえば、Dhcpmon.dll コンテキストを構成して、DHCP サーバーの管理に必要なコマンドのセットと netsh を提供します。

### <a name="obtain-a-list-of-contexts"></a>コンテキストの一覧を取得します。

Netsh コンテキストの一覧を取得するには、Windows Server 2016 または Windows 10 を実行しているコンピューターでコマンド プロンプトまたは Windows PowerShell を開きます。 コマンドを入力**netsh**し、Enter キーを押します。 種類**/ですか?**、し、Enter キーを押します。

Windows Server 2016 Datacenter を実行するコンピューターでこれらのコマンドの出力の例を次に示します。

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

Netsh コンテキストは、コマンドと呼ばれる追加のコンテキストの両方を含めることができます*サブコンテキスト*します。 たとえば、ルーティングのコンテキスト内で ip アドレスと IPv6 サブコンテキストに変更できます。

コマンドと、netsh プロンプトのコンテキスト内で使用できるサブコンテキストの一覧を表示するコンテキストの名前を入力し、いずれかのように入力し、**/ですか?** または**ヘルプ**します。 例では、コンテキストでは、ルーティング、netsh プロンプト サブコンテキストと使用できるコマンドの一覧を表示する \ (つまり、**netsh&gt;**\)、次のいずれかのように入力します。

**ルーティング/ですか?**

**ルーティングのヘルプ**

タスクを実行する別のコンテキストで現在のコンテキストから変更することがなく、netsh プロンプトを使用するコマンドのコンテキストのパスを入力します。 たとえば、IGMP コンテキストで「ローカル エリア接続」という名前のプロンプトで、netsh、IGMP コンテキストを最初に変更することがなくインターフェイスを追加する次のように入力します。

**「ローカル エリア接続」startupqueryinterval のインターフェイスを追加する ip igmp ルーティング 21 を =**

## <a name="running-netsh-commands"></a>Netsh コマンドを実行します。

Netsh コマンドを実行する必要がありますを開始する netsh コマンド プロンプトから」と入力して**netsh**し、Enter キーを押します。 次を使用するコマンドを含むコンテキストに変更することができます。 使用可能なコンテキストでは、インストールされているネットワーク コンポーネントに依存します。 たとえば、次のように入力した**dhcp** netsh プロンプトと Enter キーを押しますでは、netsh は DHCP サーバーのコンテキストに変更します。 インストールされている DHCP を持っていない場合は、次のメッセージが表示されます。

**次のコマンドが見つかりませんでした。dhcp します。**

## <a name="formatting-legend"></a>表記規則

解釈および netsh プロンプトまたはバッチ ファイルまたはスクリプトでコマンドを実行するときに、正しい netsh コマンドの構文を使用する書式設定の次の凡例を使用することができます。

- 内のテキスト*斜体*情報が、コマンドを入力するときに指定する必要があります。 たとえば、次のコマンドは、という名前のパラメーター*UserName*、実際のユーザー名を入力する必要があります。
- 内のテキスト**太字**情報が、コマンドを入力するときに表示されるとおりに入力する必要があります。
- 省略記号 \(...\) 続くテキストは、コマンド ラインで繰り返すことができます。
- 角かっこがテキスト [&nbsp;] は省略可能な項目。
- テキストは中かっこ間にある {&nbsp;} パイプで区切られた選択肢を提供する必要がありますを選択する 1 つだけなどの選択肢`{enable|disable}`します。
- 等幅フォントでフォーマットされたテキストは、コードまたはプログラムの出力です。

## <a name="running-netsh-commands-from-the-command-prompt-or-windows-powershell"></a>コマンド プロンプトまたは Windows PowerShell からの Netsh コマンドを実行しています。

ネットワーク シェルを起動し、netsh または Windows PowerShell でコマンド プロンプトでを入力して、次のコマンドを使用することができます。

### <a name="netsh"></a>netsh

Netsh は、ローカルまたはリモートで表示または実行中のコンピューターのネットワーク構成を変更することができるようにするコマンド ライン スクリプト ユーティリティです。 パラメーターを指定せずに使用される**netsh** Netsh.exe コマンド プロンプトを開きます \ (つまり、**netsh&gt;**\)。

#### <a name="syntax"></a>構文

**netsh**\[ **-a**&nbsp;*AliasFile*\] \[ **-c**&nbsp;*Context* \] \[**-r**&nbsp;*RemoteComputer*\] \[ **-u** \[ *DomainName\\* \] *UserName* \] \[ **-p**&nbsp;*Password* | \*\] \[{*NetshCommand* | **-f**&nbsp;*ScriptFile*}\]

#### <a name="parameters"></a>パラメーター

**`-a`**

省略可能です。 戻ることを指定します、**netsh**実行後プロンプト*-a エイリアス ファイル名*します。

**`AliasFile`**

省略可能です。 1 つまたは複数を含むテキスト ファイルの名前を指定**netsh**コマンド。

**`-c`**

省略可能です。 その netsh は、指定された入力を指定します。**netsh**コンテキスト。

**`Context`**

省略可能です。 指定します、**netsh**を入力するコンテキスト。 

**`-r`**

省略可能です。 コマンドは、リモート コンピューターで実行することを指定します。

>[!IMPORTANT]
>使用するといくつかの netsh コマンド リモートで別のコンピューターに、**netsh – r**パラメーター、リモート レジストリ サービスは、リモート コンピューターで実行必要があります。 実行されていない場合は、"ネットワーク パスが見つかりません"というエラー メッセージが表示されます。

***`RemoteComputer`***

省略可能です。 リモート コンピューターを構成することを指定します。

**`-u`**

省略可能です。 ユーザー アカウントでの netsh コマンドを実行することを指定します。

***`DomainName\\`***

省略可能です。 ユーザー アカウントのドメインを指定します。 場合、既定値は、ローカル ドメイン*DomainName\\*が指定されていません。

***`UserName`***

省略可能です。 ユーザー アカウント名を指定します。

**`-p`**

省略可能です。 ユーザー アカウントのパスワードを指定することを指定します。

***`Password`***

省略可能です。 使用して指定したユーザー アカウントのパスワードを指定**-u***UserName*します。

***`NetshCommand`***

省略可能です。 指定します、**netsh**に実行するコマンドです。

**`-f`**

省略可能です。 終了**netsh**で指定したスクリプトの実行後*ScriptFile*します。

***`ScriptFile`***

省略可能です。 実行するスクリプトを指定します。

**`/?`**

省略可能です。 Netsh プロンプトでヘルプを表示します。

>[!NOTE]
>指定した場合**`-r`**、別のコマンドを続けて**netsh**、リモート コンピューターでコマンドを実行し、Cmd.exe コマンド プロンプトに戻ります。 指定した場合**`-r`**せず、別のコマンド**netsh**リモート モードで開きます。 プロセスを使用してに似ています**セット マシン**Netsh コマンド プロンプトでします。 使用すると**`-r`**、ターゲット コンピューターの現在のインスタンスを設定する**netsh**のみです。 終了して再入力した後**netsh**、ローカル コンピューターと、対象コンピューターをリセットします。 行うことができます**netsh** WINS に保存されている、UNC 名、インターネット名、DNS サーバーまたは IP アドレスが解決するコンピューターを指定してリモート コンピューターでのコマンドの名前します。

**Netsh コマンドのパラメーターの文字列値を入力します。**

Netsh コマンドのリファレンス全体でコマンドを含むパラメーターの文字列値が必要があります。

場合は、文字列値に 1 つ以上の word で構成される文字列値などの文字の間にスペースが含まれていますが必要な文字列値を引用符で囲みます。 たとえば、という名前のパラメーター**インターフェイス**文字列値を**ワイヤレス ネットワーク接続**、文字列値を囲む引用符を使用します。

**`interface="Wireless Network Connection"`**

