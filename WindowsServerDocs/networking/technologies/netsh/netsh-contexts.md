---
title: Netsh コマンドの構文、コンテキスト、形式
description: このトピックでは、netsh コンテキストとサブコンテキストを入力する方法、netsh 構文とコマンドの書式について、Windows Server 2016 または Windows 10 を実行しているローカル コンピューターとリモート コンピューターで netsh コマンドを実行する方法について説明します。
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 8cb9b59f-0255-4261-b49a-562c5ea50ee0
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 815e59ca00d6450b8ef09a034434c4209c928e78
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405581"
---
# <a name="netsh-command-syntax-contexts-and-formatting"></a>Netsh コマンドの構文、コンテキスト、形式

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、netsh コンテキストとサブコンテキストを入力する方法、netsh 構文とコマンドの書式について、ローカル コンピューターとリモート コンピューターで netsh コマンドを実行する方法について説明します。

netsh は、現在実行中のコンピューターのネットワーク構成を表示したり変更したりするためのコマンド ライン スクリプト ユーティリティです。 netsh コマンドは、netsh プロンプトでコマンドを入力することで実行し、バッチ ファイルまたはスクリプトで使用できます。 リモート コンピューターとローカル コンピューターは、netsh コマンドを使用して構成できます。

また、指定したコンピューターに対して一連のコマンドをバッチ モードで実行できるスクリプト機能も備えています。 netsh では、構成スクリプトをテキスト ファイルに保存して、アーカイブとして保管したり、他のコンピューターの構成に利用したりできます。

## <a name="netsh-contexts"></a>netsh コンテキスト

netsh は、ダイナミック\-リンク ライブラリ \(DLL\) ファイルを使用して、他のオペレーティング システムのコンポーネントと対話します。 

各 netsh ヘルパー DLL には、ネットワーク サーバーの役割または機能に固有のコマンドのグループである "*コンテキスト*" と呼ばれるさまざまな機能のセットが用意されています。 これらのコンテキストにより、1 つ以上のサービス、ユーティリティ、またはプロトコルの構成と監視のサポートが提供されるため、netsh の機能が拡張されます。 たとえば、Dhcpmon.dll では netsh に DHCP サーバーを構成して管理するために必要なコンテキストとコマンドのセットが提供されます。

### <a name="obtain-a-list-of-contexts"></a>コンテキストの一覧を取得する

netsh コンテキストの一覧を取得するには、Windows Server 2016 または Windows 10 を実行しているコンピューターでコマンド プロンプトまたは Windows PowerShell を開きます。 コマンド「**netsh**」を入力し、Enter キーを押します。 「 **/?** 」と入力し、Enter キーを押します。

Windows Server 2016 Datacenter を実行しているコンピューターでのこれらのコマンドの出力例を次に示します。

