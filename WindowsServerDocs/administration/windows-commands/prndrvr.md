---
title: prndrvr
description: Prndrvr.vbs コマンドのリファレンストピックでは、プリンタードライバーを追加、削除、および一覧表示します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 82b09e3e-bd38-4df1-9953-b0e9ee2565a3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 62c63819c175f4b3f3770d90da0bd560443ccb77
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85472297"
---
# <a name="prndrvr"></a>prndrvr

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

追加、削除、およびプリンター ドライバーの一覧を表示します。 このコマンドは、ディレクトリにある Visual Basic スクリプトです `%WINdir%\System32\printing_Admin_Scripts\<language>` 。 コマンドプロンプトでこのコマンドを使用するには、「 **cscript** 」に続けて prndrvr.vbs ファイルの完全なパスを入力するか、ディレクトリを適切なフォルダーに変更します。 たとえば、`cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prndrvr` のように指定します。

パラメーターを指定せずに使用します。 **prndrvr.vbs**はコマンドラインヘルプを表示します。

## <a name="syntax"></a>構文

```
cscript prndrvr {-a | -d | -l | -x | -?} [-m <model>] [-v {0|1|2|3}] [-e <environment>] [-s <Servername>] [-u <Username>] [-w <password>] [-h <path>] [-i <inf file>]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
|--|--|
| -a | ドライバーをインストールします。 |
| -d | ドライバーを削除します。 |
| -l | 指定されたサーバーにインストールされているすべてのプリンター ドライバー一覧、 **-s** パラメーター。 サーバーを指定しない場合は、ローカルコンピューターにインストールされているプリンタードライバーが Windows によって一覧表示されます。 |
| -X | 指定されたサーバー上の論理プリンタしてすべてのプリンター ドライバーと使用中でない追加のプリンター ドライバーを削除、 **-s** パラメーター。 一覧から削除するサーバーを指定しない場合、Windows は、ローカルコンピューター上の未使用のプリンタードライバーをすべて削除します。 |
| -m`<model_name>` | インストールするドライバーを (名) を指定します。 ドライバーは、サポートするプリンターのモデルの名前は多くの場合です。 詳細については、プリンターのマニュアルを参照してください。 |
| `-v {0|1|2|3}` | インストールするドライバーのバージョンを指定します。 説明を参照して、 **-e**についてのバージョンは現在の環境で使用可能なパラメーターです。 バージョンを指定しない場合は、ドライバーをインストールするコンピューターで実行されている Windows のバージョンに適したバージョンのドライバーがインストールされます。 |
| -e `<environment>` | インストールするドライバーの環境を指定します。 環境を指定しない場合は、ドライバーをインストールするコンピューターの環境が使用されます。 サポートされている環境パラメーターは、 **WINDOWS NT x86**、 **windows x64** 、または**windows IA64**です。 |
| -s`<Servername>` | 管理するプリンターをホストするリモート コンピューターの名前を指定します。 コンピューターを指定しない場合は、ローカルコンピューターが使用されます。 |
| -u `<Username>` -w`<password>` | 管理するプリンターをホストするコンピューターに接続するアクセス許可を持つアカウントを指定します。 ターゲット コンピューターのローカル Administrators グループのすべてのメンバーはこれらのアクセス許可を持っていますが、アクセス許可を他のユーザーに与えることもできます。 アカウントを指定しない場合は、コマンドが機能するように、これらのアクセス許可を持つアカウントでログオンする必要があります。 |
| -h`<path>` | ドライバー ファイルへのパスを指定します。 パスを指定しない場合は、Windows がインストールされている場所へのパスが使用されます。 |
| -i`<filename.inf>` | インストールするドライバーの完全なパスとファイル名を指定します。 ファイル名を指定しない場合、スクリプトでは、Windows ディレクトリの inf サブディレクトリにある受信トレイの .inf ファイルの1つを使用します。<p>ドライバーパスが指定されていない場合、スクリプトは driver.cab ファイル内のドライバーファイルを検索します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>注釈

- 入力した情報にスペースが含まれている場合は、テキストを引用符で囲みます (例、"コンピューター名")。

- **-X**パラメーターは、プライマリドライバーが使用されている場合でも、追加のプリンタードライバー (代替バージョンの Windows を実行しているクライアントで使用するためにインストールされているドライバー) をすべて削除します。 Fax コンポーネントがインストールされている場合は、このオプションは、fax ドライバも削除されます。 (使用しているキューがない場合) の場合は、使用されていない場合は、プライマリ fax ドライバーが削除されます。 プライマリ fax ドライバーを削除すると、fax を再度有効にする唯一の方法は、fax コンポーネントを再インストールしています。

### <a name="examples"></a>例

ローカル printServer1 サーバー上のすべてのドライバーの一覧を表示するには \\ 、次のように入力します。

```
cscript prndrvr -l -s
```

バージョン3の Windows x64 プリンタードライバーを追加するには、c:\temp フォルダーに格納されているドライバーの c:\temp\Laserprinter1.inf ドライバー情報ファイルを使用して、次のように入力します。

```
cscript prndrvr -a -m Laser printer model 1 -v 3 -e Windows x64 -i c:\temp\Laserprinter1.inf -h c:\temp
```

バージョン3の Windows x64 プリンタードライバーのレーザープリンターモデル1を削除するには、次のように入力します。

```
cscript prndrvr -a -m Laser printer model 1 -v 3 -e Windows x64
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [印刷コマンドのリファレンス](print-command-reference.md)
