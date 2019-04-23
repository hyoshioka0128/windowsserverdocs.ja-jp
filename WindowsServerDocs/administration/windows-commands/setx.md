---
title: setx
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ef37482f-f8a8-4765-951a-2518faac3f44
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5a650fae246d71d8c1f9822dfa9ff8e96d855b4b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886573"
---
# <a name="setx"></a>setx



作成するか、プログラミングやスクリプトを必要とせず、ユーザーまたはシステム環境で環境変数を変更します。 **Setx** コマンドは、また、レジストリ キーの値を取得し、テキスト ファイルに書き込みます。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
setx [/s <Computer> [/u [<Domain>\]<User name> [/p [<Password>]]]] <Variable> <Value> [/m]
setx [/s <Computer> [/u [<Domain>\]<User name> [/p [<Password>]]]] [<Variable>] /k <Path> [/m]
setx [/s <Computer> [/u [<Domain>\]<User name> [/p [<Password>]]]] /f <FileName> {[<Variable>] {/a <X>,<Y> | /r <X>,<Y> "<String>"} [/m] | /x} [/d <Delimiters>]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/s\<コンピューター >|名前またはリモート コンピューターの IP アドレスを指定します。 円記号を使用しないでください。 既定値は、ローカル コンピューターの名前です。|
|/u [\<ドメイン >\]<User name>|指定したユーザー アカウントの資格情報でスクリプトを実行します。 既定値は、システムのアクセス許可です。|
|/p [\<パスワード >]|指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。|
|\<変数 >|設定する環境変数の名前を指定します。|
|\<値 >|環境変数を設定する値を指定します。|
|/k\<パス >|変数のベースをレジストリ キーの情報に設定されるように指定します。 P*パス* は次の構文を使用します。</br>`\\<HIVE>\<KEY>\...\<Value>`</br>たとえば、次のパスを指定します。</br>`HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\TimeZoneInformation\StandardName`|
|/f\<ファイル名 >|使用するファイルを指定します。|
|/a \<X >、<Y>|検索パラメーターとして、絶対座標およびオフセットを指定します。|
|/r \<X>,<Y> "<String>"|相対座標とからのオフセットを指定 **文字列** としてパラメーターを検索します。|
|/m|システムの環境での変数の設定を指定します。 既定の設定は、ローカルの環境です。|
|/x|ファイルを無視して、座標が表示されます、 **/a**, 、**/r**, 、および **/d** コマンド ライン オプションです。|
|/d\<区切り記号 >|などの区切り記号を指定"**、**"または"**\**"だけでなく 4 つの組み込みの区切り記号に使用する、スペース、タブ、ENTER、および改行します。 有効な区切り記号には、ASCII 文字が含まれます。 区切り文字の最大数は、15、組み込みの区切り記号を含みます。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

-   **Setx** コマンドは、UNIX ユーティリティ SETENV に似ています。
-   **Setx** は直接かつ永続的にシステムを設定する環境変数の値のみコマンドラインまたはプログラムによる方法を提供します。 システム環境変数を使用して手動で構成できます **コントロール パネルの ** またはレジストリ エディターを使用します。 **設定** コマンド インタープリター (Cmd.exe) の内部では、コマンドが現在のコンソール ウィンドウのみのユーザー環境変数を設定します。
-   使用することができます、 **setx**コマンドを次の 3 つのソース (モード) のいずれかからユーザーとシステムの値を環境変数を設定します。コマンド ライン モード、レジストリ モード、またはファイル モード。
-   **Setx** レジストリにマスター環境変数に書き込みます。 変数の設定と **setx** 変数が現在のコマンド ウィンドウのみで使用できるも現在のコマンド ウィンドウにします。
-   **HKEY_CURRENT_USER** と **HKEY_LOCAL_MACHINE** 、唯一サポートされているレジストリ ハイブです。 REG_DWORD、REG_EXPAND_SZ、REG_SZ および REG_MULTI_SZ は、有効な **RegKey** データ型。
-   アクセスできるとき **REG_MULTI_SZ** 、レジストリでは、最初の項目のみの値が抽出され、使用できます。
-   使用することはできません、 **setx** コマンドをローカル コンピューターまたはシステム環境に追加されている値を削除します。 使用する **設定** 変数名とローカルの環境から対応する値を削除する値はありません。
-   REG_DWORD レジストリ値が抽出され、16 進数のモードで使用します。
-   ライン フィード (CRLF) のテキスト ファイルだけをファイルのモードは、キャリッジ リターンの解析をサポートします。

