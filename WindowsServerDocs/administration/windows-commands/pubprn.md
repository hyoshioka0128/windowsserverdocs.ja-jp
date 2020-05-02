---
title: pubprn
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0bc7f7e3-84e1-4359-b477-7b1a1a0bd639
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 17ca9e98ef9e3423521b03c5c21be4b3f1538b62
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722778"
---
# <a name="pubprn"></a>pubprn

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

プリンターを active directory ドメインサービスに発行します。

## <a name="syntax"></a>構文
```
cscript pubprn {<ServerName> | <UNCprinterpath>} 
LDAP://CN=<Container>,DC=<Container>
```

### <a name="parameters"></a>パラメーター
|パラメーター|[説明]|
|-------|--------|
|\<ServerName>|発行するプリンターをホストしている Windows サーバーの名前を指定します。 コンピューターを指定しないと、ローカル コンピューターが使用されます。|
|\<> していないプリンターパス|共有プリンターを発行する場合に汎用名前付け規則 (UNC) パス。|
|LDAP://CN =<Container>、DC =<Container>|プリンターを公開する active directory ドメインサービス内のコンテナーへのパスを指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>Remarks
-   **Pubprn.vbs**コマンドは、%windir%\system32\ printing_Admin_Scripts\\ <language>ディレクトリにある Visual Basic スクリプトです。 このコマンドを使用するには、コマンドプロンプトで「 **cscript** 」と入力し、pubprn.vbs ファイルへの完全なパスを入力するか、ディレクトリを適切なフォルダーに変更します。 次に例を示します。
    ```
    cscript %WINdir%\System32\printing_Admin_Scripts\en-US\pubprn
    ```
-   入力した情報にスペースが含まれている場合は、テキストを引用符で囲み`computer Name`ます (たとえば、)。

## <a name="examples"></a>例
MyDomain.company.Com ドメイン内の MyContainer \\コンテナーに、Server1 コンピューター上のすべてのプリンターを発行するには、次のように入力します。
```
cscript Ppubprn Server1 LDAP://CN=MyContainer,DC=MyDomain,DC=company,DC=Com
```
MyDomain.company.Com ドメイン内の MyContainer コンテナー \\に対して、Laserprinter1 プリンターをサーバー上で発行するには、次のように入力します。
```
cscript Ppubprn \\Server1\Laserprinter1 LDAP://CN=MyContainer,DC=MyDomain,DC=company,DC=Com
```

## <a name="additional-references"></a>その他のリファレンス
- [コマンドライン構文キー](command-line-syntax-key.md)
[印刷コマンドのリファレンス](print-command-reference.md)
