---
title: ktpass
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 47087676-311e-41f1-8414-199740d01444
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ae7508aaefd136a91bd19e547b407020293ca484
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437924"
---
# <a name="ktpass"></a>ktpass

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Active directory Domain Services (AD DS) で、ホストまたはサービスのサーバー プリンシパル名を構成し、サービスの共有シークレット キーを含む .keytab ファイルを生成します。 .keytab ファイルは、Kerberos 認証プロトコルのマサチューセッツ工科大学 (MIT) による実装に基づいています。 Ktpass コマンドライン ツールは、Kerberos キー配布センター (KDC) サービスによって提供される相互運用性機能を使用する Kerberos 認証をサポートする Windows 以外のサービスを使用します。 このトピックで指定されているオペレーティング システムのバージョンに適用されます、**適用先**トピックの冒頭にある一覧。  

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
## <a name="parameters"></a>パラメーター  

|                                             パラメーター                                              |                                                                                                                                                                                                                                                                                                      説明                                                                                                                                                                                                                                                                                                       |
|----------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                          /out <FileName>                                           |                                                                                                                                                                        生成するには、Kerberos バージョン 5 .keytab ファイルの名前を指定します。 **注:** これは、次のように既存 .keytab ファイル/Etc/Krb5.keytab を使って、Windows オペレーティング システムが実行されていないコンピューターに転送して、置換またはマージ .keytab ファイル。                                                                                                                                                                        |
|                                       /princ <PrincipalName>                                       |                                                                                                                                                                                                                   フォームでプリンシパル名を指定します。host/computer.contoso.com@CONTOSO.COMします。 **警告:** このパラメーターは大文字小文字を区別します。 参照してください[解説](#BKMK_remarks)詳細についてはします。                                                                                                                                                                                                                    |
|                                       /mapuser <UserAccount>                                       |                                                                                                                                                                                                                                                マップで指定されている Kerberos プリンシパルの名前、 **princ**パラメーターを指定したドメイン アカウント。                                                                                                                                                                                                                                                |
|                                       /mapop {追加&#124;設定}                                        |                                                                                                                                                                             マッピング属性を設定する方法を指定します。<br /><br />-   **追加**指定されたローカル ユーザー名の値を追加します。 これが既定値です。<br />-   **設定**値のデータ暗号化標準 (DES) の設定-指定したローカル ユーザー名のみを暗号化します。                                                                                                                                                                             |
|                                         {-&#124;+}desonly                                          |                                                                                                                                                            既定で DES のみの暗号化が設定されます。<br /><br />-    **+** DES 専用の暗号化用のアカウントを設定します。<br />-    **-** DES 専用の暗号化のため、アカウントの制限を解放します。 **重要:** Windows 7 および Windows Server 2008 R2 以降、Windows は、既定で DES をサポートしません。                                                                                                                                                            |
|                                           /in <FileName>                                           |                                                                                                                                                                                                                                                       Windows オペレーティング システムが実行されていないホスト コンピューターから読み取る .keytab ファイルを指定します。                                                                                                                                                                                                                                                        |
|                          /pass {Password&#124;\*&#124;{-&#124;+}rndpass}                           |                                                                                                                                                                                                                                           によって指定されるプリンシパルのユーザー名のパスワードを指定します、 **princ**パラメーター。 使用して"\*"パスワードを要求します。                                                                                                                                                                                                                                            |
|                                              /minpass                                              |                                                                                                                                                                                                                                                                            15 文字のランダムなパスワードの最小の長さを設定します。                                                                                                                                                                                                                                                                            |
|                                              /maxpass                                              |                                                                                                                                                                                                                                                                           ランダムなパスワードの最大の長さを 256 文字に設定します。                                                                                                                                                                                                                                                                            |
| /crypto {DES-CBC-CRC&#124;DES-CBC-MD5&#124;RC4-HMAC-NT&#124;AES256-SHA1&#124;AES128-SHA1&#124;All} | Keytab ファイルで生成されるキーを指定します。<br /><br />-   **DES の CRC CBC**互換性のために使用します。<br />-   **DES CBC-MD5** MIT 実装により厳密に準拠し、互換性のために使用します。<br />-   **RC4-NT HMAC** 128 ビット暗号化を採用しています。<br />-   **AES256、SHA1** AES256-CTS の HMAC-SHA1-96 暗号化を採用しています。<br />-   **AES128、SHA1** AES128、CTS の HMAC-SHA1-96 暗号化を採用しています。<br />-   **すべて**暗号化の種類がサポートされているすべての状態を使用することができます。 **注:** 既定の設定は、MIT の以前のバージョンに基づいています。 そのため、`/crypto`常に指定する必要があります。 |
|                                             /itercount                                             |                                                                                                                                                                                                                        AES 暗号化で使用される、反復回数を指定します。 既定値を**itercount**は非 AES 暗号化で無視され、AES 暗号化 4,096 に設定します。                                                                                                                                                                                                                         |
|               /ptype {KRB5_NT_PRINCIPAL&#124;KRB5_NT_SRV_INST&#124;KRB5_NT_SRV_HST}                |                                                                                                                                                                                         プリンシパルの種類を指定します。<br /><br />-   **KRB5_NT_PRINCIPAL**は一般的なプリンシパルの種類 (推奨)。<br />-   **KRB5_NT_SRV_INST**はユーザーのサービス インスタンスです。<br />-   **KRB5_NT_SRV_HST**ホスト サービスのインスタンスです。                                                                                                                                                                                         |
|                                       /kvno <KeyversionNum>                                        |                                                                                                                                                                                                                                                                               キーのバージョン番号を指定します。 既定値は 1 です。                                                                                                                                                                                                                                                                                |
|                                         /answer {-&#124;+}                                         |                                                                                                                                                                                                                    バック グラウンドの応答モードに設定します。<br /><br />**-** 回答番号で自動的にパスワード プロンプトの表示をリセットします。<br /><br />**+** 回答は、[はい] が自動的にパスワード プロンプトの表示をリセットします。                                                                                                                                                                                                                     |
|                                              /target                                               |                                                                                                                                                                                           使用するドメイン コント ローラーを設定します。 既定では、検出し、プリンシパル名に基づく、ドメイン コント ローラーです。 ドメイン コント ローラー名が解決しない場合、有効なドメイン コント ローラーのダイアログ ボックスが求められます。                                                                                                                                                                                           |
|                                              /rawsalt                                              |                                                                                                                                                                                                                                                           キーの生成時に、rawsalt アルゴリズムを使用する ktpass を強制します。 このパラメーターは必要ありません。                                                                                                                                                                                                                                                            |
|                                         {0}-&#124;+} dumpsalt                                         |                                                                                                                                                                                                                                                           このパラメーターの出力は、キーの生成に使用されている MIT salt アルゴリズムを示しています。                                                                                                                                                                                                                                                            |
|                                          {-&#124;+}setupn                                          |                                                                                                                                                                                                                                          サービス プリンシパル名 (SPN) だけでなくユーザー プリンシパル名 (UPN) を設定します。 既定では、.keytab ファイルの両方を設定します。                                                                                                                                                                                                                                           |
|                                    {0}-&#124;+} setpass <Password>                                    |                                                                                                                                                                                                                                                          指定されている場合、ユーザーのパスワードを設定します。 Rndpass を使用する場合は、代わりにランダムなパスワードが生成されます。                                                                                                                                                                                                                                                           |
|                                       /?&#124;/h&#124;/help                                        |                                                                                                                                                                                                                                                                                         コマンド ライン ヘルプを表示します ktpass します。                                                                                                                                                                                                                                                                                         |

## <a name="BKMK_remarks"></a>「解説」  
Windows オペレーティング システムを実行していないシステムで実行されているサービスは、active directory Domain Services でのサービス インスタンスのアカウントで構成できます。 これにより、Windows の Kdc を使用して、Windows オペレーティング システムを実行していないサービスに対する認証に Kerberos クライアントができます。  
/Princ パラメーターは、ktpass では評価されませんし、提供されるように使用されます。 パラメーターの大文字と小文字が一致するかどうかにチェックはありません、 **userPrincipalName** Keytab ファイルを生成するときに、属性値。 この Keytab ファイルを使用して Kerberos ディストリビューションの大文字小文字を区別できない問題が生じるケースと完全に一致が存在しない場合、事前認証中に失敗する可能性があります。 確認し、適切な取得**userPrincipalName** LDifDE のエクスポート ファイルから属性の値。 例:  
```  
ldifde /f keytab_user.ldf /d "CN=Keytab User,OU=UserAccounts,DC=contoso,DC=corp,DC=microsoft,DC=com" /p base /l samaccountname,userprincipalname  
```  
## <a name="BKMK_examples"></a>例  
次の例では、サンプル 1 のユーザーの現在のディレクトリで machine.keytab、Kerberos .keytab ファイルを作成する方法を示します。 (このファイルは、Windows オペレーティング システムが実行されていないホスト コンピューター上の Krb5.keytab ファイルではマージされます)。Kerberos .keytab ファイルは、全般のプリンシパルの種類のすべてのサポートされている暗号化の種類に対して作成されます。  
Windows オペレーティング システムが実行されていないホスト コンピューターの .keytab ファイルを生成するには、プリンシパルをアカウントにマップし、ホストのプリンシパルのパスワードを設定する、次の手順を使用します。  
1.  スナップインを使用する active directory ユーザーとコンピューター、Windows オペレーティング システムが実行されていないコンピューター上のサービスのユーザー アカウントを作成します。 たとえば、サンプル 1 の名前を持つアカウントを作成します。  
2.  コマンド プロンプトで、次を入力して、ユーザー アカウントの id マッピングを設定するには、ktpass を使用します。  
    ```  
    ktpass /princ host/Sample1.contoso.com@CONTOSO.COM /mapuser Sample1 /pass MyPas$w0rd /out Sample1.keytab /crypto all /ptype KRB5_NT_PRINCIPAL /mapop set   
    ```  

    > [!NOTE]  
    > 同じユーザー アカウントに複数のサービス インスタンスをマップすることはできません。  

3.  .Keytab ファイルを Windows オペレーティング システムが実行されていないホスト コンピューターで/Etc/Krb5.keytab ファイルをマージします。 

#### <a name="additional-references"></a>その他の参照  
[コマンド ライン構文の記号](command-line-syntax-key.md)  