## <a name="BKMK_examples"></a>例

Brand1 の値に、ローカル環境でコンピューターの環境変数を設定するには、次のように入力します。
```
setx MACHINE Brand1
```
値 Brand1 コンピューターにシステムの環境でコンピューターの環境変数を設定するには、次のように入力します。
```
setx MACHINE "Brand1 Computer" /m
```
PATH 環境変数で定義された検索パスを使用するローカル環境で MYPATH 環境変数を設定するには、次のように入力します。
```
setx MYPATH %PATH%
```
交換した後、PATH 環境変数で定義された検索パスを使用するローカル環境で MYPATH 環境変数を設定する **~** と **%**, 、種類。
```
setx MYPATH ~PATH~ 
```
Brand1 に Computer1 という名前のリモート コンピューター上のローカル環境でコンピューターの環境変数を設定するには、次のように入力します。
```
setx /s computer1 /u maindom\hiropln /p p@ssW23 MACHINE Brand1
```
Computer1 という名前のリモート コンピューター上の PATH 環境変数で定義された検索パスを使用するローカル環境で MYPATH 環境変数を設定するには、次のように入力します。
```
setx /s computer1 /u maindom\hiropln /p p@ssW23 MYPATH %PATH%
```
値をローカル環境で費用の環境変数を設定する、 **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\TimeZoneInformation\StandardName** レジストリ キーの型。
```
setx TZONE /k HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\TimeZoneInformation\StandardName 
```
Computer1 をという名前の値をリモート コンピューターのローカル環境で費用の環境変数を設定する、 **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\TimeZoneInformation\StandardName** レジストリ キーの型。
```
setx /s computer1 /u maindom\hiropln /p p@ssW23 TZONE /k HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\TimeZoneInformation\StandardName 
```
値をシステムの環境でビルドの環境変数を設定する、 **HKEY_LOCAL_MACHINE\Software\Microsoft\WindowsNT\CurrentVersion\CurrentBuildNumber** レジストリ キーの型。
```
setx BUILD /k "HKEY_LOCAL_MACHINE\Software\Microsoft\WindowsNT\CurrentVersion\CurrentBuildNumber" /m
```
Computer1 をという名前の値をリモート コンピューターのシステムの環境でビルドの環境変数を設定する、 **HKEY_LOCAL_MACHINE\Software\Microsoft\WindowsNT\CurrentVersion\CurrentBuildNumber** レジストリ キーの型。
```
setx /s computer1 /u maindom\hiropln /p p@ssW23  BUILD /k "HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\CurrentBuildNumber" /m
```
内容の対応する座標、と共に Ipconfig.out、という名前のファイルの内容を表示するには、次のように入力します。
```
setx /f ipconfig.out /x
```
座標 5,11 ファイル Ipconfig.out で見つかった値に、ローカル環境で IPADDR 環境変数を設定するには、次のように入力します。
```
setx IPADDR /f ipconfig.out /a 5,11
```
座標 5, 3 Ipconfig.out 区切り記号付きのファイルで見つかった値にローカルの環境で OCTET1 環境変数を設定する **"#$\*."**, 、種類。
```
setx OCTET1 /f ipconfig.out /a 5,3 /d "#$*." 
```
「ゲートウェイ」の座標に関して座標 0,7 ファイル Ipconfig.out で見つかった値に、ローカル環境で IPGATEWAY 環境変数を設定するには、次のように入力します。
```
setx IPGATEWAY /f ipconfig.out /r 0,7 Gateway 
```
Ipconfig.out という名前のファイルの内容を表示する: 内容の対応する座標と共に: Computer1 という名前のコンピューターを入力します。
```
setx /s computer1 /u maindom\hiropln /p p@ssW23 /f ipconfig.out /x 
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)