---
title: prnmngr
description: 追加、削除、およびプリンターとの接続を一覧表示する方法について説明します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 39eee1a8-4b41-4c9f-941e-486495135eb8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 2c0aa44cc6f27e553bf8c1b57356b884bc0cd632
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887203"
---
# <a name="prnmngr"></a>prnmngr

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

追加、削除、およびプリンターまたは設定し、既定のプリンターを表示するだけでなく、プリンター接続を一覧表示します。

## <a name="syntax"></a>構文
```
cscript Prnmngr {-a | -d | -x | -g | -t | -l | -?}[c] [-s <ServerName>] 
[-p <printerName>] [-m <printermodel>] [-r <PortName>] [-u <UserName>] 
[-w <Password>]
```

## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|-a|ローカル プリンター接続を追加します。|
|-d|プリンター接続を削除します。|
|-x|指定されたサーバーからのすべてのプリンターを削除、 **-s**パラメーター。 サーバーを指定しない場合、Windows は、ローカル コンピューター上のすべてのプリンターを削除します。|
|-g|既定のプリンターが表示されます。|
|-t|指定されているプリンタを通常使うプリンターを設定、 **-p** パラメーター。|
|-l|指定されたサーバーにインストールされているすべてのプリンターを一覧表示、 **-s**パラメーター。 サーバーを指定しない場合、Windows には、ローカル コンピューターにインストールされているプリンターが一覧表示します。|
|c|パラメーターは、プリンターの接続に適用されることを指定します。 使用できる、 **-a** と **-x** パラメーター。|
|-s <ServerName>|管理するプリンターをホストするリモート コンピューターの名前を指定します。 コンピューターを指定しないと、ローカル コンピューターが使用されます。|
|-p \<printerName>|管理するプリンターの名前を指定します。|
|-m \<DrivermodelName>|インストールするドライバーを (名) を指定します。 ドライバーは、サポートするプリンターのモデルの名前は多くの場合です。 詳細については、プリンターのマニュアルを参照してください。|
|-r \<PortName>|プリンターが接続されているポートを指定します。 パラレル ポートまたはシリアル ポートの場合は、ポートの ID を使用して (たとえば、LPT1: や com1 など:)。 TCP/IP ポートである場合は、ポートを追加したときに指定したポート名を使用します。|
|-u \<UserName> -w \<Password>|管理するプリンターをホストするコンピューターに接続するアクセス許可を持つアカウントを指定します。 ターゲット コンピューターのローカル Administrators グループのすべてのメンバーにこれらのアクセス許可があるが、アクセス許可は、他のユーザーに与えることもできます。 アカウントを指定しない場合は、コマンドを実行するこれらのアクセス許可を持つアカウントでログオンする必要があります。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈
-   **Prndrvr**コマンドは、%WINdir%\System32\printing_Admin_Scripts にある Visual Basic スクリプト\\<language>ディレクトリ。 このコマンドでは、コマンド プロンプトで、使用する入力**cscript**への完全パスを続けて、 **prnmngr**ファイル、または適切なフォルダーにディレクトリを変更します。 次に、例を示します。
    ```
    cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prnmngr
    ```
-   入力する情報にスペースが含まれている場合は、テキストを囲む引用符を使用して (たとえば、 `"computer Name"`)。

## <a name="BKMK_examples"></a>例
ローカル コンピューターの LPT1 に接続されている、カラー プリンター Driver1 と呼ばれるプリンタ ドライバを必要とする colorprinter_2 をという名前のプリンターを追加するには、次のように入力します。
```
cscript prnmngr -a -p colorprinter_2 -m "color printer Driver1" -r lpt1:
```
HRServer という名前のリモート コンピューターから colorprinter_2 をという名前のプリンターを削除するには、次のように入力します。
```
cscript prnmngr -d -s HRServer -p colorprinter_2 
```

#### <a name="additional-references"></a>その他の参照
[コマンドライン構文のポイント](command-line-syntax-key.md)
[印刷コマンドのリファレンス](print-command-reference.md)
