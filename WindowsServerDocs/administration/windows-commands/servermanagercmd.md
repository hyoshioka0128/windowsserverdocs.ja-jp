---
title: Servermanagercmd
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 507c4b87-8e13-4872-8b34-0c7508eecbc1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: ba0b85814d942323b12e1874b852fcf28b8ac068
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883243"
---
# <a name="servermanagercmd"></a>Servermanagercmd

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

> [!IMPORTANT]
> このコマンドは、Windows Server 2008 を実行しているサーバーまたは Windows Server 2008 R2 でのみ使用できます。 **Servermanagercmd.exe**は非推奨し、Windows Server 2012 では使用できません。 インストールまたは Windows Server 2012 の役割、役割サービス、および機能を削除する方法については、次を参照してください。 [インストールまたは役割、役割サービス、および機能をアンインストール](https://go.microsoft.com/fwlink/?LinkID=239563) Microsoft TechNet のです。

インストールし、役割、役割サービス、および機能を削除します。 すべての役割、役割サービス、および使用可能な機能の一覧が表示され、このコンピューターにインストールされているかを示します。 役割、役割サービス、およびこのツールを使用して指定できる機能の詳細については、次を参照してください。、[サーバー マネージャーのヘルプ](https://go.microsoft.com/fwlink/?LinkID=137387)します。 このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文
```
servermanagercmd -query [[[<Drive>:]<path>]<query.xml>] [-logpath   [[<Drive>:]<path>]<log.txt>]
servermanagercmd -inputpath  [[<Drive>:]<path>]<answer.xml> [-resultpath <result.xml> [-restart] | -whatif] [-logpath [[<Drive>:]<path>]<log.txt>]
servermanagercmd -install <Id> [-allSubFeatures] [-resultpath   [[<Drive>:]<path>]<result.xml> [-restart] | -whatif] [-logpath   [[<Drive>:]<path>]<log.txt>]
servermanagercmd -remove <Id> [-resultpath    <result.xml> [-restart] | -whatif] [-logpath  [[<Drive>:]<path>]<log.txt>]
servermanagercmd [-help | -?]
servermanagercmd -version
```

## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|-query [[[\<Drive>:]\<path>]\<*query.xml*>]|サーバー上のすべての役割、役割サービス、およびインストールされ、インストール可能な機能の一覧を表示します。 このパラメーターの短い形式を使用することもできます。 **-q**します。 クエリの結果を XML ファイルに保存する場合は、置換する XML ファイルを指定 *query.xml*します。|
|-inputpath < [\<ドライブ >:]\<パス >]*answer.xml*>|インストールまたは削除、役割、役割サービス、およびによって表される XML 応答ファイルで指定されている機能 *answer.xml*します。 このパラメーターの短い形式を使用することもできます。 **-p します。**|
|-インストール\< *Id*>|役割、役割サービス、またはで指定された機能をインストール *Id*します。識別子が区別されます。 複数の役割、役割サービス、および機能は、スペースで区切る必要があります。 次のオプション パラメーターを使用、 **-インストール** パラメーター。<br /><br />-   **-設定** \< *SettingName*>=\<*SettingValue*> インストールに必須の設定を指定します。<br />-   **-allsubfeatures**すべての下位のサービスと親の役割、役割サービス、またはでという名前の機能と機能のインストールを指定します、 *Id*値。 **注:**    役割コンテナーによっては、すべての役割サービスのインストールを許可するコマンドライン識別子はありません。 これは、サーバー マネージャーのコマンドの同じインスタンスでは、役割サービスをインストールできない場合に大文字と小文字です。 たとえば、同じサーバー マネージャーのコマンド インスタンスを使用して active directory フェデレーション サービスとフェデレーション サービス プロキシ役割サービスのフェデレーション サービス役割サービスをインストールすることはできません。<br />-   **-resultpath** \< *result.xml > によって表される XML ファイルにインストールの結果を保存します。 *result.xml*します。このパラメーターの短い形式を使用することもできます。 **-r**します。**注:**    実行することはできません**servermanagercmd**と共に、 **-resultpath**パラメーターと **-whatif**パラメーターを指定します<br />。-    **-再起動**インストールの (役割または機能のインストールで再起動が必要です) の場合は、完了時に自動的にコンピューターを再起動します<br />。-    **-whatif**に指定された操作を表示、 **-インストール**パラメーター。短い形式を使用することもできます、 **-whatif**パラメーター、 **-w**します。実行することはできません**servermanagercmd**と共に、 **-resultpath**パラメーターと **-whatif**パラメーターを指定します<br />。-    **-logpath** \<[\<ドライブ >:]\<パス >]* log.txt* > ログ ファイルの既定以外の場所と名前を指定します **%windir%\temp\servermanager.log**します。|
|-削除\< *Id*>|役割、役割サービス、またはで指定された機能を削除 *Id*します。識別子が区別されます。 複数の役割、役割サービス、および機能は、スペースで区切る必要があります。 次のオプション パラメーターを使用、 **-削除** パラメーター。<br /><br />-   **-resultpath** \<[\<ドライブ >:]\<パス >]*result.xml*> によって表される XML ファイルを削除の結果を保存します。 *result.xml*します。 このパラメーターの短い形式を使用することもできます。 **-r**します。 **注:**    実行することはできません**servermanagercmd**と共に、 **-resultpath**パラメーターと **-whatif**パラメーターを指定します。<br />-   **-再起動**削除の残りの役割または機能によって、再起動が必要です) であれば、完了時に自動的にコンピューターを再起動します。<br />-   **-whatif**に指定された操作を表示、 **-削除**パラメーター。 短い形式を使用することもできます、 **-whatif**パラメーター、 **-w**します。 実行することはできません**servermanagercmd**と共に、 **-resultpath**パラメーターと **-whatif**パラメーターを指定します。<br />-   **-logpath**\<[\<ドライブ >:]\<パス >]*log.txt*> ログ ファイルの既定以外の場所と名前を指定します **%windir%\temp\servermanager.log**します。|
|-ヘルプ|コマンド プロンプト ウィンドウでヘルプを表示します。 短い形式を使用することもできます。 **-?** します。|
|バージョン|サーバー マネージャーのバージョン番号を表示します。 短い形式を使用することもできます。 **-v**します。|

