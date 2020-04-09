---
title: tsecimp
description: Tsecimp の Windows コマンドトピックでは、拡張マークアップ言語 (XML) ファイルからの割り当て情報を TAPI サーバーセキュリティファイル (Tsec.ini) にインポートします。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d7488ec6-0eff-45ff-89ee-9cbe752416bf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 30a097bcd25e981f72a421b81b80b595343404ba
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80832505"
---
# <a name="tsecimp"></a>tsecimp

拡張マークアップ言語 (XML) ファイルからの割り当て情報を TAPI サーバーセキュリティファイル (Tsec.ini) にインポートします。 また、このコマンドを使用して、TAPI プロバイダーと、それぞれに関連付けられている回線デバイスの一覧を表示したり、コンテンツをインポートせずに XML ファイルの構造を検証したり、ドメインのメンバーシップを確認したりすることもできます。

## <a name="syntax"></a>構文

```
tsecimp /f <Filename> [{/v | /u}]
tsecimp /d
```

#### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/f \<ファイル名 >|必須。 インポートする割り当て情報を含んだ XML ファイルの名前を指定します。|
|/v|Tsec.ini ファイルに情報をインポートせず、XML ファイルの構造を検証します。|
|/u|各ユーザーについて、XML ファイルで指定されたドメインのメンバーかどうかをチェックします。 このパラメーターは、ネットワークに接続されているコンピューター上で使用する必要があります。 大量のユーザー割り当て情報を処理する場合、このパラメーターを指定するとパフォーマンスが大幅に低下することがあります。|
|/d|インストールされているテレフォニー プロバイダーの一覧を表示します。 テレフォニー プロバイダーごとに、関連付けられた回線デバイスと、各回線デバイスに関連付けられたアドレスおよびユーザーが表示されます。|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="remarks"></a>コメント

-   割り当て情報のインポート元となる XML ファイルは、次に説明する構造に従っている必要があります。  
    -   **UserList**要素

        **UserList**は、XML ファイルの最上位の要素です。
    -   **User**要素

        各**user**要素には、ドメインのメンバーであるユーザーに関する情報が含まれています。 各ユーザーには 1 つ以上の回線デバイスが割り当てられることがあります。

        さらに、各**ユーザー**要素には、 **nomerge**という名前の属性が含まれている場合があります。 この属性が指定されている場合、ユーザーに対する回線デバイスの現在の割り当ては、新しい割り当てが作成される前にすべて削除されます。 この属性を使用すると、無用なユーザー割り当てを簡単に削除できます。 既定では、この属性は指定されません。

        **User**要素には、ユーザーのドメインとユーザー名を指定する単一の**domainusername**要素が含まれている必要があります。 **User**要素には、ユーザーのフレンドリ名を指定する**FriendlyName**要素が1つ含まれている場合もあります。

        **User**要素には、 **linelist**要素が1つ含まれている場合があります。 **Linelist**要素が存在しない場合、このユーザーのすべてのラインデバイスが削除されます。
    -   **Linelist**要素

        **Linelist**要素には、ユーザーに割り当てられる可能性のある各行またはデバイスに関する情報が含まれています。 各**Linelist**要素には、複数の**Line**要素を含めることができます。
    -   **Line**要素

        各**line**要素は、ラインデバイスを指定します。 **Line 要素の下**に**Address**要素または**PermanentID**要素を追加することによって、各ラインデバイスを識別する必要があります。

        各**Line**要素に対して、 **Remove**属性を設定できます。 この属性を設定した場合、当該ユーザーはその回線デバイスに割り当てられなくなります。 設定しない場合、当該ユーザーはその回線デバイスにアクセスできます。 ユーザーが回線デバイスを使用できない場合、エラーは表示されません。

## <a name="examples"></a>例
- 次に示す部分的な XML コードのサンプルは、上で定義した要素の正しい使用法を示しています。  
  - 次のコードは、User1 に割り当てられているすべてのラインデバイスを削除します。  
    ```
    <UserList>
      <User NoMerge=1>
        <DomainUser>domain1\user1</DomainUser>
      </User>
    </UserList>
    ```  
  - 次のコードは、User1 に割り当てられたすべてのラインデバイスを削除してから、アドレス99999を使用して1行を割り当てます。 これ以外の回線デバイスが既に User1 に割り当てられていたとしても、以後 User1 に割り当てられるのはこの回線だけとなります。  
    ```
    <UserList>
      <User NoMerge=1>
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
  - 次のコードでは、既に User1 に割り当てられている回線デバイスを削除することなく、1 つの回線デバイスを追加します。  
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
          <Line Remove=1>
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
          <Line Remove=1>
            <Address>88888</Address>
          </Line>
        </LineList>
      </User>
    </UserList>
    ```

-   次のサンプル出力は、現在の TAPI 構成を表示するために **/d**コマンドラインオプションを指定した後に表示されます。 テレフォニー プロバイダーごとに、関連付けられた回線デバイスと、各回線デバイスに関連付けられたアドレスおよびユーザーが表示されます。  
    ```
    NDIS Proxy TAPI Service Provider
            Line: WAN Miniport (L2TP)
                    Permanent ID: 12345678910

    NDIS Proxy TAPI Service Provider
            Line: LPT1DOMAIN1\User1
                    Permanent ID: 12345678910

    Microsoft H.323 Telephony Service Provider
            Line: H323 Line
                    Permanent ID: 123456
                    Addresses:
                            BLDG1-TAPI32

    ```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

[コマンドシェルの概要](https://technet.microsoft.com/library/cc737438(v=ws.10).aspx)
