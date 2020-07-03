---
title: prnport
description: Prnport.vbs コマンドの参照記事。ポート構成の表示と変更に加えて、標準の TCP/IP プリンターポートを作成、削除、および一覧表示します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6a0ec638-a21e-4a34-be5c-bd0f7ca89ffe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4b373547050d3d3dfb1d64160959c8dbb9e6f5c5
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931159"
---
# <a name="prnport"></a>prnport

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

作成、削除、および表示して、ポート構成を変更するだけでなく、標準の TCP/IP プリンター ポートを一覧表示します。 このコマンドは、ディレクトリにある Visual Basic スクリプトです `%WINdir%\System32\printing_Admin_Scripts\<language>` 。 コマンドプロンプトでこのコマンドを使用するには、「 **cscript** 」に続けて prnport.vbs ファイルの完全なパスを入力するか、ディレクトリを適切なフォルダーに変更します。 例: `cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prnport`。

## <a name="syntax"></a>構文

```
cscript prnport {-a | -d | -l | -g | -t | -?} [-r <portname>] [-s <Servername>] [-u <Username>] [-w <password>] [-o {raw | lpr}] [-h <Hostaddress>] [-q <Queuename>] [-n <portnumber>] -m{e | d} [-i <SNMPindex>] [-y <communityname>] -2{e | -d}
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
|--|--|
| -a | 標準 TCP/IP プリンタ ポートを作成します。 |
| -d | 標準 TCP/IP プリンタ ポートを削除します。 |
| -l | **-S**パラメーターによって指定されたコンピューター上のすべての標準 tcp/ip プリンターポートを一覧表示します。 |
| -g | 標準 TCP/IP プリンタ ポートの構成を表示します。 |
| -t | 標準 TCP/IP プリンタ ポートのポートの設定を構成します。 |
| -r`<portname>` | プリンターが接続されているポートを指定します。 |
| -s`<Servername>` | 管理するプリンターをホストするリモート コンピューターの名前を指定します。 コンピューターを指定しない場合は、ローカルコンピューターが使用されます。 |
| -u `<Username>` -w`<password>` | 管理するプリンターをホストするコンピューターに接続するアクセス許可を持つアカウントを指定します。 ターゲット コンピューターのローカル Administrators グループのすべてのメンバーはこれらのアクセス許可を持っていますが、アクセス許可を他のユーザーに与えることもできます。 アカウントを指定しない場合は、コマンドが機能するように、これらのアクセス許可を持つアカウントでログオンする必要があります。 |
| -o`{raw|lpr}` | ポートが使用するプロトコル (TCP raw または TCP lpr) を指定します。 TCP raw プロトコルは、lpr プロトコルよりも Windows での高パフォーマンスプロトコルです。 使用してポート番号を必要に応じて指定生 TCP を使用する場合、 **-n** パラメーター。 既定のポート番号は 9100 です。 |
| -h`<Hostaddress>` | ポートを構成するプリンターを (IP アドレス) を指定します。 |
| -q`<Queuename>` | 生の TCP ポートのキュー名を指定します。 |
| -n`<portnumber>` | 生の TCP ポートのポート番号を指定します。 既定のポート番号は 9100 です。 |
| -m`{e|d}` | SNMP が有効になっているかどうかを指定します。 パラメーター **e** SNMP を使用します。 パラメーター **d** SNMP を無効にします。 |
| -i`<SNMPindex` | SNMP が有効になっている場合は、SNMP インデックスを指定します。 詳細については、 [rfc editor web サイト](https://www.ietf.org/rfc/rfc1759.txt?number=1759)の**rfc 1759**を参照してください。 |
| -y`<communityname>` | SNMP が有効になっている場合は、SNMP コミュニティ名を指定します。 |
| -2`{e|-d}` | TCP lpr ポートに対して、二重スプール (respooling とも呼ばれます) を有効にするかどうかを指定します。 TCP lpr は、プリンターに送信されるコントロールファイルに正確なバイト数を含める必要がありますが、プロトコルはローカルの印刷プロバイダーからカウントを取得できないため、二重スプールが必要です。 このため、ファイルが TCP lpr 印刷キューにスプールされると、ファイルは system32 ディレクトリ内の一時ファイルとしてもスプールされます。 TCP lpr は、一時ファイルのサイズを決定し、そのサイズを LPD を実行しているサーバーに送信します。 パラメーター **e** 二重スプールを使用します。 パラメーター **d** 二重スプールを無効にします。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>注釈

- 入力した情報にスペースが含まれている場合は、テキストを引用符で囲みます (例、"コンピューター名")。

### <a name="examples"></a>例

サーバー Server1 のすべての標準 TCP/IP 印刷ポートを表示するには \\ 、次のように入力します。

```
cscript prnport -l -s Server1
```

\Server1 10.2.3.4 のネットワークプリンターに接続するサーバー Server1 の標準 TCP/IP 印刷ポートを削除するには \\ 、次のように入力します。

```
cscript prnport -d -s Server1 -r IP_10.2.3.4
```

\\\Server1 10.2.3.4 のネットワークプリンターに接続し、ポート9100で tcp raw プロトコルを使用する、標準の tcp/ip 印刷ポートをサーバー Server1 に追加するには、次のように入力します。

```
cscript prnport -a -s Server1 -r IP_10.2.3.4 -h 10.2.3.4 -o raw -n 9100
```

SNMP を有効にするには、"public" というコミュニティ名を指定し、サーバー Server1 で共有されている \server1 10.2.3.4 のネットワークプリンターで SNMP インデックスを1に設定し \\ ます。次のように入力します。

```
cscript prnport -t -s Server1 -r IP_10.2.3.4 -me -y public -i 1 -n 9100
```

10.2.3.4 にネットワーク プリンターに接続し、プリンターからデバイスの設定を自動的に取得するローカル コンピューター上の標準の TCP/IP 印刷ポートを追加するに次のように入力します。

```
cscript prnport -a -r IP_10.2.3.4 -h 10.2.3.4
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [印刷コマンドのリファレンス](print-command-reference.md)
