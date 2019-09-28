---
title: Netsh コマンドの構文、コンテキスト、形式
description: このトピックでは、netsh コンテキストとサブコンテキストを入力する方法、netsh 構文とコマンドの書式を理解する方法、および Windows Server 2016 または Windows 10 を実行しているローカルコンピューターおよびリモートコンピューターで netsh コマンドを実行する方法について説明します。
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 8cb9b59f-0255-4261-b49a-562c5ea50ee0
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 815e59ca00d6450b8ef09a034434c4209c928e78
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405581"
---
# <a name="netsh-command-syntax-contexts-and-formatting"></a>Netsh コマンドの構文、コンテキスト、形式

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、netsh コンテキストとサブコンテキストを入力する方法、netsh 構文とコマンドの書式を理解する方法、およびローカルコンピューターとリモートコンピューターで netsh コマンドを実行する方法について説明します。

Netsh は、現在実行中のコンピューターのネットワーク構成を表示または変更するためのコマンドラインスクリプトユーティリティです。 Netsh コマンドは、netsh プロンプトでコマンドを入力することで実行でき、バッチファイルまたはスクリプトで使用できます。 リモートコンピューターとローカルコンピューターは、netsh コマンドを使用して構成できます。

また、指定したコンピューターに対して一連のコマンドをバッチ モードで実行できるスクリプト機能も備えています。 netsh では、構成スクリプトをテキスト ファイルに保存して、アーカイブとして保管したり、他のコンピューターの構成に利用したりできます。

## <a name="netsh-contexts"></a>Netsh コンテキスト

Netsh は、動的な @ no__t-0link ライブラリ \(DLL @ no__t ファイルを使用して、他のオペレーティングシステムコンポーネントと対話します。 

各 netsh helper DLL には、*コンテキスト*と呼ばれる広範な機能セットが用意されています。これは、ネットワークサーバーの役割または機能に固有のコマンドのグループです。 これらのコンテキストにより、1つ以上のサービス、ユーティリティ、またはプロトコルの構成と監視のサポートが提供されるため、netsh の機能が拡張されます。 たとえば、DHCP サーバーを構成および管理するために必要なコンテキストとコマンドのセットを使用して netsh を提供します。

### <a name="obtain-a-list-of-contexts"></a>コンテキストの一覧を取得する

Netsh コンテキストの一覧を取得するには、Windows Server 2016 または Windows 10 を実行しているコンピューターでコマンドプロンプトまたは Windows PowerShell を開きます。 コマンド**netsh**を入力し、enter キーを押します。 「 **/?** 」と入力し、enter キーを押します。

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

### <a name="subcontexts"></a>テキスト

Netsh コンテキストには、コマンドと、*サブコン*テキストと呼ばれる追加のコンテキストの両方を含めることができます。 たとえば、ルーティングコンテキスト内では、IP および IPv6 サブコンテキストに変更できます。

コンテキスト内で使用できるコマンドとサブコンテキストの一覧を表示するには、netsh プロンプトでコンテキスト名を入力し、「/?」と入力し**ます。** または**ヘルプ**。 たとえば、ルーティングコンテキストで使用できるサブコンテキストとコマンドの一覧を表示するには、netsh プロンプトで @no__t、netsh **@ no__t-2**\) と入力し、次のいずれかを入力します。

**ルーティング/確認**

**ルーティングのヘルプ**

現在のコンテキストから変更せずに別のコンテキストでタスクを実行するには、netsh プロンプトで使用するコマンドのコンテキストパスを入力します。 たとえば、igmp コンテキストに最初に変更を加えることなく、IGMP コンテキストに "ローカルエリア接続" という名前のインターフェイスを追加するには、netsh プロンプトで次のように入力します。

**ルーティング ip igmp add interface "ローカルエリア接続" startupqueryinterval = 21**

## <a name="running-netsh-commands"></a>Netsh コマンドの実行

Netsh コマンドを実行するには、コマンドプロンプトで「 **netsh** 」と入力し、enter キーを押して netsh を起動する必要があります。 次に、使用するコマンドが含まれているコンテキストに変更できます。 使用できるコンテキストは、インストールされているネットワークコンポーネントによって異なります。 たとえば、netsh プロンプトで「 **dhcp** 」と入力し、enter キーを押すと、netsh によって dhcp サーバーのコンテキストが変更されます。 ただし、DHCP がインストールされていない場合は、次のメッセージが表示されます。

**次のコマンドが見つかりませんでした: dhcp。**

## <a name="formatting-legend"></a>凡例の書式設定

Netsh プロンプトまたはバッチファイルまたはスクリプトでコマンドを実行するときに、次の書式設定の凡例を使用して、正しい netsh コマンド構文を解釈して使用することができます。