## <a name="remarks"></a>注釈
**Servermanagercmd** は推奨されず、および Windows の将来のリリースでサポートされるとは限りません。 Windows Server 2008 R2 を実行しているコンピューターでサーバー マネージャーを実行している場合、サーバー マネージャーの使用できる Windows PowerShell コマンドレットを使用することをお勧めします。 詳細については、次を参照してください。 [サーバー マネージャー コマンドレット](https://go.microsoft.com/fwlink/?LinkID=137653)します。
Servermanagercmd は、サーバーのローカル ドライブ上の任意のディレクトリから実行できます。 インストールまたはソフトウェアを削除するサーバーの Administrators グループのメンバーである必要があります。

> [!IMPORTANT]
> Windows Server 2008 R2 でのユーザー アカウント制御によって課せられるセキュリティの制限により実行する必要があります**Servermanagercmd**管理者特権で開いたコマンド プロンプト ウィンドウで、します。 これを行うには、実行可能ファイル、コマンド プロンプトを右クリックし、または**コマンド プロンプト**上のオブジェクト、**開始** メニューをクリック**管理者として実行**します。

## <a name="BKMK_examples"></a>例
次の例は、使用する方法を示しています。 **servermanagercmd** を一連のすべての役割、役割サービス、および機能の使用可能な、どの役割、役割サービス、および機能がコンピューターにインストールされているを表示します。
```
servermanagercmd -query
```
次の例は、使用する方法を示しています。 **servermanagercmd** Web サーバー (IIS) の役割をインストールし、インストールの結果をによって表される XML ファイルに保存 *installResult.xml*します。
```
servermanagercmd -install Web-Server -resultpath installResult.xml
```
次の例は、使用する方法を示します、* * * * whatif パラメーター **servermanagercmd**指示に基づいて、役割、役割サービス、およびインストールまたは削除される機能に関する詳細情報を表示します。によって表される XML 応答ファイルで指定されて*install.xml*します。
```
servermanagercmd -inputpath install.xml -whatif
```

#### <a name="additional-references"></a>その他の参照情報
-   役割、役割サービス、または機能の識別子の完全な一覧を指定できます、 *Id*パラメーター、または XML 応答ファイルでの使用の詳細について**Servermanagercmd**を参照してください[。サーバー マネージャーのヘルプ](https://go.microsoft.com/fwlink/?LinkID=137387)します。 (https://go.microsoft.com/fwlink/?LinkID=137387)。
-   参照してください [サーバー マネージャー コマンドレット](https://go.microsoft.com/fwlink/?LinkID=137653) サーバー マネージャーの使用できる Windows PowerShell コマンドレットの一覧です。
-   [コマンドライン構文キー](command-line-syntax-key.md)
