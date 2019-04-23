---
title: telnet
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b70a6156-9413-4300-84ce-a34c467e2b4e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6439a91d82d6d199666629e333d8130bf65a384b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858563"
---
# <a name="telnet"></a>telnet

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Telnet サーバー サービスを実行しているコンピューターと通信します。 
## <a name="syntax"></a>構文
```
telnet [/a] [/e <EscapeChar>] [/f <FileName>] [/l <UserName>] [/t {vt100 | vt52 | ansi | vtnt}] [<Host> [<Port>]] [/?]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/a|自動ログオンを試行します。 /L オプションと同じ使用を除き、現在ログオンしているユーザーの名前にします。|
|/e \<EscapeChar >|Telnet クライアント プロンプトを入力するために使用する文字をエスケープします。|
|/f \<FileName>|クライアント側のログ記録に使用するファイル名。|
|/l\<ユーザー名 >|リモート コンピューター上でログオンするユーザー名を指定します。|
|/t {vt100 & #124; vt52 & #124; ansi & #124; vtnt}|端末の種類を指定します。 サポートされている種類の端末は、vt52、vt100、ansi、および vtnt です。|
|\<ホスト > [\<ポート >]|ホスト名またはリモートのコンピューターに、接続して、必要に応じて使用する TCP ポートの IP アドレスを指定します (既定では TCP ポート 23)。|
|/?|コマンド プロンプトにヘルプを表示します。 または、/h を入力することができます。|

## <a name="remarks"></a>注釈
-   このコマンドを実行する前に、telnet クライアント ソフトウェアをインストールする必要があります。 詳細については、次を参照してください。 [telnet をインストールする](https://technet.microsoft.com/library/cc754293(v=ws.10).aspx)します。
-   Telnet プロンプトで示される、telnet のコンテキストを入力するパラメーターなしの telnet を実行することができます (**Microsoft telnet >**)。 Telnet プロンプトで、telnet コマンドを使用して telnet クライアントを実行しているコンピューターを管理することができます。

## <a name="BKMK_Examples"></a>例
Telnet を使用して、telnet.microsoft.com で telnet サーバー サービスを実行しているコンピューターに接続します。
```
telnet telnet.microsoft.com
```
Telnet を使用して、TCP ポート 44 上 telnet.microsoft.com で telnet サーバー サービスを実行しているコンピューターに接続し、telnetlog.txt と呼ばれるローカル ファイル内にセッション アクティビティを記録するには
```
telnet /f telnetlog.txt telnet.microsoft.com 44
```

## <a name="additional-references"></a>その他の参照
-   [Telnet をインストールします。](https://technet.microsoft.com/library/cc754293(v=ws.10).aspx)
-   [telnet のテクニカル リファレンス](https://technet.microsoft.com/library/cc754987(v=ws.10).aspx)
-   [コマンドライン構文キー](command-line-syntax-key.md)
