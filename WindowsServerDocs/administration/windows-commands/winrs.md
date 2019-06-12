---
title: winrs
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c370de31-5651-400a-872d-ef229aae2309
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f9c612a7c6f5d0935223b3c193c52fe970c970d7
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440056"
---
# <a name="winrs"></a>winrs

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows リモート管理を使用すると、管理し、プログラムをリモートで実行できます。   
## <a name="syntax"></a>構文  
```  
winrs [/<parameter>[:<value>]] <command>  
```  
### <a name="parameters"></a>パラメーター  

|           パラメーター            |                                                                                                                                                                                    説明                                                                                                                                                                                     |
|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      /remote:\<endpoint>       |                                                                                          NetBIOS 名または標準の接続を使用して、ターゲット エンドポイントを指定します。<br /><br />-   <url>: [\<トランスポート >://]\<ターゲット > [:\<ポート >]<br /><br />指定しない場合、 **/r:localhost**使用されます。                                                                                          |
|          暗号化されていない/          | リモート シェルにメッセージは暗号化されませんを指定します。 これはトラブルシューティングや、ネットワーク トラフィックが暗号化を使用して既にときに役立ちます。 **ipsec**、物理的なセキュリティを適用するタイミングまたはします。<br /><br />既定では、Kerberos または NTLM のキーを使用して、メッセージが暗号化されます。<br /><br />このコマンド ライン オプションには、HTTPS トランスポートを選択した場合は無視されます。 |
|     /username:\<username>      |                                                                                コマンドラインでユーザー名を指定します。<br /><br />指定しない場合、ツールは、名前のネゴシエート認証またはプロンプトが使用されます。<br /><br />場合 **/username**が指定されている **/password**も指定する必要があります。                                                                                 |
|     /password:\<password>      |                                                                           コマンドラインでパスワードを指定します。<br /><br />場合 **/password**が指定されていませんが、 **/username**は、ツールでは、パスワードが求められます。<br /><br />場合 **/password**が指定されている **/username**も指定する必要があります。                                                                            |
|      /timeout:\<seconds>       |                                                                                                                                                                             このオプションは非推奨とされます。                                                                                                                                                                             |
|       /directory:\<path>       |                                                                                            リモート シェルを開始するディレクトリを指定します。<br /><br />リモート シェルは、環境変数で定義されているユーザーのホーム ディレクトリで開始されている指定しない場合、 **%userprofile%** します。                                                                                             |
| /environment:\<文字列 > =<value> |                                                                          シェルのシェルを起動する既定の環境の変更を許可する場合に設定される 1 つの環境変数を指定します。<br /><br />このスイッチの複数の発生は、複数の環境変数を指定するために使用する必要があります。                                                                          |
|            /noecho             |                                                                                                    そのエコーを無効にする必要がありますを指定します。 リモート画面の指示をユーザーの答がローカルに表示されないことを確認するために必要な場合があります。<br /><br />既定では、エコーが"on"です。                                                                                                    |
|           /noprofile           |                                              ユーザーのプロファイルを読み込まれていないことを指定します。<br /><br />既定では、サーバーはユーザー プロファイルの読み込みを試みます。<br /><br />リモート ユーザーが、ターゲット システムにローカル管理者ではないかどうかは、このオプションが必要になります (既定値をエラーになります)。                                               |
|         /allowdelegate         |                                                                                                                  ユーザーの資格情報使用できることなど、リモート共有にアクセスするターゲット エンドポイントとは別のコンピューターで検出されたを指定します。                                                                                                                   |
|          /compression          |                                                                           圧縮を有効にします。  リモート コンピューター上の古いインストールできるように既定でオフになります圧縮はサポート可能性があります。<br /><br />リモート マシン上の以前のインストールが圧縮をサポートしていないために、既定の設定がオフです。                                                                           |
|            /usessl             |                                                                                                               リモート エンドポイントを使用する場合は、SSL 接続を使用します。  これを指定するトランスポートではなく**https:** 既定値を使用**WinRM**既定のポート。                                                                                                                |
|               /?               |                                                                                                                                                                        コマンド プロンプトにヘルプを表示します。                                                                                                                                                                        |

## <a name="remarks"></a>注釈  
-   すべてのコマンド ライン オプションには、長い形式または短い形式のいずれかがそのまま使用します。 たとえば、両方 **/r**と **/リモート**は有効です。  
-   終了する、 **/リモート**コマンドをユーザーが入力できる**Ctrl + C**または**ctrl + break**、これは、リモート シェルに送信されます。 2 番目の**Ctrl + C**は強制終了**winrs.exe**します。  
-   アクティブなリモート シェルまたは winrs 構成を管理するには、WinRM のツールを使用します。  URI をアクティブなシェルを管理するエイリアスは**cmdシェル/** します。  エイリアス winrs 構成の URI は**winrm/構成/winrs**します。  

## <a name="BKMK_Examples"></a>例  
```  
winrs /r:https://contoso.com command  
```  
```  
winrs /r:contoso.com /usessl command  
```  
```  
winrs /r:myserver command  
```  
```  
winrs /r:http://127.0.0.1 command  
```  
```  
winrs /r:http://169.51.2.101:80 /unencrypted command  
```  
```  
winrs /r:https://[::FFFF:129.144.52.38] command  
```  
```  
winrs /r:http://[1080:0:0:0:8:800:200C:417A]:80 command  
```  
```  
winrs /r:https://contoso.com /t:600 /u:administrator /p:$%fgh7 ipconfig  
```  
```  
winrs /r:myserver /env:path=^%path^%;c:\tools /env:TEMP=d:\temp config.cmd  
```  
```  
winrs /r:myserver netdom join myserver /domain:testdomain /userd:johns /passwordd:$%fgh789  
```  
```  
winrs /r:myserver /ad /u:administrator /p:$%fgh7 dir \\anotherserver\share  
```  

## <a name="additional-references"></a>その他の参照情報  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  

