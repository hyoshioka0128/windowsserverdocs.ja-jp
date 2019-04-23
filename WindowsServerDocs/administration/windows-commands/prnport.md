---
title: prnport
description: 作成、削除、およびプリンター ポートを一覧表示する方法について説明します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6a0ec638-a21e-4a34-be5c-bd0f7ca89ffe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: eb6ef7632c10217c4fdf114d4e67c8bc52be07e2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856893"
---
# <a name="prnport"></a>prnport

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

作成、削除、および表示して、ポート構成を変更するだけでなく、標準の TCP/IP プリンター ポートを一覧表示します。

## <a name="syntax"></a>構文
```
cscript prnport {-a | -d | -l | -g | -t | -?} [-r <PortName>] 
[-s <ServerName>] [-u <UserName>] [-w <Password>] [-o {raw | lpr}] 
[-h <Hostaddress>] [-q <QueueName>] [-n <PortNumber>] -m{e | d} 
[-i <SNMPIndex>] [-y <CommunityName>] -2{e | -d}
```

## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|-a|標準 TCP/IP プリンタ ポートを作成します。|
|-d|標準 TCP/IP プリンタ ポートを削除します。|
|-l|すべての標準 TCP/IP プリンタ ポートを指定したコンピューターを一覧表示、 **-s**パラメーター。|
|-g|標準 TCP/IP プリンタ ポートの構成を表示します。|
|-t|標準 TCP/IP プリンタ ポートのポートの設定を構成します。|
|-r \<PortName>|プリンターが接続されているポートを指定します。|
|-s \<ServerName>|管理するプリンターをホストするリモート コンピューターの名前を指定します。 コンピューターを指定しないと、ローカル コンピューターが使用されます。|
|-u \<UserName> -w <Password>|管理するプリンターをホストするコンピューターに接続するアクセス許可を持つアカウントを指定します。 ターゲット コンピューターのローカル Administrators グループのすべてのメンバーにこれらのアクセス許可があるが、アクセス許可は、他のユーザーに与えることもできます。 アカウントを指定しない場合は、コマンドを実行するこれらのアクセス許可を持つアカウントでログオンする必要があります。|
|-o {raw & #124; lpr}|ポート使用するプロトコルを指定します。生の TCP または TCP lpr します。 使用してポート番号を必要に応じて指定生 TCP を使用する場合、 **-n** パラメーター。 既定のポート番号は 9100 です。|
|-h \<Hostaddress>|ポートを構成するプリンターを (IP アドレス) を指定します。|
|-q \<QueueName>|生の TCP ポートのキュー名を指定します。|
|-n \<PortNumber>|生の TCP ポートのポート番号を指定します。 既定のポート番号は 9100 です。|
|-m {& #124; d}|SNMP が有効になっているかどうかを指定します。 パラメーター **e** SNMP を使用します。 パラメーター **d** SNMP を無効にします。|
|-i \<SNMPIndex|SNMP が有効になっている場合は、SNMP インデックスを指定します。 詳細についてでの Rfc 1759 を参照してください、 [Rfc editor の Web サイト](https://go.microsoft.com/fwlink/?LinkId=569)します。|
|-y \<CommunityName>|SNMP が有効になっている場合は、SNMP コミュニティ名を指定します。|
|-2 {& #124; d}|(再スプールとも呼ばれます)、二重スプールが TCP lpr ポートに対して有効かどうかを指定します。 二重スプールは必要なため、TCP lpr は、プリンターに送信される、コントロール ファイルで、正確なバイト数を含める必要がありますが、プロトコルは、ローカルの印刷プロバイダーからカウントを取得できません。 したがって、ファイルがスプールされたときに、tcp lpr 印刷キュー、system32 ディレクトリに一時ファイルとしてもスプールされます。 TCP lpr は、一時ファイルのサイズを決定し、サイズを LPD を実行しているサーバーに送信します。 パラメーター **e** 二重スプールを使用します。 パラメーター **d** 二重スプールを無効にします。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈
-   **Prnport**コマンドは、%WINdir%\System32\printing_Admin_Scripts にある Visual Basic スクリプト\\<language>ディレクトリ。 このコマンドでは、コマンド プロンプトで、使用する入力**cscript** prnport ファイル、または適切なフォルダーにディレクトリを変更する、完全なパスを続けています。 例:
    ```
    cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prnport
    ```
-   入力する情報にスペースが含まれている場合は、テキストを囲む引用符を使用して (たとえば、 `"computer Name"`)。
-   TCP raw プロトコルは、lpr プロトコルよりも Windows で高いパフォーマンス プロトコルです。

## <a name="BKMK_examples"></a>例
サーバー上のすべての標準の TCP/IP 印刷ポートを表示する \\\Server1 を入力します。
```
cscript prnport -l -s Server1
```
サーバー上の標準の TCP/IP 印刷ポートを削除する \\\Server1 10.2.3.4 型で、ネットワーク プリンターに接続します。
```
cscript prnport -d -s Server1 -r IP_10.2.3.4
```
サーバーで、標準の TCP/IP 印刷ポートを追加する \\\Server1 10.2.3.4 にネットワーク プリンターに接続し、ポート 9100 型で TCP raw プロトコルを使用します。
```
cscript prnport -a -s Server1 -r IP_10.2.3.4 -h 10.2.3.4 -o raw -n 9100
```
SNMP を有効にするには、「パブリック」コミュニティ名を指定し、サーバーで共有される 10.2.3.4 にネットワーク プリンターの SNMP インデックスを 1 に設定 \\\Server1 を入力します。
```
cscript prnport -t -s Server1 -r IP_10.2.3.4 -me -y public -i 1 -n 9100
```
10.2.3.4 にネットワーク プリンターに接続し、プリンターからデバイスの設定を自動的に取得するローカル コンピューター上の標準の TCP/IP 印刷ポートを追加するに次のように入力します。
```
cscript prnport -a -r IP_10.2.3.4 -h 10.2.3.4
```

#### <a name="additional-references"></a>その他の参照
[コマンドライン構文のポイント](command-line-syntax-key.md)
[印刷コマンドのリファレンス](print-command-reference.md)
