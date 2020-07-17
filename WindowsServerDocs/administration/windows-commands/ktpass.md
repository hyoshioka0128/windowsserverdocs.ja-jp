---
title: ktpass
description: Ktpass コマンドの参照記事。このコマンドは、AD DS でホストまたはサービスのサーバープリンシパル名を構成し、サービスの共有シークレットキーを含む... キーを生成します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 47087676-311e-41f1-8414-199740d01444
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fbf7b47f4f21a2c964d14dd1200b15ad635d7471
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931826"
---
# <a name="ktpass"></a>ktpass

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Active Directory Domain Services (AD DS) でホストまたはサービスのサーバープリンシパル名を構成し、サービスの共有シークレットキーを含む、キーファイルを生成します。 .keytab ファイルは、Kerberos 認証プロトコルのマサチューセッツ工科大学 (MIT) による実装に基づいています。 Ktpass コマンドラインツールを使用すると、kerberos 認証をサポートする非 Windows サービスで、Kerberos キー配布センター (KDC) サービスによって提供される相互運用性機能を使用できます。

## <a name="syntax"></a>構文

```
ktpass
[/out <filename>]
[/princ <principalname>]
[/mapuser <useraccount>]
[/mapop {add|set}] [{-|+}desonly] [/in <filename>]
[/pass {password|*|{-|+}rndpass}]
[/minpass]
[/maxpass]
[/crypto {DES-CBC-CRC|DES-CBC-MD5|RC4-HMAC-NT|AES256-SHA1|AES128-SHA1|All}]
[/itercount]
[/ptype {KRB5_NT_PRINCIPAL|KRB5_NT_SRV_INST|KRB5_NT_SRV_HST}]
[/kvno <keyversionnum>]
[/answer {-|+}]
[/target]
[/rawsalt] [{-|+}dumpsalt] [{-|+}setupn] [{-|+}setpass <password>]  [/?|/h|/help]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ------------|
| /out`<filename>` | 生成する Kerberos version 5. キータブファイルの名前を指定します。 **注:** これは、Windows オペレーティングシステムを実行していないコンピューターに転送する、キーが付けられたファイルです。その後、既存の.............. */Etc/Krb5.keytab*ファイルを置き換えます。 |
| /princ `<principalname>` | の形式でプリンシパル名を指定し host/computer.contoso.com@CONTOSO.COM ます。 **警告:** このパラメーターでは、大文字と小文字が区別されます。 |
| /mapuser `<useraccount>` | **Princ**パラメーターによって指定された Kerberos プリンシパルの名前を、指定されたドメインアカウントにマップします。 |
| /mapop`{add|set}` | マッピング属性を設定する方法を指定します。<ul><li>**追加**-指定したローカルユーザー名の値を追加します。 既定値です。</li><li>**設定**-指定したローカルユーザー名のデータ暗号化標準 (DES) のみの暗号化の値を設定します。</li></ul> |
| `{-|+}`desonly | 既定では、DES のみの暗号化が設定されます。<ul><li>**+** DES のみの暗号化のアカウントを設定します。</li><li>**-** アカウントの制限を、DES のみの暗号化に対して解放します。 **重要:** Windows では既定で DES がサポートされていません。</li></ul> |
| /in`<filename>` | Windows オペレーティングシステムを実行していないホストコンピューターから読み取るための、キーのキーファイルを指定します。 |
| /pass`{password|*|{-|+}rndpass}` | **Princ**パラメーターで指定したプリンシパルユーザー名のパスワードを指定します。 `*`パスワードの入力を求めるには、を使用します。 |
| /minpass | ランダムパスワードの長さの最小値を15文字に設定します。 |
| /maxpass | ランダムなパスワードの最大長を256文字に設定します。 |
| /暗号化`{DES-CBC-CRC|DES-CBC-MD5|RC4-HMAC-NT|AES256-SHA1|AES128-SHA1|All}` | キータブファイルに生成されるキーを指定します。<ul><li>**DES-CBC** -互換性のために使用されます。</li><li>**DES (CBC** )-MIT 実装により厳密に準拠し、互換性のために使用されます。</li><li>**RC4-HMAC-NT** -128 ビットの暗号化を採用しています。</li><li>**AES256-sha1** -AES256 暗号化を採用しています。</li><li>   **AES128-sha1** -AES128 暗号化を採用しています。</li><li>**All** -サポートされているすべての暗号化の種類を使用できます。</li></ul><p>**注:** 既定の設定は、旧バージョンの MIT に基づいているため、常にパラメーターを使用する必要があり `/crypto` ます。 |
| /自動カウント | AES 暗号化に使用されるイテレーションの数を指定します。 既定では、AES 以外の**暗号化の場合は、** 値が無視され、aes 暗号化は4096に設定されます。 |
| /ptype`{KRB5_NT_PRINCIPAL|KRB5_NT_SRV_INST|KRB5_NT_SRV_HST}` | プリンシパルの種類を指定します。<ul><li>**KRB5_NT_PRINCIPAL** -一般プリンシパルの種類 (推奨)。</li><li>**KRB5_NT_SRV_INST** -ユーザーサービスインスタンス</li><li>  **KRB5_NT_SRV_HST** -ホストサービスインスタンス</li></ul> |
| /kvno`<keyversionnum>` | キーのバージョン番号を指定します。 既定値は 1 です。 |
| /answer`{-|+}` | バックグラウンド応答モードを設定します。<ul><li>**-** 回答を入力**せず**にパスワードのプロンプトを自動的にリセットします。</li><li>**+****[Ok] をオン**にすると、パスワードの入力を自動的にリセットします。</li></ul> |
| /target | 使用するドメインコントローラーを設定します。 既定では、プリンシパル名に基づいて、ドメインコントローラーが検出されます。 ドメインコントローラ名が解決されない場合は、有効なドメインコントローラの入力を求めるダイアログボックスが表示されます。 |
| /rawsalt | キーの生成時に ktpass が rawsalt アルゴリズムを使用するように強制します。 このパラメーターは省略可能です。 |
| `{-|+}dumpsalt` | このパラメーターの出力は、キーの生成に使用されている MIT salt アルゴリズムを示しています。 |
| `{-|+}setupn` | サービスプリンシパル名 (SPN) に加えて、ユーザープリンシパル名 (UPN) を設定します。 既定では、キーセットファイルに両方を設定します。 |
| `{-|+}setpass <password>` | 指定されたときにユーザーのパスワードを設定します。 Rndpass が使用されている場合は、ランダムなパスワードが代わりに生成されます。 |
| /? | このコマンドのヘルプを表示します。 |

#### <a name="remarks"></a>注釈

- Windows オペレーティングシステムを実行していないシステムで実行されているサービスは、AD DS のサービスインスタンスアカウントを使用して構成できます。 これにより、任意の Kerberos クライアントが windows Kdc を使用して、Windows オペレーティングシステムを実行していないサービスに対して認証を行うことができます。

- **/Princ**パラメーターは ktpass によって評価されず、提供されたとおりに使用されます。 キーボックスファイルを生成するときに、パラメーターが**userPrincipalName**属性値の大文字と小文字の区別に一致しているかどうかは確認されません。 このキータブファイルを使用する、大文字と小文字が区別される Kerberos ディストリビューションでは、大文字と小文字の一致がない場合に問題が発生する可能性があり、事前認証時に失敗することもあります。 LDifDE エクスポートファイルから正しい**userPrincipalName**属性値を確認して取得すること。 次に例を示します。

    ```
    ldifde /f keytab_user.ldf /d CN=Keytab User,OU=UserAccounts,DC=contoso,DC=corp,DC=microsoft,DC=com /p base /l samaccountname,userprincipalname
    ````

### <a name="examples"></a>例

Windows オペレーティングシステムを実行していないホストコンピューターの Kerberos のキーセットファイルを作成するには、プリンシパルをアカウントにマップし、ホストプリンシパルのパスワードを設定する必要があります。

1. Active directory**ユーザーとコンピューター**スナップインを使用して、Windows オペレーティングシステムを実行していないコンピューター上のサービスのユーザーアカウントを作成します。 たとえば、 *User1*という名前のアカウントを作成します。

2. 次のように入力して、 **ktpass**コマンドを使用して、ユーザーアカウントの id マッピングを設定します。

    ```
    ktpass /princ host/User1.contoso.com@CONTOSO.COM /mapuser User1 /pass MyPas$w0rd /out machine.keytab /crypto all /ptype KRB5_NT_PRINCIPAL /mapop set
    ```

    > [!NOTE]
    > 複数のサービスインスタンスを同じユーザーアカウントにマップすることはできません。

3. Windows オペレーティングシステムを実行していないホストコンピューター上の */Etc/Krb5.keytab*ファイルに、このキーファイルをマージします。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
