---
title: pubprn
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0bc7f7e3-84e1-4359-b477-7b1a1a0bd639
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 844a13c1a650ebedcc0d5b4fbf65b9de671b2180
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372013"
---
# <a name="pubprn"></a>pubprn

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

プリンターを active directory ドメインサービスに発行します。

## <a name="syntax"></a>構文
```
cscript pubprn {<ServerName> | <UNCprinterpath>} 
"LDAP://CN=<Container>,DC=<Container>"
```

## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|\<ServerName >|発行するプリンターをホストしている Windows サーバーの名前を指定します。 コンピューターを指定しないと、ローカル コンピューターが使用されます。|
|\< 番目のプリンターパス >|共有プリンターを発行する場合に汎用名前付け規則 (UNC) パス。|
|"なります<Container>,、DC =<Container>"|プリンターを公開する active directory ドメインサービス内のコンテナーへのパスを指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>コメント
-   **Pubprn.vbs**コマンドは、%WINdir%\System32\printing_Admin_Scripts @ no__t @ no__t ディレクトリにある Visual Basic スクリプトです。 このコマンドを使用するには、コマンドプロンプトで「 **cscript** 」と入力し、pubprn.vbs ファイルへの完全なパスを入力するか、ディレクトリを適切なフォルダーに変更します。 以下に例を示します。
    ```
    cscript %WINdir%\System32\printing_Admin_Scripts\en-US\pubprn
    ```
-   入力した情報にスペースが含まれている場合は、テキストを引用符で囲みます (たとえば、`"computer Name"`)。

## <a name="BKMK_examples"></a>例
@No__t 0 から Server1 コンピューター上のすべてのプリンターを、MyDomain.company.Com ドメインの MyContainer コンテナーに発行するには、次のように入力します。
```
cscript Ppubprn Server1 "LDAP://CN=MyContainer,DC=MyDomain,DC=company,DC=Com"
```
@No__t 0 の Server1 サーバーにある Laserprinter1 プリンターを MyDomain.company.Com ドメインの MyContainer コンテナーに発行するには、次のように入力します。
```
cscript Ppubprn \\Server1\Laserprinter1 "LDAP://CN=MyContainer,DC=MyDomain,DC=company,DC=Com"
```

#### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文のキー](command-line-syntax-key.md)
[印刷コマンドリファレンス](print-command-reference.md)
