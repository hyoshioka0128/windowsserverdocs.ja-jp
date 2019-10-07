---
title: prndrvr
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 82b09e3e-bd38-4df1-9953-b0e9ee2565a3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 05e03a4b0b5d686c8fbd1646a775c7f0e5c95706
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372122"
---
# <a name="prndrvr"></a>prndrvr

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

**Prndrvr.vbs**コマンドを使用して、プリンタードライバーの追加、削除、および一覧表示を行います。

## <a name="syntax"></a>構文
```
cscript prndrvr {-a | -d | -l | -x | -?} [-m <model>] [-v {0|1|2|3}] 
[-e <environment>] [-s <ServerName>] [-u <UserName>] [-w <Password>] 
[-h <path>] [-i <inf file>]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------|--------|
|-a|ドライバーをインストールします。|
|-d|ドライバーを削除します。|
|-l|**-s**パラメーターによって指定されたサーバーにインストールされているすべてのプリンタードライバーを一覧表示します。 サーバーを指定しない場合、Windows には、ローカル コンピューターにインストールされているプリンター ドライバーが一覧表示します。|
|-x|**-s**パラメーターによって指定されたサーバー上の論理プリンターによって使用されていない、すべてのプリンタードライバーと追加のプリンタードライバーを削除します。 一覧から削除するサーバーを指定しない場合、Windows は、ローカル コンピューター上のすべての未使用のプリンター ドライバーを削除します。|
|-m \<DrivermodelName @ no__t-1|インストールするドライバーを (名) を指定します。 ドライバーは、サポートするプリンターのモデルの名前は多くの場合です。 詳細については、プリンターのマニュアルを参照してください。|
|-v {0 &#124; 1 &#124; 2 および #124; 3}|インストールするドライバーのバージョンを指定します。 説明を参照して、 **-e**についてのバージョンは現在の環境で使用可能なパラメーターです。 バージョンを指定しないと、ドライバーをインストールするコンピューターで実行されている Windows のバージョンに適切なドライバーのバージョンがインストールされます。<br /><br />-version **0**は、windows 95、windows 98、および windows Millennium edition をサポートしています。<br />-version **1**では、Windows NT 3.51 がサポートされています。<br />-version **2**では、Windows NT 4.0 がサポートされています。<br />-version **3**では、windows Vista、windows XP、windows 2000、および windows Server 2003 オペレーティングシステムがサポートされています。 これは Windows Vista をサポートする唯一のプリンター ドライバーのバージョンであることに注意してください。|
|-e \<Environment >|インストールするドライバーの環境を指定します。 環境を指定しないと、ドライバーをインストールするコンピューターの環境が使用されます。 サポートされている環境のパラメーターは次のとおりです。<br /><br />-    **"WINDOWS NT x86"**<br />-    **"Windows x64"**<br />-    **"WINDOWS IA64"**|
|-s \<ServerName >|管理するプリンターをホストするリモート コンピューターの名前を指定します。 コンピューターを指定しないと、ローカル コンピューターが使用されます。|
|-u \<UserName >-w \< Password >|管理するプリンターをホストするコンピューターに接続するアクセス許可を持つアカウントを指定します。 ターゲット コンピューターのローカル Administrators グループのすべてのメンバーにこれらのアクセス許可があるが、アクセス許可は、他のユーザーに与えることもできます。 アカウントを指定しない場合は、コマンドを実行するこれらのアクセス許可を持つアカウントでログオンする必要があります。|
|-h \<path >|ドライバー ファイルへのパスを指定します。 パスを指定しない場合は、Windows がインストールされている場所へのパスは使用されます。|
|-i \<Filename.inf>|インストールするドライバーの完全なパスとファイル名を指定します。 ファイル名を指定しない場合、スクリプトは Windows ディレクトリの inf サブディレクトリには、受信トレイ プリンター .inf ファイルのいずれかを使用します。<br /><br />ドライバーパスが指定されていない場合、スクリプトは driver ファイル内のドライバーファイルを検索します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈
- **Prndrvr.vbs**コマンドは、%WINdir%\System32\printing_Admin_Scripts @ no__t @ no__t ディレクトリにある Visual Basic スクリプトです。 このコマンドを使用するには、コマンドプロンプトで「 **cscript** 」と入力し、prndrvr.vbs ファイルへの完全なパスを入力するか、ディレクトリを適切なフォルダーに変更します。

  次に、例を示します。
  ```
  cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prndrvr
  ```
- 入力する情報にスペースが含まれる場合は、テキストを囲む引用符を使用して (たとえば、 `"computer Name"`)。
- は、-x オプションは、主な要因が使用されている場合でも、すべての追加のプリンター ドライバー (ドライバー インストール用にクライアントで実行されている別のバージョンの Windows) を削除します。 Fax コンポーネントがインストールされている場合は、このオプションは、fax ドライバも削除されます。 (使用しているキューがない場合) の場合は、使用されていない場合は、プライマリ fax ドライバーが削除されます。 プライマリ fax ドライバーを削除すると、fax を再度有効にする唯一の方法は、fax コンポーネントを再インストールしています。
- パラメーターを指定せずに使用**prndrvr.vbs** 、 **prndrvr.vbs**コマンドのコマンドラインヘルプを表示します。

## <a name="BKMK_examples"></a>例

@No__t-0 \ printServer1 server 上のすべてのドライバーの一覧を表示するには、次のように入力します。
```
cscript Prndrvr -l -s
```

C:\temp フォルダーの種類に格納されているドライバーの C:\temp\Laserprinter1.inf ドライバー情報ファイルを使用して、"レーザープリンターモデル 1" モデル用のバージョン3の Windows x64 プリンタードライバーを追加するには、次のようにします。
```
cscript Prndrvr -a -m "Laser printer model 1" -v 3 -e "Windows x64" -i c:\temp\Laserprinter1.inf -h c:\temp
```

"レーザープリンターモデル 1" 用のバージョン 3 Windows NT x86 プリンタードライバーを削除するには、次のように入力します。
```
cscript Prndrvr -a -m "Laser printer model 1" -v 3 -e "Windows NT x86" 
```

#### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文のキー](command-line-syntax-key.md)
[印刷コマンドリファレンス](print-command-reference.md)
