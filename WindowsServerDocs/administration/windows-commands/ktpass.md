---
title: ktpass
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 47087676-311e-41f1-8414-199740d01444
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: de74d04ceaca0147b4d12cd9c0eaacbf233e2fd7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841215"
---
# <a name="ktpass"></a>ktpass

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Active directory ドメインサービス (AD DS) のホストまたはサービスのサーバープリンシパル名を構成し、サービスの共有シークレットキーを含む、キーの付いたファイルを生成します。 .keytab ファイルは、Kerberos 認証プロトコルのマサチューセッツ工科大学 (MIT) による実装に基づいています。 Ktpass コマンドラインツールを使用すると、kerberos 認証をサポートする非 Windows サービスで、Kerberos キー配布センター (KDC) サービスによって提供される相互運用性機能を使用できます。 このトピックは、トピックの冒頭にある「**適用対象**」の一覧に指定されているオペレーティングシステムのバージョンに適用されます。  

## <a name="syntax"></a>構文  
```  
ktpass  
[/out <FileName>]   
[/princ <PrincipalName>]   
[/mapuser <UserAccount>]   
[/mapop {add|set}] [{-|+}desonly] [/in <FileName>]  
[/pass {Password|*|{-|+}rndpass}]  
[/minpass]  
[/maxpass]  
[/crypto {DES-CBC-CRC|DES-CBC-MD5|RC4-HMAC-NT|AES256-SHA1|AES128-SHA1|All}]  
[/itercount]  
[/ptype {KRB5_NT_PRINCIPAL|KRB5_NT_SRV_INST|KRB5_NT_SRV_HST}]  
[/kvno <KeyversionNum>]  
[/answer {-|+}]  
[/target]  
[/rawsalt] [{-|+}dumpsalt] [{-|+}setupn] [{-|+}setpass <Password>]  [/?|/h|/help]  
```  
### <a name="parameters"></a>パラメーター  

