---
title: prndrvr
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 13c89b78ba177362cb9bf1d6a1e601eefb4f4ce3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882123"
---
# <a name="prndrvr"></a>prndrvr

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

使用して、 **prndrvr**コマンドを追加、削除、およびプリンター ドライバーを一覧表示します。

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
|-l|指定されたサーバーにインストールされているすべてのプリンター ドライバーの一覧、 **-s**パラメーター。 サーバーを指定しない場合、Windows には、ローカル コンピューターにインストールされているプリンター ドライバーが一覧表示します。|
|-x|指定されたサーバー上の論理プリンタしてすべてのプリンター ドライバーと使用中でない追加のプリンター ドライバーを削除、 **-s**パラメーター。 一覧から削除するサーバーを指定しない場合、Windows は、ローカル コンピューター上のすべての未使用のプリンター ドライバーを削除します。|
|-m \<DrivermodelName\>|インストールするドライバーを (名) を指定します。 ドライバーは、サポートするプリンターのモデルの名前は多くの場合です。 詳細については、プリンターのマニュアルを参照してください。|
|-v {0 &#124; 1 &#124; 2 および #124; 3}|インストールするドライバーのバージョンを指定します。 説明を参照して、 **-e**についてのバージョンは現在の環境で使用可能なパラメーターです。 バージョンを指定しないと、ドライバーをインストールするコンピューターで実行されている Windows のバージョンに適切なドライバーのバージョンがインストールされます。<br /><br />-バージョン**0** Windows 95、Windows 98、および Windows Millennium edition をサポートします。<br />-バージョン**1** Windows NT 3.51 をサポートしています。<br />-バージョン**2** Windows NT 4.0 をサポートしています。<br />-バージョン**3** Windows Vista、Windows XP、Windows 2000、および Windows Server 2003 オペレーティング システムをサポートしています。 これは Windows Vista をサポートする唯一のプリンター ドライバーのバージョンであることに注意してください。|
|-e\<環境 >|インストールするドライバーの環境を指定します。 環境を指定しないと、ドライバーをインストールするコンピューターの環境が使用されます。 サポートされている環境のパラメーターは次のとおりです。<br /><br />-   **"Windows NT x86"**<br />-   **"Windows x64"**<br />-   **"Windows IA64"**|
|-s \<ServerName>|管理するプリンターをホストするリモート コンピューターの名前を指定します。 コンピューターを指定しないと、ローカル コンピューターが使用されます。|
|-u \<UserName> -w \<Password>|管理するプリンターをホストするコンピューターに接続するアクセス許可を持つアカウントを指定します。 ターゲット コンピューターのローカル Administrators グループのすべてのメンバーにこれらのアクセス許可があるが、アクセス許可は、他のユーザーに与えることもできます。 アカウントを指定しない場合は、コマンドを実行するこれらのアクセス許可を持つアカウントでログオンする必要があります。|
|-h\<パス >|ドライバー ファイルへのパスを指定します。 パスを指定しない場合は、Windows がインストールされている場所へのパスは使用されます。|
|-i \<Filename.inf>|インストールするドライバーの完全なパスとファイル名を指定します。 ファイル名を指定しない場合、スクリプトは Windows ディレクトリの inf サブディレクトリには、受信トレイ プリンター .inf ファイルのいずれかを使用します。<br /><br />ドライバーのパスが指定されていない場合、スクリプトは、driver.cab ファイル内のドライバー ファイルを検索します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈
-   **Prndrvr**コマンドは、%WINdir%\System32\printing_Admin_Scripts にある Visual Basic スクリプト\\<language>ディレクトリ。 このコマンドでは、コマンド プロンプトで、使用する入力**cscript** prndrvr ファイル、または適切なフォルダーにディレクトリを変更する、完全なパスを続けています。
   
   次に、例を示します。
    ```
    cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prndrvr
    ```
-   入力する情報にスペースが含まれる場合は、テキストを囲む引用符を使用して (たとえば、 `"computer Name"`)。
-   は、-x オプションは、主な要因が使用されている場合でも、すべての追加のプリンター ドライバー (ドライバー インストール用にクライアントで実行されている別のバージョンの Windows) を削除します。 Fax コンポーネントがインストールされている場合は、このオプションは、fax ドライバも削除されます。 (使用しているキューがない場合) の場合は、使用されていない場合は、プライマリ fax ドライバーが削除されます。 プライマリ fax ドライバーを削除すると、fax を再度有効にする唯一の方法は、fax コンポーネントを再インストールしています。
-   パラメーターを指定せずに使用される**prndrvr**コマンド ライン ヘルプを表示、 **prndrvr**コマンド。

## <a name="BKMK_examples"></a>例

すべてのドライバーの一覧を表示、 \\\printServer1 サーバー、タイプ。
```
cscript Prndrvr -l -s
```

「レーザー プリンター モデル 1」モデルの C:\temp\Laserprinter1.inf ドライバー情報ファイルを C:\temp フォルダーの種類に格納されているドライバーを使用してプリンター用バージョン 3 Windows x64 プリンター ドライバーを追加します。
```
cscript Prndrvr -a -m "Laser printer model 1" -v 3 -e "Windows x64" -i c:\temp\Laserprinter1.inf -h c:\temp
```

「レーザー プリンター モデル 1」のバージョン 3 Windows NT x86 のプリンター ドライバーを削除するには、次のように入力します。
```
cscript Prndrvr -a -m "Laser printer model 1" -v 3 -e "Windows NT x86" 
```

#### <a name="additional-references"></a>その他の参照
[コマンドライン構文のポイント](command-line-syntax-key.md)
[印刷コマンドのリファレンス](print-command-reference.md)
