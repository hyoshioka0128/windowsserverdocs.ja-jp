---
title: telnet
description: Telnet サーバーサービスを実行しているコンピューターと通信する telnet のリファレンス記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b70a6156-9413-4300-84ce-a34c467e2b4e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 70c4eb44a654094410432dd9d37d0ad0082f5874
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86958814"
---
# <a name="telnet"></a>telnet

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Telnet サーバーサービスを実行しているコンピューターと通信します。

## <a name="syntax"></a>構文
```
telnet [/a] [/e <EscapeChar>] [/f <FileName>] [/l <UserName>] [/t {vt100 | vt52 | ansi | vtnt}] [<Host> [<Port>]] [/?]
```
#### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/a|自動ログオンを試行します。 [/L] オプションと同じですが、現在ログオンしているユーザーの名前が使用されます。|
|/e\<EscapeChar>|Telnet クライアントプロンプトを入力するために使用されるエスケープ文字。|
|/f \<FileName>|クライアント側のログ記録に使用するファイル名。|
|/l\<UserName>|リモート コンピューター上でログオンするユーザー名を指定します。|
|/t {vt100 & #124; vt52 & #124; ansi & #124; vtnt}|端末の種類を指定します。 サポートされている種類の端末は、vt52、vt100、ansi、および vtnt です。|
|\<Host> [\<Port>]|ホスト名またはリモートのコンピューターに、接続して、必要に応じて使用する TCP ポートの IP アドレスを指定します (既定では TCP ポート 23)。|
|/?|コマンド プロンプトにヘルプを表示します。 または、/h を入力することができます。|

## <a name="remarks"></a>注釈
-   このコマンドを実行する前に、telnet クライアントソフトウェアをインストールする必要があります。 詳細については、「 [telnet のインストール](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754293(v=ws.10))」を参照してください。
-   Telnet プロンプト (**Microsoft telnet>**) によって示される telnet コンテキストを入力するために、パラメーターを指定せずに telnet を実行できます。 Telnet プロンプトから telnet コマンドを使用して、telnet クライアントを実行しているコンピューターを管理できます。

## <a name="examples"></a>例
Telnet を使用して、telnet.microsoft.com で telnet サーバーサービスを実行しているコンピューターに接続します。
```
telnet telnet.microsoft.com
```
Telnet を使用して、TCP ポート44の telnet.microsoft.com で telnet サーバーサービスを実行しているコンピューターに接続し、という名前のローカルファイルにセッションアクティビティを記録し telnetlog.txt
```
telnet /f telnetlog.txt telnet.microsoft.com 44
```

## <a name="additional-references"></a>その他のリファレンス
-   [Telnet をインストールする](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754293(v=ws.10))
-   [telnet のテクニカルリファレンス](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754987(v=ws.10))
- [コマンド ライン構文の記号](command-line-syntax-key.md)
