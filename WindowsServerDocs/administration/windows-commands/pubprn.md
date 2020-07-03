---
title: pubprn
description: Pubprn.vbs コマンドの参照記事。プリンターを Active Directory Domain Services に発行します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0bc7f7e3-84e1-4359-b477-7b1a1a0bd639
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c73c79450d4feb4d2567f29bfed56364dea9b5a8
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932014"
---
# <a name="pubprn"></a>pubprn

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

プリンターを Active Directory ドメイン サービスに発行します。 このコマンドは、ディレクトリにある Visual Basic スクリプトです `%WINdir%\System32\printing_Admin_Scripts\<language>` 。 コマンドプロンプトでこのコマンドを使用するには、「 **cscript** 」に続けて pubprn.vbs ファイルの完全なパスを入力するか、ディレクトリを適切なフォルダーに変更します。 例: `cscript %WINdir%\System32\printing_Admin_Scripts\en-US\pubprn`。

## <a name="syntax"></a>構文

```
cscript pubprn {<servername> | <UNCprinterpath>} LDAP://CN=<container>,DC=<container>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
|--|--|
| `<servername>` | 発行するプリンターをホストしている Windows サーバーの名前を指定します。 コンピューターを指定しない場合は、ローカルコンピューターが使用されます。 |
| `<UNCprinterpath>` | 共有プリンターを発行する場合に汎用名前付け規則 (UNC) パス。 |
| `LDAP://CN=<Container>,DC=<Container>` | Active Directory ドメイン サービスが、プリンターを公開するには、コンテナーのパスを指定します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>注釈

- 入力した情報にスペースが含まれている場合は、テキストを引用符で囲みます (例、"コンピューター名")。

### <a name="examples"></a>例

Server1 コンピューター上のすべてのプリンターを \\ MyDomain.company.com ドメイン内の MyContainer コンテナーに発行するには、次のように入力します。

```
cscript pubprn Server1 LDAP://CN=MyContainer,DC=MyDomain,DC=company,DC=Com
```

MyDomain.company.com ドメイン内の MyContainer コンテナーに対して、Laserprinter1 プリンターをサーバー上で発行するには \\ 、次のように入力します。

```
cscript pubprn \\Server1\Laserprinter1 LDAP://CN=MyContainer,DC=MyDomain,DC=company,DC=Com
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [印刷コマンドのリファレンス](print-command-reference.md)
