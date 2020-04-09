---
title: pubprn
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0bc7f7e3-84e1-4359-b477-7b1a1a0bd639
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8696a372902f36f703670cf514bddf75cf4cc7e3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80837105"
---
# <a name="pubprn"></a>pubprn

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

プリンターを active directory ドメインサービスに発行します。

## <a name="syntax"></a>構文
```
cscript pubprn {<ServerName> | <UNCprinterpath>} 
LDAP://CN=<Container>,DC=<Container>
```

### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|\<ServerName >|発行するプリンターをホストしている Windows サーバーの名前を指定します。 コンピューターを指定しないと、ローカル コンピューターが使用されます。|
|\<出てくるプリンターパス >|共有プリンターを発行する場合に汎用名前付け規則 (UNC) パス。|
|LDAP://CN =<Container>、DC =<Container>|プリンターを公開する active directory ドメインサービス内のコンテナーへのパスを指定します。|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="remarks"></a>コメント
-   **Pubprn.vbs**コマンドは、%windir%\system32\ printing_Admin_Scripts\\<language> ディレクトリにある Visual Basic スクリプトです。 このコマンドを使用するには、コマンドプロンプトで「 **cscript** 」と入力し、pubprn.vbs ファイルへの完全なパスを入力するか、ディレクトリを適切なフォルダーに変更します。 例 :
    ```
    cscript %WINdir%\System32\printing_Admin_Scripts\en-US\pubprn
    ```
-   入力した情報にスペースが含まれている場合は、テキストを引用符で囲みます (`computer Name`など)。

## <a name="examples"></a><a name=BKMK_examples></a>例
\\Server1 コンピューター上のすべてのプリンターを MyDomain.company.Com ドメイン内の MyContainer コンテナーに発行するには、次のように入力します。
```
cscript Ppubprn Server1 LDAP://CN=MyContainer,DC=MyDomain,DC=company,DC=Com
```
\\サーバー上の Laserprinter1 プリンターを MyDomain.company.Com ドメインの MyContainer コンテナーに発行するには、次のように入力します。
```
cscript Ppubprn \\Server1\Laserprinter1 LDAP://CN=MyContainer,DC=MyDomain,DC=company,DC=Com
```

## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のキー](command-line-syntax-key.md)
[印刷コマンドリファレンス](print-command-reference.md)
