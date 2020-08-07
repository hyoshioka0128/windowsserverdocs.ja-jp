---
title: Scwcmd 分析
description: 参照記事 * * * *-
ms.topic: article
ms.assetid: 0259271b-be5b-48d7-a51d-8b9b6786efb4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 635da8cd31140ea0b1d0cd786e7b16e2ce692bcd
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87883228"
---
# <a name="scwcmd-analyze"></a>Scwcmd: 分析

> 適用対象: Windows Server 2012 R2、Windows Server 2012

コンピューターが、ポリシーに準拠しているかどうかを判断します。 .Xml ファイルには、結果が返されます。 コンピューター名の一覧を入力としても受け取ります。 ブラウザーで結果を表示するには使用 **scwcmd ビュー** 指定 **%windir%\security\msscw\TransformFiles\scwanalysis.xsl** .xsl 変換として。

## <a name="syntax"></a>構文

```
scwcmd analyze [[[/m:<ComputerName> | /ou:<Ou>] /p:<Policy>] | /i:<ComputerList>] [/o:
<ResultDir>] [/u:<UserName>] [/pw:<Password>] [/t:<Threads>] [/l] [/e]
```

#### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/m\<ComputerName>|NetBIOS 名、DNS 名、または分析するコンピューターの IP アドレスを指定します。 場合、 **/m** パラメーターが指定されている、 **/p** パラメーターも指定する必要があります。|
|/ou\<OuName>|Active Directory ドメイン サービスでは、組織単位 (OU) の完全修飾ドメイン名 (FQDN) を指定します。 場合、 **/ou** パラメーターが指定されている、 **/p** パラメーターも指定する必要があります。 OU 内のすべてのコンピューターが特定のポリシーに対して分析されます。|
|/p\<Policy>|分析の実行に使用する .xml ポリシー ファイルのパスとファイル名を指定します。|
|/i\<ComputerList>|予想されるポリシー ファイルと共にコンピューターの一覧を含む .xml ファイルのパスとファイル名を指定します。 .Xml ファイル内のすべてのコンピューターは、対応するポリシー ファイルに対して分析されます。 サンプルの .xml ファイルは、%windir%\security\samplemachinelist.xml です。|
|/o\<ResultDir>|分析結果ファイルの保存先ディレクトリとパスを指定します。 既定値は、現在のディレクトリです。|
|/u\<UserName>|リモート コンピューターで、分析を実行するときに使用する、代替のユーザー資格情報を指定します。 既定値は、ユーザーには、ログオンしています。|
|pw\<Password>|リモート コンピューターで、分析を実行するときに使用する、代替のユーザー資格情報を指定します。 既定値は、ログオン ユーザーのパスワードです。|
|/t: \<Threads>|分析中に保守する必要が優れた分析を同時操作の数を指定します (既定値 = 40、MinValue = 1、最大値 = 1000)。|
|/l|ログに記録する分析処理を行われます。 1 つのログ ファイルが、分析するコンピューターごとに生成されます。 ログ ファイルは、結果のファイルと同じディレクトリに保存されます。 使用して、 **/o** 結果ファイルのディレクトリを指定するにはオプションです。|
|/e|不一致が検出された場合は、アプリケーション イベント ログにイベントを記録します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>Remarks

Scwcmd.exe は Windows Server 2008 R2、Windows Server 2008 または Windows Server 2003 を実行するコンピューターにできるだけです。

## <a name="examples"></a>例

ファイル webpolicy.xml に対してセキュリティ ポリシーを分析するには、次のように入力します。
```
scwcmd analyze /p:webpolicy.xml

```
Webadmin アカウントの資格情報を使用してファイル webpolicy.xml に対して web サーバーをという名前のコンピューターのセキュリティ ポリシーを分析するには、次のように入力します。
```
scwcmd analyze /m:webserver /p:webpolicy.xml /u:webadmin

```
最大 100 個のスレッドを使用して、ファイル webpolicy.xml に対してセキュリティ ポリシーを分析し、結果 resultserver 共有内の結果をという名前のファイルを出力する次のように入力します。
```
scwcmd analyze /i:webpolicy.xml /t:100 /o:\\resultserver\results

```
ファイル webpolicy.xml に対してウェブサーバ OU のセキュリティ ポリシーを DomainAdmin の資格情報を使用して、分析、次のように入力します。
```
scwcmd analyze /ou:OU=WebServers,DC=Marketing,DC=ABCCompany,DC=com /p:webpolicy.xml /u:DomainAdmin
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)