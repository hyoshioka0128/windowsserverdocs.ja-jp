---
title: tsecimp
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 1c596d6d24a611882c0ecf234c22c83a268ec53c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363933"
---
# <a name="tsecimp"></a>tsecimp



拡張マークアップ言語 (XML) ファイルからの割り当て情報を TAPI サーバーセキュリティファイル (Tsec.ini) にインポートします。 また、このコマンドを使用して、TAPI プロバイダーと、それぞれに関連付けられている回線デバイスの一覧を表示したり、コンテンツをインポートせずに XML ファイルの構造を検証したり、ドメインのメンバーシップを確認したりすることもできます。

## <a name="syntax"></a>構文

```
tsecimp /f <Filename> [{/v | /u}]
tsecimp /d
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/f \<ファイル名 >|必須。 インポートする割り当て情報を含む XML ファイルの名前を指定します。|
|/v|Tsec.ini ファイルに情報をインポートせずに、XML ファイルの構造を検証します。|
|/u|各ユーザーが XML ファイルで指定されたドメインのメンバーであるかどうかを確認します。 このパラメーターを使用するコンピューターは、ネットワークに接続されている必要があります。 大量のユーザー割り当て情報を処理する場合、このパラメーターを使用するとパフォーマンスが大幅に低下する可能性があります。|
|/d|インストールされているテレフォニープロバイダーの一覧を表示します。 テレフォニープロバイダーごとに、関連付けられた回線デバイスと、各回線デバイスに関連付けられているアドレスおよびユーザーが一覧表示されます。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>コメント

-   割り当て情報のインポート元となる XML ファイルは、以下で説明する構造に従う必要があります。  
    -   **UserList**要素

        **UserList**は、XML ファイルの最上位の要素です。
    -   **User**要素

        各**user**要素には、ドメインのメンバーであるユーザーに関する情報が含まれています。 各ユーザーには、1つまたは複数のラインデバイスが割り当てられている可能性があります。

        さらに、各**ユーザー**要素には、 **nomerge**という名前の属性が含まれている場合があります。 この属性が指定されている場合、ユーザーに対する現在のラインデバイスの割り当てはすべて削除されてから、新しいものが作成されます。 この属性を使用すると、不要なユーザー割り当てを簡単に削除できます。 既定では、この属性は設定されていません。

        **User**要素には、ユーザーのドメインとユーザー名を指定する単一の**domainusername**要素が含まれている必要があります。 **User**要素には、ユーザーのフレンドリ名を指定する**FriendlyName**要素が1つ含まれている場合もあります。

        **User**要素には、 **linelist**要素が1つ含まれている場合があります。 **Linelist**要素が存在しない場合、このユーザーのすべてのラインデバイスが削除されます。
    -   **Linelist**要素

        **Linelist**要素には、ユーザーに割り当てられる可能性のある各行またはデバイスに関する情報が含まれています。 各**Linelist**要素には、複数の**Line**要素を含めることができます。
    -   **Line**要素

        各**line**要素は、ラインデバイスを指定します。 Line**要素の下**に**Address**要素または**PermanentID**要素を追加することによって、各ラインデバイスを識別する必要があります。

        各**Line**要素に対して、 **Remove**属性を設定できます。 この属性を設定すると、その行デバイスはユーザーに割り当てられなくなります。 この属性が設定されていない場合、ユーザーはその回線デバイスにアクセスできます。 ユーザーが回線デバイスを使用できない場合、エラーは表示されません。

## <a name="examples"></a>使用例
- 次のサンプル XML コードセグメントでは、上で定義した要素の正しい使用方法を示しています。  
  - 次のコードは、User1 に割り当てられているすべてのラインデバイスを削除します。  
    ```
    <UserList>
      <User NoMerge="1">
        <DomainUser>domain1\user1</DomainUser>
      </User>
    </UserList>
    ```  
  - 次のコードは、User1 に割り当てられたすべてのラインデバイスを削除してから、アドレス99999を使用して1行を割り当てます。 1つのラインデバイスが以前に割り当てられているかどうかに関係なく、User1 にはその他の回線デバイスは割り当てられません。  
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
  - 次のコードでは、以前に割り当てられた回線デバイスを削除せずに、User1 に1つのラインデバイスを追加します。  
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
  - 次のコードでは、行アドレス99999を追加し、User1 アクセスから行アドレス88888を削除します。  
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
  - 次のコードでは、永続的なデバイス1000を追加し、User1 アクセスから88888行目を削除します。  
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

-   次のサンプル出力は、現在の TAPI 構成を表示するために **/d**コマンドラインオプションを指定した後に表示されます。 テレフォニープロバイダーごとに、関連付けられた回線デバイスと、各回線デバイスに関連付けられているアドレスおよびユーザーが一覧表示されます。  
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

[コマンド ライン構文の記号](command-line-syntax-key.md)

[コマンドシェルの概要](https://technet.microsoft.com/library/cc737438(v=ws.10).aspx)
