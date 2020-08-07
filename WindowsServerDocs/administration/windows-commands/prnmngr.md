---
title: prnmngr
description: 既定のプリンターの設定と表示に加えて、プリンターまたはプリンターの接続を追加、削除、および一覧表示する prnmngr コマンドの参照記事です。
ms.topic: article
ms.assetid: 39eee1a8-4b41-4c9f-941e-486495135eb8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 53c49de622b38efc6e536d8113b58b43ffef2dbe
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87884732"
---
# <a name="prnmngr"></a>prnmngr

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

追加、削除、およびプリンターまたは設定し、既定のプリンターを表示するだけでなく、プリンター接続を一覧表示します。 このコマンドは、ディレクトリにある Visual Basic スクリプトです `%WINdir%\System32\printing_Admin_Scripts\<language>` 。 コマンドプロンプトでこのコマンドを使用するには、「 **cscript** 」に続けて prnmngr ファイルの完全なパスを入力するか、ディレクトリを適切なフォルダーに変更します。 (例: `cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prnmngr`)。

## <a name="syntax"></a>構文

```
cscript prnmngr {-a | -d | -x | -g | -t | -l | -?}[c] [-s <Servername>] [-p <Printername>] [-m <printermodel>] [-r <portname>] [-u <Username>]
[-w <password>]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
|--|--|
| -a | ローカル プリンター接続を追加します。 |
| -d | プリンター接続を削除します。 |
| -X | **-S**パラメーターによって指定されたサーバーからすべてのプリンターを削除します。 サーバーを指定しない場合、Windows はローカルコンピューター上のすべてのプリンターを削除します。 |
| -g | 既定のプリンターが表示されます。 |
| -t | 指定されているプリンタを通常使うプリンターを設定、 **-p** パラメーター。 |
| -l | 指定されたサーバーにインストールされているすべてのプリンターを一覧表示、 **-s** パラメーター。 サーバーを指定しない場合は、ローカルコンピューターにインストールされているプリンターが Windows によって一覧表示されます。 |
| c | パラメーターは、プリンターの接続に適用されることを指定します。 使用できる、 **-a** と **-x** パラメーター。 |
| -s `<Servername>` | 管理するプリンターをホストするリモート コンピューターの名前を指定します。 コンピューターを指定しない場合は、ローカルコンピューターが使用されます。 |
| -p`<Printername>` | 管理するプリンターの名前を指定します。 |
| -m `<Modelname>` | インストールするドライバーを (名) を指定します。 ドライバーは、サポートするプリンターのモデルの名前は多くの場合です。 詳細については、プリンターのマニュアルを参照してください。 |
| -r`<portname>` | プリンターが接続されているポートを指定します。 パラレル ポートまたはシリアル ポートの場合は、ポートの ID を使用して (たとえば、LPT1: や com1 など:)。 TCP/IP ポートである場合は、ポートを追加したときに指定したポート名を使用します。 |
| -u `<Username>` -w`<password>` | 管理するプリンターをホストするコンピューターに接続するアクセス許可を持つアカウントを指定します。 ターゲット コンピューターのローカル Administrators グループのすべてのメンバーはこれらのアクセス許可を持っていますが、アクセス許可を他のユーザーに与えることもできます。 アカウントを指定しない場合は、コマンドが機能するように、これらのアクセス許可を持つアカウントでログオンする必要があります。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>Remarks

- 入力した情報にスペースが含まれている場合は、テキストを引用符で囲みます (例、"コンピューター名")。

### <a name="examples"></a>例

ローカルコンピューター上の LPT1 に接続され、color printer Driver1 というプリンタードライバーを必要とする colorprinter_2 という名前のプリンターを追加するには、次のように入力します。

```
cscript prnmngr -a -p colorprinter_2 -m "color printer Driver1" -r lpt1:
```

HRServer という名前のリモートコンピューターから colorprinter_2 という名前のプリンターを削除するには、次のように入力します。

```
cscript prnmngr -d -s HRServer -p colorprinter_2
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [印刷コマンドのリファレンス](print-command-reference.md)
