---
title: netsh
description: Netsh コマンドのリファレンス記事。これは、現在実行中のコンピューターのネットワーク構成をローカルまたはリモートで表示または変更できるコマンドラインスクリプトユーティリティです。
ms.topic: article
ms.assetid: 96fc069d-53c0-4d0a-9f7f-f9f3d49a02bd carmonmills
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 366c7a21f44dc6545de7ba81cba8fe152c245b6b
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87886035"
---
# <a name="netsh"></a>netsh

> 適用先:Windows Server (半期チャネル)、Windows Server 2016

ネットワークシェルコマンドラインスクリプトユーティリティ。このユーティリティを使用すると、現在実行しているコンピューターのネットワーク構成をローカルまたはリモートで表示または変更できます。 このユーティリティは、コマンドプロンプトまたは Windows PowerShell で開始できます。

## <a name="syntax"></a>構文

```
netsh [-a <Aliasfile>][-c <Context>][-r <Remotecomputer>][-u [<domainname>\<username>][-p <Password> | [{<NetshCommand> | -f <scriptfile>}]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| -a `<Aliasfile>` | エイリアスファイルを実行した後に netsh プロンプトに戻り、1つまたは複数の netsh コマンドを含むテキストファイルの名前を返すことを指定します。 |
| -c`<Context>` | Netsh が指定した netsh コンテキストと、入力する netsh コンテキストを入力するように指定します。 |
| -r`<Remotecomputer>` | 構成するリモートコンピューターを指定します。<p>**重要:** このパラメーターを使用する場合は、リモートレジストリサービスがリモートコンピューターで実行されていることを確認する必要があります。 実行されていない場合は、"ネットワークパスが見つかりません" というエラーメッセージが表示されます。 |
| -u`<domainname>\<username>` | ユーザーアカウントで netsh コマンドを実行しているときに使用するドメインとユーザーアカウント名を指定します。 ドメインを省略した場合、既定ではローカルドメインが使用されます。 |
| -p`<Password>` | パラメーターで指定したユーザーアカウントのパスワードを指定し `-u <username>` ます。 |
| `<NetshCommand>` | 実行する netsh コマンドを指定します。 |
| -f`<scriptfile>` | 指定したスクリプトファイルを実行した後に netsh コマンドを終了します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>Remarks

- **-R**の後に別のコマンドを指定すると、netsh によってリモートコンピューターでコマンドが実行され、Cmd.exe コマンドプロンプトに戻ります。 別のコマンドを指定せず**に-r**を指定すると、netsh がリモートモードで開きます。 このプロセスは **set machine** を netsh コマンド プロンプトで使用するのと似ています。 **-R**を使用する場合は、netsh の現在のインスタンスに対してのみターゲットコンピューターを設定します。 netsh を終了して再入力すると、ターゲット コンピューターがローカル コンピューターとして再設定されます。 WINS に格納されているコンピューター名、UNC 名、DNS サーバーによって解決されるインターネット名、または IP アドレスを指定することにより、リモート コンピューター上で netsh コマンドを実行できます。

- 文字列値に文字間のスペースが含まれている場合は、文字列値を引用符で囲む必要があります。 たとえば、`-r "contoso remote device"` のように指定します。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
