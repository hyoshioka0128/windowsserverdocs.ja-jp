---
title: pubprn
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 499ff2ade7ffc6c608791ba3da0ede0c3282c13d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831703"
---
# <a name="pubprn"></a>pubprn

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

プリンターを active directory Domain Services に発行します。

## <a name="syntax"></a>構文
```
cscript pubprn {<ServerName> | <UNCprinterpath>} 
"LDAP://CN=<Container>,DC=<Container>"
```

## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|\<サーバー名 >|発行するプリンターをホストしている Windows サーバーの名前を指定します。 コンピューターを指定しないと、ローカル コンピューターが使用されます。|
|\<UNCprinterpath >|共有プリンターを発行する場合に汎用名前付け規則 (UNC) パス。|
|"なります<Container>,、DC =<Container>"|プリンターを発行する active directory ドメイン サービスでは、コンテナーへのパスを指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈
-   **Pubprn**コマンドは、%WINdir%\System32\printing_Admin_Scripts にある Visual Basic スクリプト\\<language>ディレクトリ。 このコマンドでは、コマンド プロンプトで、使用する入力**cscript** pubprn ファイル、または適切なフォルダーにディレクトリを変更する、完全なパスを続けています。 例:
    ```
    cscript %WINdir%\System32\printing_Admin_Scripts\en-US\pubprn
    ```
-   入力する情報にスペースが含まれている場合は、テキストを囲む引用符を使用して (たとえば、 `"computer Name"`)。

## <a name="BKMK_examples"></a>例
上のすべてのプリンターを公開する、 \\MyDomain.company.Com ドメイン内の MyContainer コンテナーに \Server1 コンピューターを入力します。
```
cscript Ppubprn Server1 "LDAP://CN=MyContainer,DC=MyDomain,DC=company,DC=Com"
```
上の Laserprinter1 プリンターを公開する、 \\MyDomain.company.Com ドメインの種類の MyContainer コンテナーに \Server1 サーバー。
```
cscript Ppubprn \\Server1\Laserprinter1 "LDAP://CN=MyContainer,DC=MyDomain,DC=company,DC=Com"
```

#### <a name="additional-references"></a>その他の参照
[コマンドライン構文のポイント](command-line-syntax-key.md)
[印刷コマンドのリファレンス](print-command-reference.md)