>    ```
>   PS C:\Windows\system32> netsh
>   netsh>/?
>    
>    The following commands are available:
>    
>    Commands in this context:
>    ..            - Goes up one context level.
>    ?             - Displays a list of commands.
>    abort         - Discards changes made while in offline mode.
>    add           - Adds a configuration entry to a list of entries.
>    advfirewall   - Changes to the `netsh advfirewall' context.
>    alias         - Adds an alias.
>    branchcache   - Changes to the `netsh branchcache' context.
>    bridge        - Changes to the `netsh bridge' context.
>    bye           - Exits the program.
>    commit        - Commits changes made while in offline mode.
>    delete        - Deletes a configuration entry from a list of entries.
>    dhcpclient    - Changes to the `netsh dhcpclient' context.
>    dnsclient     - Changes to the `netsh dnsclient' context.
>    dump          - Displays a configuration script.
>    exec          - Runs a script file.
>    exit          - Exits the program.
>    firewall      - Changes to the `netsh firewall' context.
>    help          - Displays a list of commands.
>    http          - Changes to the `netsh http' context.
>    interface     - Changes to the `netsh interface' context.
>    ipsec         - Changes to the `netsh ipsec' context.
>    ipsecdosprotection - Changes to the `netsh ipsecdosprotection' context.
>    lan           - Changes to the `netsh lan' context.
>    namespace     - Changes to the `netsh namespace' context.
>    netio         - Changes to the `netsh netio' context.
>    offline       - Sets the current mode to offline.
>    online        - Sets the current mode to online.
>    popd          - Pops a context from the stack.
>    pushd         - Pushes current context on stack.
>    quit          - Exits the program.
>    ras           - Changes to the `netsh ras' context.
>    rpc           - Changes to the `netsh rpc' context.
>    set           - Updates configuration settings.
>    show          - Displays information.
>    trace         - Changes to the `netsh trace' context.
>    unalias       - Deletes an alias.
>    wfp           - Changes to the `netsh wfp' context.
>    winhttp       - Changes to the `netsh winhttp' context.
>    winsock       - Changes to the `netsh winsock' context.
>    
>    The following sub-contexts are available:
>     advfirewall branchcache bridge dhcpclient dnsclient firewall http interface ipsec ipsecdosprotection lan namespace netio ras rpc trace wfp winhttp winsock
>    
>    To view help for a command, type the command, followed by a space, and then type ?.
>    ```

### <a name="subcontexts"></a>サブコンテキスト

netsh コンテキストには、コマンドと、"*サブコンテキスト*" と呼ばれる追加のコンテキストの両方を含めることができます。 たとえば、ルーティング コンテキスト内では、IP および IPv6 サブコンテキストに変更できます。

コンテキスト内で使用できるコマンドとサブコンテキストの一覧を表示するには、netsh プロンプトでコンテキスト名を入力し、「 **/?** 」と入力するか、 「**help**」と入力します。 たとえば、ルーティング コンテキストで使用できるサブコンテキストとコマンドの一覧を表示するには、netsh プロンプト (\(つまり、**netsh&gt;** \)) で、次のいずれかを入力します。

**routing /?**

**routing help**

現在のコンテキストから変更せずに別のコンテキストでタスクを実行するには、netsh プロンプトで使用するコマンドのコンテキスト パスを入力します。 たとえば、IGMP コンテキストに最初に変更を加えることなく、IGMP コンテキストに "Local Area Connection" という名前のインターフェイスを追加するには、netsh プロンプトで次のように入力します。

**routing ip igmp add interface "Local Area Connection" startupqueryinterval=21**

## <a name="running-netsh-commands"></a>netsh コマンドの実行

netsh コマンドを実行するには、「**netsh**」と入力し、Enter キーを押して、コマンド プロンプトから netsh を起動する必要があります。 次に、使用するコマンドが含まれているコンテキストに変更できます。 使用できるコンテキストは、インストールしたネットワーク コンポーネントによって異なります。 たとえば、netsh プロンプトで「**dhcp**」と入力し、Enter キーを押すと、netsh が DHCP サーバーのコンテキストに変わります。 ただし、DHCP がインストールされていない場合は、次のメッセージが表示されます。

**次のコマンドは見つかりませんでした: dhcp**

## <a name="formatting-legend"></a>表記規則

netsh プロンプトまたはバッチ ファイルまたはスクリプトでコマンドを実行するときに、次の表記規則に従うことで、正しい netsh コマンド構文を解釈して使用できます。

- "*イタリック*" のテキストは、コマンドの入力時に指定する必要がある情報です。 たとえば、コマンドに -*UserName* という名前のパラメーターがある場合、実際のユーザー名を入力する必要があります。
- **太字**のテキストは、コマンドの入力時に表示されるとおりに入力する必要がある情報です。
- テキストの後に省略記号 \(...\) が続くパラメーターは、コマンド ラインで複数回繰り返すことができるパラメーターです。
- 角かっこ [&nbsp;] に囲まれたテキストはオプションの項目です。
- 中かっこ {&nbsp;} に囲まれたテキストは、パイプで区切られた選択肢であり、そのうちの 1 つだけ選択する必要があります (例: `{enable|disable}`)。
- 等幅フォントで書式設定されたテキストは、コードまたはプログラムの出力です。

## <a name="running-netsh-commands-from-the-command-prompt-or-windows-powershell"></a>コマンド プロンプトまたは Windows PowerShell からの netsh コマンドの実行

ネットワーク シェルを起動し、コマンド プロンプトまたは Windows PowerShell で netsh を入力するには、次のコマンドを使用します。

### <a name="netsh"></a>netsh

netsh は、実行中のコンピューターのネットワーク構成をローカルまたはリモートで表示または変更することができるようにするコマンド ライン スクリプト ユーティリティです。 パラメーターを指定しないで使用すると、**netsh** により netsh.exe コマンド プロンプト (\(つまり、**netsh&gt;** \)) が開きます。

#### <a name="syntax"></a>構文

**netsh**\[ **-a**&nbsp;*AliasFile*\] \[ **-c**&nbsp;*Context* \] \[ **-r**&nbsp;*RemoteComputer*\] \[ **-u** \[ *DomainName\\* \] *UserName* \] \[ **-p**&nbsp;*Password* | \*\] \[{*NetshCommand* |  **-f**&nbsp;*ScriptFile*}\]

#### <a name="parameters"></a>パラメーター

**`-a`**

任意。 *AliasFile* を実行した後に **netsh** プロンプトに戻ることを指定します。

**`AliasFile`**

任意。 **netsh** コマンドを 1 つ以上含むテキスト ファイルの名前を指定します。

**`-c`**

任意。 指定された **netsh** コンテキストが netsh によって入力されることを指定します。

**`Context`**

任意。 入力する **netsh** コンテキストを指定します。 

**`-r`**

任意。 コマンドをリモート コンピューターで実行することを指定します。

> [!IMPORTANT]
> **netsh – r** パラメーターを使用して別のコンピューターで一部の netsh コマンドをリモートで使用する場合は、リモート コンピューターでリモート レジストリ サービスが実行されている必要があります。 実行されていない場合は、"ネットワーク パスが見つかりません" というエラー メッセージが表示されます。

***`RemoteComputer`***

任意。 構成するリモート コンピューターを指定します。

**`-u`**

任意。 ユーザー アカウントで netsh コマンドを実行することを指定します。

***`DomainName\\`***

任意。 ユーザー アカウントが存在するドメインを指定します。 *DomainName\\* が指定されていない場合の既定値は、ローカル ドメインです。

***`UserName`***

任意。 ユーザー アカウント名を指定します。

**`-p`**

任意。 ユーザー アカウントのパスワードを指定することを指定します。

***`Password`***

任意。 **-u** *UserName* で指定したユーザー アカウントのパスワードを指定します。

***`NetshCommand`***

任意。 実行する **netsh** コマンドを指定します。

**`-f`**

任意。 *ScriptFile* で指定したスクリプトを実行した後に **netsh** を終了します。

***`ScriptFile`***

任意。 実行するスクリプトを指定します。

**`/?`**

任意。 netsh プロンプトでヘルプを表示します。

> [!NOTE]
> **`-r`** を指定して別のコマンドを続けると、**netsh** によりコマンドがリモート コンピューターで実行され、その後 Cmd.exe コマンド プロンプトに戻ります。 別のコマンドを使用せずに **`-r`** を指定すると、**netsh** がリモート モードで開きます。 このプロセスは **set machine** を netsh コマンド プロンプトで使用するのと似ています。 **`-r`** を使用するときは、**netsh** の現在のインスタンスに対してのみターゲット コンピューターを設定します。 **netsh** を終了して再入力すると、ターゲット コンピューターがローカル コンピューターとして再設定されます。 WINS に格納されているコンピューター名、UNC 名、DNS サーバーによって解決されるインターネット名、または IP アドレスを指定することにより、リモート コンピューター上で **netsh** コマンドを実行できます。

**netsh コマンドのパラメーター文字列値の入力**

netsh コマンド リファレンス全体にわたって、文字列値が必要とされるパラメーターが含まれるコマンドがあります。

複数の単語で構成される文字列値など、文字列値の文字間にスペースが含まれている場合は、文字列値を引用符で囲む必要があります。 たとえば、文字列値が **Wireless Network Connection** の **interface** という名前のパラメーターの場合は、次のように文字列値を引用符で囲みます。

**`interface="Wireless Network Connection"`**

