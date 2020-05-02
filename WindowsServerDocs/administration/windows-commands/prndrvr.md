---
title: prndrvr
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 82b09e3e-bd38-4df1-9953-b0e9ee2565a3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c47a49146b1f20fb327d93c8cd00969cbe0a2304
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722826"
---
# <a name="prndrvr"></a>prndrvr

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

**Prndrvr.vbs**コマンドを使用して、プリンタードライバーの追加、削除、および一覧表示を行います。

## <a name="syntax"></a>構文
```
cscript prndrvr {-a | -d | -l | -x | -?} [-m <model>] [-v {0|1|2|3}] 
[-e <environment>] [-s <ServerName>] [-u <UserName>] [-w <Password>] 
[-h <path>] [-i <inf file>]
```

### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|-------|--------|
|-a|ドライバーをインストールします。|
|-d|ドライバーを削除します。|
|-l|**-s**パラメーターによって指定されたサーバーにインストールされているすべてのプリンタードライバーを一覧表示します。 サーバーを指定しない場合、Windows には、ローカル コンピューターにインストールされているプリンター ドライバーが一覧表示します。|
|-X|**-s**パラメーターによって指定されたサーバー上の論理プリンターによって使用されていない、すべてのプリンタードライバーと追加のプリンタードライバーを削除します。 一覧から削除するサーバーを指定しない場合、Windows は、ローカル コンピューター上のすべての未使用のプリンター ドライバーを削除します。|
|-m \<DrivermodelName\>|インストールするドライバーを (名) を指定します。 ドライバーは、サポートするプリンターのモデルの名前は多くの場合です。 詳細については、プリンターのマニュアルを参照してください。|
|-v {0 & #124; 1 & #124; 2 および #124; 3}|インストールするドライバーのバージョンを指定します。 説明を参照して、 **-e**についてのバージョンは現在の環境で使用可能なパラメーターです。 バージョンを指定しないと、ドライバーをインストールするコンピューターで実行されている Windows のバージョンに適切なドライバーのバージョンがインストールされます。<p>-version **0**は、windows 95、windows 98、および windows Millennium edition をサポートしています。<br />-version **1**では、Windows NT 3.51 がサポートされています。<br />-version **2**では、Windows NT 4.0 がサポートされています。<br />-version **3**では、windows Vista、windows XP、windows 2000、および windows Server 2003 オペレーティングシステムがサポートされています。 これは Windows Vista をサポートする唯一のプリンター ドライバーのバージョンであることに注意してください。|
|-e \<環境>|インストールするドライバーの環境を指定します。 環境を指定しないと、ドライバーをインストールするコンピューターの環境が使用されます。 サポートされている環境のパラメーターは次のとおりです。<p>-   **Windows NT x86**<br />-   **Windows x64**<br />-   **Windows IA64**|
|-s \<ServerName>|管理するプリンターをホストするリモート コンピューターの名前を指定します。 コンピューターを指定しないと、ローカル コンピューターが使用されます。|
|-u \<ユーザー名>- \<w パスワード>|管理するプリンターをホストするコンピューターに接続するアクセス許可を持つアカウントを指定します。 ターゲット コンピューターのローカル Administrators グループのすべてのメンバーはこれらのアクセス許可を持っていますが、アクセス許可を他のユーザーに与えることもできます。 アカウントを指定しない場合は、コマンドを実行するこれらのアクセス許可を持つアカウントでログオンする必要があります。|
|-h \<パス>|ドライバー ファイルへのパスを指定します。 パスを指定しない場合は、Windows がインストールされている場所へのパスは使用されます。|
|-i \<Filename. inf>|インストールするドライバーの完全なパスとファイル名を指定します。 ファイル名を指定しない場合、スクリプトは Windows ディレクトリの inf サブディレクトリには、受信トレイ プリンター .inf ファイルのいずれかを使用します。<p>ドライバーパスが指定されていない場合、スクリプトは driver ファイル内のドライバーファイルを検索します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>Remarks
- **Prndrvr.vbs**コマンドは、%windir%\system32\ printing_Admin_Scripts\\ <language>ディレクトリにある Visual Basic スクリプトです。 このコマンドを使用するには、コマンドプロンプトで「 **cscript** 」と入力し、prndrvr.vbs ファイルへの完全なパスを入力するか、ディレクトリを適切なフォルダーに変更します。

  次に例を示します。
  ```
  cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prndrvr
  ```
- 入力する情報にスペースが含まれる場合は、テキストを囲む引用符を使用して (たとえば、 `computer Name`)。
- は、-x オプションは、主な要因が使用されている場合でも、すべての追加のプリンター ドライバー (ドライバー インストール用にクライアントで実行されている別のバージョンの Windows) を削除します。 Fax コンポーネントがインストールされている場合は、このオプションは、fax ドライバも削除されます。 (使用しているキューがない場合) の場合は、使用されていない場合は、プライマリ fax ドライバーが削除されます。 プライマリ fax ドライバーを削除すると、fax を再度有効にする唯一の方法は、fax コンポーネントを再インストールしています。
- パラメーターを指定せずに使用**prndrvr.vbs** 、 **prndrvr.vbs**コマンドのコマンドラインヘルプを表示します。

## <a name="examples"></a>例

\\\ Printserver1 サーバー上のすべてのドライバーを一覧表示するには、次のように入力します。
```
cscript Prndrvr -l -s
```

バージョン3の Windows x64 プリンタードライバーを追加するには、C:\temp フォルダーの種類に格納されているドライバーの C:\temp\Laserprinter1.inf ドライバー情報ファイルを使用して、プリンターのレーザープリンターモデル1モデルのプリンタードライバーを追加します。
```
cscript Prndrvr -a -m Laser printer model 1 -v 3 -e Windows x64 -i c:\temp\Laserprinter1.inf -h c:\temp
```

バージョン3の Windows NT x86 プリンタードライバーのレーザープリンターモデル1を削除するには、次のように入力します。
```
cscript Prndrvr -a -m Laser printer model 1 -v 3 -e Windows NT x86 
```

## <a name="additional-references"></a>その他のリファレンス
- [コマンドライン構文キー](command-line-syntax-key.md)
[印刷コマンドのリファレンス](print-command-reference.md)