|                                             パラメーター                                              |                                                                                                                                                                                                                                                                                                      説明                                                                                                                                                                                                                                                                                                       |
|----------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                          /out <FileName>                                           |                                                                                                                                                                        生成する Kerberos version 5. キータブファイルの名前を指定します。 **注:** これは、Windows オペレーティングシステムを実行していないコンピューターに転送し、既存の.......... を使用して、/Etc/Krb5.keytab.                                                                                                                                                                        |
|                                       /princ <PrincipalName>                                       |                                                                                                                                                                                                                   host/computer.contoso.com@CONTOSO.COMの形式でプリンシパル名を指定します。 **警告:** このパラメーターは大文字と小文字が区別されます。 詳細については、「[解説](#BKMK_remarks)」を参照してください。                                                                                                                                                                                                                    |
|                                       /mapuser <UserAccount>                                       |                                                                                                                                                                                                                                                **Princ**パラメーターによって指定された Kerberos プリンシパルの名前を、指定されたドメインアカウントにマップします。                                                                                                                                                                                                                                                |
|                                       /mapop {add&#124;set}                                        |                                                                                                                                                                             マッピング属性を設定する方法を指定します。<p>-   **追加**すると、指定したローカルユーザー名の値が追加されます。 これが既定値です。<br />-   **セット**は、指定されたローカルユーザー名に対して、Data Encryption STANDARD (DES) のみの暗号化の値を設定します。                                                                                                                                                                             |
|                                         {-&#124;+} desonly                                          |                                                                                                                                                            既定では、DES のみの暗号化が設定されます。<p>-    **+** は、DES のみの暗号化のアカウントを設定します。<br />-    **-** では、DES のみの暗号化でアカウントの制限が解放されます。 **重要:** Windows 7 と windows Server 2008 R2 以降では、Windows では既定で DES がサポートされていません。                                                                                                                                                            |
|                                           /in <FileName>                                           |                                                                                                                                                                                                                                                       Windows オペレーティングシステムを実行していないホストコンピューターから読み取るための、キーのキーファイルを指定します。                                                                                                                                                                                                                                                        |
|                          /pass {パスワード&#124;\*&#124;{-&#124;+} rndpass}                           |                                                                                                                                                                                                                                           **Princ**パラメーターで指定したプリンシパルユーザー名のパスワードを指定します。 パスワードの入力を求めるには、\* を使用します。                                                                                                                                                                                                                                            |
|                                              /minpass                                              |                                                                                                                                                                                                                                                                            ランダムパスワードの長さの最小値を15文字に設定します。                                                                                                                                                                                                                                                                            |
|                                              /maxpass                                              |                                                                                                                                                                                                                                                                           ランダムなパスワードの最大長を256文字に設定します。                                                                                                                                                                                                                                                                            |
| /crypto {DES-CBC-CRC&#124;DES-CBC-MD5&#124;RC4-HMAC-NT&#124;AES256-sha1&#124;AES128-sha1&#124;All} | キータブファイルに生成されるキーを指定します。<p>-   には、互換性のために**CRC-CBC**が使用されます。<br />-   **DES-CBC-MD5**は、MIT 実装により厳密に準拠し、互換性のために使用されます。<br />-   **RC4-HMAC-NT**は、128ビットの暗号化を採用しています。<br />-   **AES256-sha1**は AES256 暗号化を採用しています。<br />-   **AES128-sha1**は AES128 暗号化を採用しています。<br />すべてのサポートされている暗号化の種類を使用できる**すべて**の状態を -   します。 **注:** 既定の設定は、旧バージョンの MIT に基づいています。 したがって、`/crypto` は常に指定する必要があります。 |
|                                             /自動カウント                                             |                                                                                                                                                                                                                        AES 暗号化に使用されるイテレーションの数を指定します。 既定では、非 AES 暗号化の場合は、4096に**設定され**ています。                                                                                                                                                                                                                         |
|               /ptype {KRB5_NT_PRINCIPAL&#124;KRB5_NT_SRV_INST&#124;KRB5_NT_SRV_HST}                |                                                                                                                                                                                         プリンシパルの種類を指定します。<p>-   **KRB5_NT_PRINCIPAL**は一般的なプリンシパルの種類です (推奨)。<br />-   **KRB5_NT_SRV_INST**は、ユーザーサービスインスタンスです。<br />-   **KRB5_NT_SRV_HST**はホストサービスインスタンスです。                                                                                                                                                                                         |
|                                       /kvno <KeyversionNum>                                        |                                                                                                                                                                                                                                                                               キーのバージョン番号を指定します。 既定値は 1 です。                                                                                                                                                                                                                                                                                |
|                                         /answer {-&#124;+}                                         |                                                                                                                                                                                                                    バックグラウンド応答モードを設定します。<p>**-** 回答を入力せずにパスワードのプロンプトを自動的にリセットします。<p>**+** [OK] をオンにすると、パスワードの入力を自動的にリセットします。                                                                                                                                                                                                                     |
|                                              /target                                               |                                                                                                                                                                                           使用するドメインコントローラーを設定します。 既定では、プリンシパル名に基づいて、ドメインコントローラーが検出されます。 ドメインコントローラ名が解決されない場合は、有効なドメインコントローラの入力を求めるダイアログボックスが表示されます。                                                                                                                                                                                           |
|                                              /rawsalt                                              |                                                                                                                                                                                                                                                           キーの生成時に ktpass が rawsalt アルゴリズムを使用するように強制します。 このパラメーターは必要ありません。                                                                                                                                                                                                                                                            |
|                                         {-&#124;+} dumpsalt                                         |                                                                                                                                                                                                                                                           このパラメーターの出力は、キーの生成に使用されている MIT salt アルゴリズムを示しています。                                                                                                                                                                                                                                                            |
|                                          {-&#124;+} setupn                                          |                                                                                                                                                                                                                                          サービスプリンシパル名 (SPN) に加えて、ユーザープリンシパル名 (UPN) を設定します。 既定では、キーセットファイルに両方を設定します。                                                                                                                                                                                                                                           |
|                                    {-&#124;+} setpass <Password>                                    |                                                                                                                                                                                                                                                          指定されたときにユーザーのパスワードを設定します。 Rndpass が使用されている場合は、ランダムなパスワードが代わりに生成されます。                                                                                                                                                                                                                                                           |
|                                       /?&#124;/h&#124;/help                                        |                                                                                                                                                                                                                                                                                         Ktpass のコマンドラインヘルプを表示します。                                                                                                                                                                                                                                                                                         |

## <a name="remarks"></a><a name=BKMK_remarks></a>」  
Windows オペレーティングシステムを実行していないシステムで実行されているサービスは、active directory ドメインサービスのサービスインスタンスアカウントを使用して構成できます。 これにより、任意の Kerberos クライアントが windows Kdc を使用して、Windows オペレーティングシステムを実行していないサービスに対して認証を行うことができます。  
/Princ パラメーターは ktpass によって評価されず、提供されたとおりに使用されます。 キーボックスファイルを生成するときに、パラメーターが**userPrincipalName**属性値の大文字小文字と一致するかどうかのチェックはありません。 このキータブファイルを使用した大文字と小文字が区別される Kerberos ディストリビューションでは、大文字と小文字の一致がない場合に問題が発生し、事前認証時に失敗することがあります。 LDifDE エクスポートファイルから正しい**userPrincipalName**属性値を確認して取得します。 例 :  
```  
ldifde /f keytab_user.ldf /d CN=Keytab User,OU=UserAccounts,DC=contoso,DC=corp,DC=microsoft,DC=com /p base /l samaccountname,userprincipalname  
```  
## <a name="examples"></a><a name=BKMK_examples></a>例  
次の例では、ユーザーサンプル1の現在のディレクトリに、Kerberos のキータブファイルを作成する方法を示します。 (このファイルは、Windows オペレーティングシステムを実行していないホストコンピューター上の Krb5.conf ファイルとマージされます)。Kerberos のキーの種類が、サポートされているすべての暗号化の種類に対して作成されます。  
Windows オペレーティングシステムを実行していないホストコンピューターに対して、キーセットファイルを生成するには、次の手順を使用してプリンシパルをアカウントにマップし、ホストプリンシパルパスワードを設定します。  
1.  Active directory ユーザーとコンピュータースナップインを使用して、Windows オペレーティングシステムを実行していないコンピューター上のサービスのユーザーアカウントを作成します。 たとえば、サンプル1という名前のアカウントを作成します。  
2.  Ktpass を使用して、コマンドプロンプトで次のように入力し、ユーザーアカウントの id マッピングを設定します。  
    ```  
    ktpass /princ host/Sample1.contoso.com@CONTOSO.COM /mapuser Sample1 /pass MyPas$w0rd /out Sample1.keytab /crypto all /ptype KRB5_NT_PRINCIPAL /mapop set   
    ```  

    > [!NOTE]  
    > 複数のサービスインスタンスを同じユーザーアカウントにマップすることはできません。  

3.  Windows オペレーティングシステムを実行していないホストコンピューター上の/Etc/Krb5.keytab ファイルに、このキーファイルをマージします。 

## <a name="additional-references"></a>その他の参照情報  
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