- *斜体*のテキストは、コマンドの入力時に指定する必要がある情報です。 たとえば、コマンドに-*UserName*という名前のパラメーターがある場合は、実際のユーザー名を入力する必要があります。
- **太字**のテキストは、コマンドの入力時に表示されるとおりに正確に入力する必要がある情報です。
- テキストの後に省略記号 \(... \) は、コマンドラインで複数回繰り返すことができるパラメーターです。
- 角かっこ [&nbsp;] のテキストはオプションの項目です。
- 中かっこ {&nbsp;} の間にあるテキストは、パイプで区切られた選択肢であり、1つだけ選択する必要があります (`{enable|disable}` など)。
- 媒体使用フォントで書式設定されたテキストは、コードまたはプログラムの出力です。

## <a name="running-netsh-commands-from-the-command-prompt-or-windows-powershell"></a>コマンドプロンプトまたは Windows PowerShell からの Netsh コマンドの実行

ネットワークシェルを起動し、コマンドプロンプトまたは Windows PowerShell で netsh を入力するには、次のコマンドを使用します。

### <a name="netsh"></a>netsh

Netsh は、現在実行中のコンピューターのネットワーク構成をローカルまたはリモートで表示または変更できるコマンドラインスクリプトユーティリティです。 Netsh では、パラメーターを指定せずに netsh .exe コマンドプロンプト**を開く @no__t** -1、 **netsh @ no__t-3**\) です。

#### <a name="syntax"></a>構文

**netsh**\[ **-a**&nbsp;*エイリアスファイル*\] \[ **-c**&nbsp;*Context* 0 1 **-r**3*RemoteComputer*5 6 **-u** 8 *DomainName @ no__t-20* 1*ユーザー名*3 4 **-p**6*パスワード*8 @ no__t-29 @ No__t-30 1 {*netshcommand*3 **-f**5*ScriptFile*}7

#### <a name="parameters"></a>パラメーター

**`-a`**

任意。 *エイリアスファイル*を実行した後に**netsh**プロンプトに戻ることを指定します。

**`AliasFile`**

任意。 1つ以上の**netsh**コマンドを含むテキストファイルの名前を指定します。

**`-c`**

任意。 Netsh が指定した**netsh**コンテキストを入力するように指定します。

**`Context`**

任意。 入力する**netsh**コンテキストを指定します。 

**`-r`**

任意。 コマンドをリモートコンピューターで実行することを指定します。

> [!IMPORTANT]
> Netsh **– r**パラメーターを使用して別のコンピューターで netsh コマンドをリモートで使用する場合、リモートレジストリサービスがリモートコンピューター上で実行されている必要があります。 実行されていない場合は、"ネットワークパスが見つかりません" というエラーメッセージが表示されます。

***`RemoteComputer`***

任意。 構成するリモートコンピューターを指定します。

**`-u`**

任意。 ユーザーアカウントで netsh コマンドを実行することを指定します。

***`DomainName\\`***

任意。 ユーザーアカウントが存在するドメインを指定します。 *DomainName @ no__t*が指定されていない場合、既定値はローカルドメインです。

***`UserName`***

任意。 ユーザーアカウント名を指定します。

**`-p`**

任意。 ユーザーアカウントのパスワードを指定することを指定します。

***`Password`***

任意。 **-U** *UserName*で指定したユーザーアカウントのパスワードを指定します。

***`NetshCommand`***

任意。 実行する**netsh**コマンドを指定します。

**`-f`**

任意。 *ScriptFile*で指定したスクリプトを実行した後、 **netsh**を終了します。

***`ScriptFile`***

任意。 実行するスクリプトを指定します。

**`/?`**

任意。 Netsh プロンプトでヘルプを表示します。

> [!NOTE]
> **@No__t-1**の後に別のコマンドを指定した場合は、 **netsh**によってリモートコンピューターでコマンドが実行され、cmd.exe コマンドプロンプトに戻ります。 別のコマンドを使用せずに **`-r`** を指定した場合は、 **netsh**がリモートモードで開きます。 このプロセスは、Netsh コマンドプロンプトでの**set machine**の使用に似ています。 **@No__t-1**を使用する場合は、 **netsh**の現在のインスタンスに対してのみターゲットコンピューターを設定します。 を終了して再**入力すると、ターゲット**コンピュータはローカルコンピュータとしてリセットされます。 WINS に格納されているコンピューター名、UNC 名、DNS サーバーによって解決されるインターネット名、または IP アドレスを指定することにより、リモートコンピューターで**netsh**コマンドを実行できます。

**Netsh コマンドのパラメーター文字列値の入力**

Netsh コマンドリファレンス全体で、文字列値が必要なパラメーターを含むコマンドがあります。

文字列値に複数の単語で構成される文字列値など、文字間のスペースが含まれている場合は、文字列値を引用符で囲む必要があります。 たとえば、文字列値が**ワイヤレスネットワーク接続**の**インターフェイス**という名前のパラメーターの場合は、文字列値を引用符で囲みます。

**`interface="Wireless Network Connection"`**

