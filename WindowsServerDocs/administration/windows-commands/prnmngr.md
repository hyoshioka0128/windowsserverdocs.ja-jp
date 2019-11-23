---
title: prnmngr
description: プリンターと接続を追加、削除、および一覧表示する方法について説明します。
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 12981519a1d3bfc079a58e5883bc845955b8a8c6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372070"
---
# <a name="prnmngr"></a>prnmngr

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

追加、削除、およびプリンターまたは設定し、既定のプリンターを表示するだけでなく、プリンター接続を一覧表示します。

## <a name="syntax"></a>構文
```
cscript Prnmngr {-a | -d | -x | -g | -t | -l | -?}[c] [-s <ServerName>] 
[-p <printerName>] [-m <printermodel>] [-r <PortName>] [-u <UserName>] 
[-w <Password>]
```

## <a name="parameters"></a>パラメーター

|           パラメーター           |                                                                                                                                                                                        説明                                                                                                                                                                                        |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|              -a               |                                                                                                                                                                             ローカルプリンター接続を追加します。                                                                                                                                                                              |
|              -d               |                                                                                                                                                                               プリンター接続を削除します。                                                                                                                                                                               |
|              -x               |                                                                                                               指定されたサーバーからすべてのプリンターを削除、 **-s**パラメーター。 サーバーを指定しない場合、Windows は、ローカル コンピューター上のすべてのプリンターを削除します。                                                                                                               |
|              -g               |                                                                                                                                                                               既定のプリンターが表示されます。                                                                                                                                                                               |
|              -t               |                                                                                                                                                        指定されているプリンタを通常使うプリンターを設定、 **-p** パラメーター。                                                                                                                                                         |
|              -l               |                                                                                                         **-s**パラメーターによって指定されたサーバーにインストールされているすべてのプリンターを一覧表示します。 サーバーを指定しない場合、Windows には、ローカル コンピューターにインストールされているプリンターが一覧表示します。                                                                                                         |
|               c               |                                                                                                                                      パラメーターは、プリンターの接続に適用されることを指定します。 使用できる、 **-a** と **-x** パラメーター。                                                                                                                                      |
|        -s <ServerName>        |                                                                                                                  管理するプリンターをホストするリモート コンピューターの名前を指定します。 コンピューターを指定しないと、ローカル コンピューターが使用されます。                                                                                                                  |
|       -p \<printerName >       |                                                                                                                                                                管理するプリンターの名前を指定します。                                                                                                                                                                 |
|     -m \<DrivermodelName >     |                                                                                                          インストールするドライバーを (名) を指定します。 ドライバーは、サポートするプリンターのモデルの名前は多くの場合です。 詳細については、プリンターのマニュアルを参照してください。                                                                                                           |
|        -r \<PortName >         |                                                                         プリンターが接続されているポートを指定します。 パラレル ポートまたはシリアル ポートの場合は、ポートの ID を使用して (たとえば、LPT1: や com1 など:)。 TCP/IP ポートである場合は、ポートを追加したときに指定したポート名を使用します。                                                                          |
| -u \<UserName >-w \<パスワード > | 管理するプリンターをホストするコンピューターに接続するアクセス許可を持つアカウントを指定します。 ターゲット コンピューターのローカル Administrators グループのすべてのメンバーにこれらのアクセス許可があるが、アクセス許可は、他のユーザーに与えることもできます。 アカウントを指定しない場合は、コマンドを実行するこれらのアクセス許可を持つアカウントでログオンする必要があります。 |
|              /?               |                                                                                                                                                                           コマンド プロンプトにヘルプを表示します。                                                                                                                                                                            |

## <a name="remarks"></a>注釈
-   **Prndrvr.vbs**コマンドは、%windir%\system32\ printing_Admin_Scripts\\<language> ディレクトリにある Visual Basic スクリプトです。 このコマンドを使用するには、コマンドプロンプトで「 **cscript** 」と入力し、 **prnmngr**ファイルへの完全なパスを入力するか、ディレクトリを適切なフォルダーに変更します。 次に、例を示します。
    ```
    cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prnmngr
    ```
-   入力した情報にスペースが含まれている場合は、テキストを引用符で囲みます (`"computer Name"`など)。

## <a name="BKMK_examples"></a>例
ローカルコンピューター上の LPT1 に接続され、color printer Driver1 というプリンタードライバーを必要とする colorprinter_2 という名前のプリンターを追加するには、次のように入力します。
```
cscript prnmngr -a -p colorprinter_2 -m "color printer Driver1" -r lpt1:
```
HRServer という名前のリモートコンピューターから colorprinter_2 という名前のプリンターを削除するには、次のように入力します。
```
cscript prnmngr -d -s HRServer -p colorprinter_2 
```

#### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文のキー](command-line-syntax-key.md)
[印刷コマンドリファレンス](print-command-reference.md)
