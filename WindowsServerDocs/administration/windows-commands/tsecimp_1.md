---
title: tsecimp
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d7488ec6-0eff-45ff-89ee-9cbe752416bf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 38582706dfa5db2b5069415b81dafc533c8a89b9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822103"
---
# <a name="tsecimp"></a>tsecimp



TAPI サーバー セキュリティ ファイル (Tsec.ini) に、拡張マークアップ言語 (XML) ファイルからの割り当てに関する情報をインポートします。 TAPI プロバイダーの一覧を表示する次のコマンドを使用することもできにし、各回線デバイスが関連付けられている、内容をインポートせずに XML ファイルの構造を検証、およびドメイン メンバーシップを確認します。

## <a name="syntax"></a>構文

```
tsecimp /f <Filename> [{/v | /u}]
tsecimp /d
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/f\<ファイル名 >|必須。 インポートする割り当て情報を含む XML ファイルの名前を指定します。|
|/v|Tsec.ini ファイルに情報をインポートせず、XML ファイルの構造を検証します。|
|/u|各ユーザーが XML ファイルで指定されたドメインのメンバーであるかどうかを確認します。 このパラメーターを使用するコンピューターは、ネットワークに接続する必要があります。 このパラメーターでは、大量のユーザーの割り当てに関する情報を処理する場合、パフォーマンスが大幅に低下します。|
|/d|インストールされているテレフォニー プロバイダーの一覧が表示されます。 テレフォニー プロバイダーごとに、関連付けられた回線デバイスと、アドレスと各回線デバイスに関連付けられているユーザーは表示します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

-   割り当て情報をインポートする XML ファイルは、以下に示す構造に従う必要があります。  
    -   **UserList**要素

        **UserList**は XML ファイルの最上位要素です。
    -   **ユーザー**要素

        各**ユーザー**要素には、ドメインのメンバーであるユーザーに関する情報が含まれています。 各ユーザーには、1 つまたは複数の回線デバイスを割り当てることがあります。

        さらに、各**ユーザー**という名前の属性が要素**NoMerge**します。 この属性を指定すると、新規に作成する前に、現在のすべての行デバイス割り当てが、ユーザーは削除されます。 この属性を使用すると、簡単に不要なユーザーの割り当てを削除します。 既定では、この属性は設定されません。

        **ユーザー**要素は、1 つを含める必要があります**DomainUserName**要素で、ユーザーのドメインとユーザー名を指定します。 **ユーザー**要素では 1 つ含めることがありますも**FriendlyName**要素で、ユーザーのフレンドリ名を指定します。

        **ユーザー**要素は、1 つを含めることが**LineList**要素。 場合、 **LineList**要素が存在しない、このユーザーのすべての回線デバイスが削除されます。
    -   **LineList**要素

        **LineList**要素には、それぞれの行またはユーザーに割り当てられる可能性がデバイスに関する情報が含まれています。 各**LineList**要素は 1 つ以上を含めることができます**行**要素。
    -   **行**要素

        各**行**要素は、回線デバイスを指定します。 いずれかを追加することで、各回線デバイスを識別する必要があります、**アドレス**要素または**PermanentID**の下の要素、**行**要素。

        各**行**要素を設定できます、**削除**属性。 この属性を設定する場合は、ユーザーにその回線デバイスが不要になった割り当てられます。 この属性が設定されていない場合、ユーザーはその回線デバイスへのアクセスを取得します。 回線デバイスがユーザーに使用できない場合、エラーは表示されません。

## <a name="examples"></a>例
-   次のサンプル XML のコード セグメントでは、上記で定義された要素の正しい使用法について説明します。  
    -   次のコードは、User1 に割り当てられたすべての回線デバイスを削除します。  
        ```
        <UserList>
          <User NoMerge="1">
            <DomainUser>domain1\user1</DomainUser>
          </User>
        </UserList>
        ```  
    -   次のコードは、アドレス 99999 の回線が 1 つを割り当てる前に、User1 に割り当てられているすべての回線デバイスを削除します。 User1 には、割り当てられているすべての回線デバイスが以前に割り当てられたかどうかに関係なく、他の回線デバイスはありません。  
        ```
        <UserList>
          <User NoMerge="1">
            <DomainUser>domain1\user1</DomainUser>
            <FriendlyName>User1</FriendlyName>
            <LineList>
              <Line>
                <Address>99999</Address>
              </Line>
            </LineList>
          </User>
        </UserList>
        
        ```  
    -   次のコードでは、以前に割り当てられた回線デバイスを削除することがなく、User1 の 1 つの回線デバイスを追加します。  
        ```
        <UserList>
          <User>
            <DomainUser>domain1\user1</DomainUser>
            <FriendlyName>User1</FriendlyName>
            <LineList>
              <Line>
                <Address>99999</Address>
              </Line>
            </LineList>
          </User>
        </UserList>
        
        ```  
    -   次のコードでは、回線アドレス 99999 を追加し、User1 のアクセスから回線アドレス 88888 を削除します。  
        ```
        <UserList>
          <User>
            <DomainUser>domain1\user1</DomainUser>
            <FriendlyName>User1</FriendlyName>
            <LineList>
              <Line>
                <Address>99999</Address>
              </Line>
              <Line Remove="1">
                <Address>88888</Address>
              </Line>
            </LineList>
          </User>
        </UserList>
        
        ```  
    -   次のコードでは、永続的なデバイス 1000 を追加し、User1 のアクセスから 88888 を削除します。  
        ```
        <UserList>
          <User>
            <DomainUser>domain1\user1</DomainUser>
            <FriendlyName>User1</FriendlyName>
            <LineList>
              <Line>
                <PermanentID>1000</PermanentID>
              </Line>
              <Line Remove="1">
                <Address>88888</Address>
              </Line>
            </LineList>
          </User>
        </UserList>
        
        
        ```  
-   後に、次のサンプル出力が表示されます、 **/d** TAPI の現在の構成を表示するコマンド ライン オプションを指定します。 テレフォニー プロバイダーごとに、関連付けられた回線デバイスと、アドレスと各回線デバイスに関連付けられているユーザーは表示します。  
    ```
    NDIS Proxy TAPI Service Provider
            Line: "WAN Miniport (L2TP)"
                    Permanent ID: 12345678910
    
    NDIS Proxy TAPI Service Provider
            Line: "LPT1DOMAIN1\User1"
                    Permanent ID: 12345678910
    
    Microsoft H.323 Telephony Service Provider
            Line: "H323 Line"
                    Permanent ID: 123456
                    Addresses:
                            BLDG1-TAPI32
    
    ```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)

[コマンド シェルの概要](https://technet.microsoft.com/library/cc737438(v=ws.10).aspx)