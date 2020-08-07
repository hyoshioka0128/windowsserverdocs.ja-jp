---
title: setx
description: ユーザーまたはシステム環境で環境変数を作成または変更する setx の参照記事。プログラミングやスクリプトは必要ありません。
ms.topic: article
ms.assetid: ef37482f-f8a8-4765-951a-2518faac3f44
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0edab4ce56d3e43e26c1d14b32403a2954cbbce6
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87882523"
---
# <a name="setx"></a>setx

作成するか、プログラミングやスクリプトを必要とせず、ユーザーまたはシステム環境で環境変数を変更します。 **Setx** コマンドは、また、レジストリ キーの値を取得し、テキスト ファイルに書き込みます。



## <a name="syntax"></a>構文

```
setx [/s <Computer> [/u [<Domain>\]<User name> [/p [<Password>]]]] <Variable> <Value> [/m]
setx [/s <Computer> [/u [<Domain>\]<User name> [/p [<Password>]]]] [<Variable>] /k <Path> [/m]
setx [/s <Computer> [/u [<Domain>\]<User name> [/p [<Password>]]]] /f <FileName> {[<Variable>] {/a <X>,<Y> | /r <X>,<Y> <String>} [/m] | /x} [/d <Delimiters>]
```

### <a name="parameters"></a>パラメーター

|         パラメーター          |                                                                                                                                              説明                                                                                                                                              |
|----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       /s\<Computer>       |                                                                                  名前またはリモート コンピューターの IP アドレスを指定します。 円記号を使用しないでください。 既定値は、ローカル コンピューターの名前です。                                                                                  |
| u\<Domain>\]<User name> |                                                                                           指定したユーザー アカウントの資格情報でスクリプトを実行します。 既定値は、システムのアクセス許可です。                                                                                            |
|      /p [\<Password>]      |                                                                                                         指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。                                                                                                         |
|        \<Variable>         |                                                                                                                 設定する環境変数の名前を指定します。                                                                                                                  |
|          \<Value>          |                                                                                                                環境変数を設定する値を指定します。                                                                                                                 |
|         /k\<Path>         | 変数のベースをレジストリ キーの情報に設定されるように指定します。 P*パス* は次の構文を使用します。</br>`\\<HIVE>\<KEY>\...\<Value>`</br>たとえば、[次のパスを指定します。</br>`HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\TimeZoneInformation\StandardName` |
|      /f \<File name>       |                                                                                                                               使用するファイルを指定します。                                                                                                                                |
|        /a \<X> 、<Y>         |                                                                                                                    検索パラメーターとして、絶対座標およびオフセットを指定します。                                                                                                                    |
|   /r \<X> 、 <Y><String>   |                                                                                                            相対座標とからのオフセットを指定 **文字列** としてパラメーターを検索します。                                                                                                            |
|             /m             |                                                                                                システムの環境での変数の設定を指定します。 既定の設定は、ローカルの環境です。                                                                                                 |
|             /x             |                                                                                                       ファイルを無視して、座標が表示されます、 **/a**, 、**/r**, 、および **/d** コマンド ライン オプションです。                                                                                                        |
|      d\<Delimiters>      |                    **などの**区切り記号を指定します。また、 **\\** 4 つの組み込みの区切り記号 (スペース、タブ、ENTER、およびラインフィード) に加えて使用することもできます。 有効な区切り記号には、ASCII 文字が含まれます。 区切り文字の最大数は、15、組み込みの区切り記号を含みます。                    |
|             /?             |                                                                                                                                 コマンド プロンプトにヘルプを表示します。                                                                                                                                  |

## <a name="remarks"></a>Remarks

-   **Setx** コマンドは、UNIX ユーティリティ SETENV に似ています。
-   **Setx** は直接かつ永続的にシステムを設定する環境変数の値のみコマンドラインまたはプログラムによる方法を提供します。 システム環境変数を使用して手動で構成できます **コントロール パネルの [** またはレジストリ エディターを使用します。 **設定** コマンド インタープリター (Cmd.exe) の内部では、コマンドが現在のコンソール ウィンドウのみのユーザー環境変数を設定します。
-   使用することができます、 **setx** から 3 つのソース (モード) のいずれかのユーザーおよびシステムの値を環境変数を設定するコマンド。 コマンド ライン モード、レジストリ モード、またはファイルのモードです。
-   **Setx** レジストリにマスター環境変数に書き込みます。 変数の設定と **setx** 変数が現在のコマンド ウィンドウのみで使用できるも現在のコマンド ウィンドウにします。
-   **HKEY_CURRENT_USER** と **HKEY_LOCAL_MACHINE** 、唯一サポートされているレジストリ ハイブです。 REG_DWORD、REG_EXPAND_SZ、REG_SZ および REG_MULTI_SZ は、有効な **RegKey** データ型。
-   アクセスできるとき **REG_MULTI_SZ** 、レジストリでは、最初の項目のみの値が抽出され、使用できます。
-   使用することはできません、 **setx** コマンドをローカル コンピューターまたはシステム環境に追加されている値を削除します。 使用する **設定** 変数名とローカルの環境から対応する値を削除する値はありません。
-   REG_DWORD レジストリ値が抽出され、16 進数のモードで使用します。
-   ライン フィード (CRLF) のテキスト ファイルだけをファイルのモードは、キャリッジ リターンの解析をサポートします。

## <a name="examples"></a>例

Brand1 の値に、ローカル環境でコンピューターの環境変数を設定するには、次のように入力します。
```
setx MACHINE Brand1
```
値 Brand1 コンピューターにシステムの環境でコンピューターの環境変数を設定するには、次のように入力します。
```
setx MACHINE Brand1 Computer /m
```
PATH 環境変数で定義された検索パスを使用するローカル環境で MYPATH 環境変数を設定するには、次のように入力します。
```
setx MYPATH %PATH%
```
をに置き換えた後、PATH 環境変数で定義された検索パスを使用するようにローカル環境の MYPATH 環境変数を設定するには **~** **%** 、次のように入力します。
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
setx BUILD /k HKEY_LOCAL_MACHINE\Software\Microsoft\WindowsNT\CurrentVersion\CurrentBuildNumber /m
```
Computer1 をという名前の値をリモート コンピューターのシステムの環境でビルドの環境変数を設定する、 **HKEY_LOCAL_MACHINE\Software\Microsoft\WindowsNT\CurrentVersion\CurrentBuildNumber** レジストリ キーの型。
```
setx /s computer1 /u maindom\hiropln /p p@ssW23  BUILD /k HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\CurrentBuildNumber /m
```
内容の対応する座標、と共に Ipconfig.out、という名前のファイルの内容を表示するには、次のように入力します。
```
setx /f ipconfig.out /x
```
座標 5,11 ファイル Ipconfig.out で見つかった値に、ローカル環境で IPADDR 環境変数を設定するには、次のように入力します。
```
setx IPADDR /f ipconfig.out /a 5,11
```
ローカル環境で OCTET1 環境変数を、座標5で見つかった値に設定するには、次のように入力し** #$ \* ます。**
```
setx OCTET1 /f ipconfig.out /a 5,3 /d #$*.
```
ローカル環境で IPGATEWAY 環境変数を設定するには、次のように入力して、ゲートウェイの座標に関して、座標 0, 7 で見つかった値を指定します。
```
setx IPGATEWAY /f ipconfig.out /r 0,7 Gateway
```
Ipconfig.out という名前のファイルの内容を表示する: 内容の対応する座標と共に: Computer1 という名前のコンピューターを入力します。
```
setx /s computer1 /u maindom\hiropln /p p@ssW23 /f ipconfig.out /x
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)