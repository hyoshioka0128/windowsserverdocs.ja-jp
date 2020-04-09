---
title: winrs
description: プログラムをリモートで管理および実行できるようにする winrs の Windows コマンドに関するトピック。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c370de31-5651-400a-872d-ef229aae2309
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d3b714f851c981611bbe4d4f26a7b7eed2db7903
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80829145"
---
# <a name="winrs"></a>winrs

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows リモート管理を使用すると、プログラムをリモートで管理および実行できます。   
## <a name="syntax"></a>構文  
```  
winrs [/<parameter>[:<value>]] <command>  
```  
#### <a name="parameters"></a>パラメーター  

|           パラメーター            |                                                                                                                                                                                    説明                                                                                                                                                                                     |
|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      /\<エンドポイント >       |                                                                                          NetBIOS 名または標準接続を使用してターゲットエンドポイントを指定します。<p>-   <url>: [\<transport >:/]\<ターゲット > [:\<ポート >]<p>指定しない場合、 **/r: localhost**が使用されます。                                                                                          |
|          /非暗号化          | リモートシェルへのメッセージが暗号化されないことを指定します。 これは、トラブルシューティングや、 **ipsec**を使用してネットワークトラフィックが既に暗号化されている場合、または物理的なセキュリティが適用されている場合に便利です。<p>既定では、メッセージは Kerberos または NTLM キーを使用して暗号化されます。<p>このコマンドラインオプションは、HTTPS トランスポートが選択されている場合は無視されます。 |
|     /username:\<ユーザー名 >      |                                                                                コマンドラインのユーザー名を指定します。<p>指定しない場合、ツールはネゴシエート認証または名前のプロンプトを使用します。<p>場合 **/username**が指定されている場合、 **/password**も指定する必要があります。                                                                                 |
|     /password:\<パスワード >      |                                                                           コマンドラインのパスワードを指定します。<p>**/password**が指定されておらず、 **/username**がの場合、ツールはパスワードの入力を求めます。<p>**/password**を指定する場合は、 **/username**も指定する必要があります。                                                                            |
|      /timeout:\<seconds >       |                                                                                                                                                                             このオプションは非推奨とされます。                                                                                                                                                                             |
|       /ディレクトリ:\<パス >       |                                                                                            リモートシェルの開始ディレクトリを指定します。<p>指定しない場合、リモートシェルは、環境変数 **% USERPROFILE%** によって定義されたユーザーのホームディレクトリで開始されます。                                                                                             |
| /環境:\<文字列 > =<value> |                                                                          シェルの起動時に設定される単一の環境変数を指定します。これにより、シェルの既定の環境を変更できます。<p>複数の環境変数を指定するには、このスイッチを複数回使用する必要があります。                                                                          |
|            /noecho             |                                                                                                    Echo を無効にすることを指定します。 これは、リモートプロンプトに対するユーザーの回答がローカルに表示されないようにするために必要な場合があります。<p>既定では、echo はオンになっています。                                                                                                    |
|           /noprofile           |                                              ユーザーのプロファイルを読み込まないことを指定します。<p>既定では、サーバーはユーザープロファイルの読み込みを試みます。<p>リモートユーザーがターゲットシステムのローカル管理者でない場合は、このオプションが必要になります (既定ではエラーが発生します)。                                               |
|         /allowdelegate         |                                                                                                                  リモート共有にアクセスするためにユーザーの資格情報を使用できることを指定します。たとえば、ターゲットエンドポイントとは異なるコンピューター上に存在します。                                                                                                                   |
|          /compression          |                                                                           圧縮を有効にします。  リモートコンピューター上の古いインストールでは、圧縮がサポートされていないため、既定でオフになっています。<p>リモートコンピューター上の古いインストールでは圧縮がサポートされないため、既定の設定はオフになっています。                                                                           |
|            /usessl             |                                                                                                               リモートエンドポイントを使用する場合は、SSL 接続を使用します。  トランスポート**https**の代わりにこの値を指定すると、既定の**WinRM**既定ポートが使用されます。                                                                                                                |
|               /?               |                                                                                                                                                                        コマンド プロンプトでヘルプを表示します。                                                                                                                                                                        |

## <a name="remarks"></a>コメント  
-   すべてのコマンドラインオプションでは、短い形式または長い形式のいずれかを使用できます。 たとえば、 **/r**と//は両方**とも有効**です。  
-   このコマンドを終了するには、ユーザーが**Ctrl + C**キーまたは**Ctrl + break キー**を押して、リモートシェルに**送信します**。 2番目の**Ctrl + C キー**を押すと、 **winrs.exe**が強制的に終了します。  
-   アクティブなリモートシェルまたは winrs 構成を管理するには、WinRM ツールを使用します。  アクティブシェルを管理するための URI エイリアスは、 **shell/cmd**です。  Winrs 構成の URI エイリアスは、 **winrm/config/winrs**です。  

## <a name="examples"></a><a name=BKMK_Examples></a>例  
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
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  

