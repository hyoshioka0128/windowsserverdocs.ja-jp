---
title: "AD FS 2.0 フェデレーション サーバーを移行します。"
description: "Windows Server 2012 R2 への AD FS サーバーの移行についてを説明します。"
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: bef24f79cfa92dfeca1846501f14ebf6d8231f0d
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="migrate-the-ad-fs-20-federation-server-to-ad-fs-on-windows-server-2012-r2"></a>Windows Server 2012 R2 での AD FS への AD FS 2.0 フェデレーション サーバーを移行します。

単一ノード AD FS ファーム、WIF ファーム、または Windows Server 2012 R2 への SQL Server ファームに属している AD FS フェデレーション サーバーを移行するには、次のタスクを実行する必要があります。  
  
1.  [エクスポートし、AD FS 構成データのバックアップ](migrate-ad-fs-fed-server-r2.md#export-and-backup-the-ad-fs-configuration-data)  
  
2.  [Windows Server 2012 R2 フェデレーション サーバー ファームを作成します。](migrate-ad-fs-fed-server-r2.md#create-a-windows-server-2012-r2-federation-server-farm)  
  
3.  [Windows Server 2012 R2 AD FS ファームにインポート元の構成データ](migrate-ad-fs-fed-server-r2.md#import-the-original-configuration-data-into-the-windows-server-2012-r2-ad-fs-farm)  
  
##  <a name="export-and-backup-the-ad-fs-configuration-data"></a>エクスポートし、AD FS 構成データのバックアップ  
 AD FS の構成設定をエクスポートするには、次の手順を実行します。  
  
###  <a name="to-export-service-settings"></a>サービスの設定をエクスポートするには  
  
1.  .Pfx ファイルに次の証明書と秘密キーへのアクセスがあることを確認します。  
  
    -   移行するフェデレーション サーバー ファームで使用される SSL 証明書  
  
    -   サービス通信証明書 (SSL 証明書と異なる場合) に移行するフェデレーション サーバー ファームで使用されています。  
  
    -   サード パーティのトークン署名やトークン暗号化/暗号化解除証明書をすべてに移行するフェデレーション サーバー ファームで使用されています。  
  
SSL 証明書を見つけるには、インターネット インフォメーション サービス (IIS) 管理を開きますコンソールで、選択**既定の Web サイト**左側のウィンドウで [**バインドしています.** **アクション**、ウィンドウの検索と選択、https バインド] をクリックして**編集**、] をクリックし、**ビュー**します。  
  
フェデレーション サービスとその秘密キーを .pfx ファイルで使用される SSL 証明書をエクスポートする必要があります。 詳細については、次を参照してください。[サーバー認証証明書の秘密キー部分のエクスポート](export-the-private-key-portion-of-a-server-authentication-certificate.md)します。  
  
> [!NOTE]
>  Windows Server 2012 R2 での AD FS を実行しているの一部としてデバイス登録サービスを展開する場合は、新しい SSL 証明書を取得する必要があります。詳細については、次を参照してください。[AD FS の SSL 証明書を登録](enroll-an-ssl-certificate-for-ad-fs.md)と[デバイス登録サービスによるフェデレーション サーバーを構成する](configure-a-federation-server-with-device-registration-service.md)します。  
  
トークン署名、トークン暗号化解除および使用されるサービス通信証明書を表示するには、ファイルで使用中のすべての証明書の一覧を作成する次の Windows PowerShell コマンドを実行します。  
  
``` powershell
Get-ADFSCertificate | Out-File “.\certificates.txt”  
 ```  
  
2.  フェデレーション サービス名、フェデレーション サービス表示名、フェデレーション サーバー識別子など、AD FS フェデレーション サービスのプロパティをファイルにエクスポートします。  
  
フェデレーション サービスのプロパティをエクスポートするには、Windows PowerShell を開き、次のコマンドを実行します。 

``` powershell
Get-ADFSProperties | Out-File “.\properties.txt”`.  
``` 

出力ファイルは、次の重要な構成値が表示されます。  
 
|**Get-ADFSProperties によってレポートされるフェデレーション サービスのプロパティ名**|**AD FS 管理コンソールで、フェデレーション サービスのプロパティ名**|
|-----|-----|  
|ホスト名|フェデレーション サービス名|  
|識別子|フェデレーション サービス識別子|  
|DisplayName|フェデレーション サービスの表示名|  
  
3.  アプリケーション構成ファイルをバックアップします。 その他の設定の間では、このファイルにはポリシー データベース接続文字列が含まれています。  
  
アプリケーション構成ファイルをバックアップする必要があります手動でコピーする、`%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config`ファイルをバックアップ サーバー上の安全な場所です。  
  
> [!NOTE]
>  メモ データベース接続文字列のこのファイルの直後にある"policystore connectionstring ="です。 接続文字列は、SQL Server データベースを指定する場合は、フェデレーション サーバーで元の AD FS 構成を復元するときに、値が必要です。  
>   
>  WID 接続文字列の例を次に示します:`“Data Source=\\.\pipe\mssql$microsoft##ssee\sql\query;Initial Catalog=AdfsConfiguration;Integrated Security=True"`します。 SQL Server 接続文字列の例を次に示します:`"Data Source=databasehostname;Integrated Security=True"`します。  
  
4.  AD FS フェデレーション サービス アカウントの ID とこのアカウントのパスワードを記録します。  
  
Id 値を検索するを調べて、**ログとして**の列**AD FS 2.0 Windows サービス**で、**サービス**コンソールを手動でこの値を記録します。  
  
> [!NOTE]
>  スタンドアロン フェデレーション サービスでは、組み込みの NETWORK SERVICE アカウントが使用されます。  この場合、パスワードを保持する必要はありません。  
  
5.  有効な AD FS エンドポイントの一覧をファイルにエクスポートします。  
  
これを行うには、Windows PowerShell を開き、次のコマンドを実行します。 

``` powershell
Get-ADFSEndpoint | Out-File “.\endpoints.txt”`.  
``` 

6.  カスタム要求記述をすべてをファイルにエクスポートします。  
  
これを行うには、Windows PowerShell を開き、次のコマンドを実行します。 

``` powershell
Get-ADFSClaimDescription | Out-File “.\claimtypes.txt”`.  
 ```

7.  Web.config ファイルで構成されている useRelayStateForIdpInitiatedSignOn などのカスタム設定を使っている場合は、参照の Web.config ファイルをバックアップすることを確認します。 仮想パスにマップされたディレクトリからファイルをコピーする**"/adfs/ls"** IIS でします。 既定では、**%systemdrive%\inetpub\adfs\ls**ディレクトリ。  
  
###  <a name="to-export-claims-provider-trusts-and-relying-party-trusts"></a>要求プロバイダー信頼と証明書利用者信頼をエクスポートするには  
  
1.  エクスポート AD FS の要求プロバイダー信頼と証明書利用者の信頼をする必要があります管理者としてログイン (ただし、として、ドメイン管理者ではなく)、フェデレーション サーバーと、次の Windows PowerShell スクリプトを実行にある、**メディア/server_support/adfs** 、Windows Server 2012 R2 のインストール CD のフォルダー:`export-federationconfiguration.ps1`します。  
  
> [!IMPORTANT]
>  エクスポート スクリプトは、次のパラメーターを受け取ります。  
>   
>  -   Export-FederationConfiguration .ps1-Path < string\ > [-ComputerName < string\ >] [-Credential < pscredential\ >] [-Force] [-< securestring\ > CertificatePassword]  
> -   Export-FederationConfiguration .ps1-Path < string\ > [-ComputerName < string\ >] [-Credential < pscredential\ >] [-Force] [-< securestring\ > CertificatePassword] [-RelyingPartyTrustIdentifier < string[] >] [-ClaimsProviderTrustIdentifier < string[] >]  
> -   Export-FederationConfiguration .ps1-Path < string\ > [-ComputerName < string\ >] [-Credential < pscredential\ >] [-Force] [-< securestring\ > CertificatePassword] [-RelyingPartyTrustName < string[] >] [-ClaimsProviderTrustName < string[] >]  
>   
>  **-Relyingpartytrustidentifier < string[] >** - このコマンドレットのみをエクスポート証明書利用者の信頼の識別子が string 配列に指定されています。 既定では、どの証明書利用者信頼もエクスポートしません。 スクリプトをすべてエクスポート RelyingPartyTrustIdentifier、ClaimsProviderTrustIdentifier、RelyingPartyTrustName、および ClaimsProviderTrustName が指定されていない場合、証明書利用者信頼し、要求プロバイダー信頼します。  
>   
>  **-Claimsprovidertrustidentifier < string[] >** -このコマンドレットの識別子が string 配列に指定されている要求プロバイダー信頼のみをエクスポートします。 既定では、どの要求プロバイダー信頼もエクスポートしません。  
>   
>  **-Relyingpartytrustname < string[] >** - このコマンドレットのみをエクスポート証明書利用者の信頼の名前が string 配列に指定されています。 既定では、どの証明書利用者信頼もエクスポートしません。  
>   
>  **-Claimsprovidertrustname < string[] >** -このコマンドレットは名前が string 配列に指定されている要求プロバイダー信頼のみをエクスポートします。 既定では、どの要求プロバイダー信頼もエクスポートしません。  
>   
>  **パス < string\ >** -エクスポートされたファイルが含まれるフォルダーへのパス。  
>   
>  **-ComputerName < string\ >** -STS サーバーのホスト名を指定します。 既定では、ローカル コンピューターです。 Windows Server 2012 R2 の AD FS に AD FS 2.0 または Windows Server 2012 での AD FS を移行する場合は、レガシ AD FS サーバーのホスト名とします。  
>   
>  **-Credential < PSCredential\ >** -この操作を実行するアクセス許可を持つユーザー アカウントを指定します。 既定では、現在のユーザーです。  
>   
>  **-強制**– ユーザーの確認プロンプトではなくするように指定します。  
>   
>  **-Certificatepassword < SecureString\ >** -AD FS 証明書の秘密キーをエクスポートするためのパスワードを指定します。 指定されていない場合は、プライベート キーを使用して、AD FS 証明書をエクスポートする必要がある場合、パスワードのスクリプトが求められます。  
>   
>  **入力**: なし  
>   
>  **出力**: string - このコマンドレットは、エクスポート フォルダーのパスを返します。 返されたオブジェクトを Import-FederationConfiguration にパイプ処理することができます。  
  
###  <a name="to-back-up-custom-attribute-stores"></a>カスタム属性ストアをバックアップするには  
  
1.  Windows Server 2012 R2 で新しい AD FS ファームに維持するすべてのカスタム属性ストアを手動でエクスポートする必要があります。  
  
> [!NOTE]
>  Windows Server 2012 R2 で AD FS に .NET Framework 4.0 または上に基づくカスタム属性ストアが必要です。 指示に従って[Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653)をインストールして .Net Framework 4.5。  
  
次の Windows PowerShell コマンドを実行して AD FS によって使用中のカスタム属性ストアに関する情報を見つけることができます。 

``` powershell
Get-ADFSAttributeStore
```  

アップグレードまたはカスタム属性ストアを移行する手順は異なります。  
  
2.  Windows Server 2012 R2 で新しい AD FS ファームに維持するカスタム属性ストアのすべての .dll ファイルを手動でエクスポートする必要があります。 アップグレードまたはカスタム属性ストアの .dll ファイルを移行する手順は異なります。  
  
##  <a name="create-a-windows-server-2012-r2-federation-server-farm"></a>Windows Server 2012 R2 フェデレーション サーバー ファームを作成します。  
  
1.  フェデレーション サーバーとして機能し、AD FS サーバー役割を追加するコンピューターで Windows Server 2012 R2 オペレーティング システムをインストールします。 詳細については、次を参照してください。 [AD FS 役割サービスをインストール](install-the-ad-fs-role-service.md)します。 新しいフェデレーション サービス、Active Directory フェデレーション サービス構成ウィザードまたは Windows PowerShell を使用して構成します。 詳細についてを参照してください「新しいフェデレーション サーバー ファーム最初のフェデレーション サーバーを構成する"[フェデレーション サーバーを構成する](configure-a-federation-server.md)します。  

この手順を完了すると、中には、この手順に従う必要があります。  
  
-   フェデレーション サービスを構成するためにドメイン管理者特権が必要です。  
  
-   AD FS 2.0 または Windows Server 2012 で AD FS で使用されていたように、同じフェデレーション サービス名 (ファーム名) を使用する必要があります。 同じフェデレーション サービス名を使用しない場合、バックアップした証明書は、構成しようとしている Windows Server 2012 R2 フェデレーション サービスで機能しません。  
  
-   これは、WID または SQL Server のフェデレーション サーバー ファームであるかどうかを指定します。 SQL ファームである場合は、SQL Server データベースの場所とインスタンス名を指定します。  
  
-   AD FS の移行プロセスの準備の一環としてバックアップした SSL サーバー認証証明書を含む、pfx ファイルを提供する必要があります。  
  
-   AD FS 2.0 または Windows Server 2012 ファーム内の AD FS で使用されたサービス アカウントの資格情報を指定する必要があります。  
  
2.  最初のノードを構成すると、新しいファームにノードを追加できます。 詳細についてを参照してください「既存のフェデレーション サーバー ファームにフェデレーション サーバーを追加する」で[フェデレーション サーバーを構成する](configure-a-federation-server.md)します。  
  
##  <a name="import-the-original-configuration-data-into-the-windows-server-2012-r2-ad-fs-farm"></a>Windows Server 2012 R2 AD FS ファームにインポート元の構成データ  
 Windows Server 2012 R2 で実行されている AD FS フェデレーション サーバー ファームがある場合は、これでは、それに元の AD FS 構成データをインポートできます。  
  
1.  インポートするには、その他のカスタム AD FS 証明書を構成、およびを含む外部で登録したトークン署名やトークン暗号化/暗号化解除証明書、およびサービス通信証明書が SSL 証明書と異なる場合。  
  
AD FS 管理コンソールで、次のように選択します。**証明書**します。 各移行の準備中に certificates.txt ファイルにエクスポートした値と比較して、サービス通信の場合、トークン暗号化/暗号化解除、およびトークン署名証明書を確認します。  
  
トークン暗号化解除またはトークン署名証明書を既定の自己署名証明書から外部証明書を変更するには、最初に既定で有効になっている証明書の自動ロール オーバー機能を無効にする必要があります。 これを行うには、次の Windows PowerShell コマンドを使用できます。  
  
``` powershell 
Set-ADFSProperties –AutoCertificateRollover $false  
```  
  
2.  Set-AdfsProperties コマンドレットを使用して AutoCertificateRollover や SSO の有効期間などのカスタムの AD FS サービスの設定を構成します。  
  
3.  AD FS の証明書利用者信頼と要求プロバイダー信頼をインポートする管理者としてログインする必要があります (ただし、として、ドメイン管理者ではなく)、フェデレーション サーバーと、次の Windows PowerShell スクリプトを実行にある Windows Server 2012 R2 のインストール CD の \support\adfs フォルダー。  
  
``` powershell 
import-federationconfiguration.ps1  
```  
  
> [!IMPORTANT]
>  インポート スクリプトは、次のパラメーターを受け取ります。  
>   
>  -  Import-FederationConfiguration .ps1-Path < string\ > [-ComputerName < string\ >] [-Credential < pscredential\ >] [-Force] [-LogPath < string\ >] [-< securestring\ > CertificatePassword]  
> -   Import-FederationConfiguration .ps1-Path < string\ > [-ComputerName < string\ >] [-Credential < pscredential\ >] [-Force] [-LogPath < string\ >] [-< securestring\ > CertificatePassword] [-RelyingPartyTrustIdentifier < string[] >] [-ClaimsProviderTrustIdentifier < string[] >  
> -   Import-FederationConfiguration .ps1-Path < string\ > [-ComputerName < string\ >] [-Credential < pscredential\ >] [-Force] [-LogPath < string\ >] [-< securestring\ > CertificatePassword] [-RelyingPartyTrustName < string[] >] [-ClaimsProviderTrustName < string[] >]  
>   
>  **-Relyingpartytrustidentifier < string[] >** - 証明書利用者の信頼の識別子が string 配列に指定されたコマンドレットのみインポートします。 既定では、どの証明書利用者信頼もインポートしません。 スクリプトがすべてインポートされます RelyingPartyTrustIdentifier、ClaimsProviderTrustIdentifier、RelyingPartyTrustName、および ClaimsProviderTrustName が指定されていない場合、証明書利用者信頼し、要求プロバイダー信頼します。  
>   
>  **-Claimsprovidertrustidentifier < string[] >** -このコマンドレットの識別子が string 配列に指定されている要求プロバイダー信頼のみをインポートします。 既定では、どの要求プロバイダー信頼もインポートしません。  
>   
>  **-Relyingpartytrustname < string[] >** - このコマンドレットのみをインポート証明書利用者の信頼の名前が string 配列に指定されています。 既定では、どの証明書利用者信頼もインポートしません。  
>   
>  **-Claimsprovidertrustname < string[] >** -このコマンドレットは名前が string 配列に指定されている要求プロバイダー信頼のみをインポートします。 既定では、どの要求プロバイダー信頼もインポートしません。  
>   
>  **パス < string\ >** -をインポートする構成ファイルが含まれるフォルダーへのパス。  
>   
>  **-Logpath < string\ >** -インポート ログ ファイルが含まれるフォルダーへのパス。 "Import.log"という名前のログ ファイルは、このフォルダーに作成されます。  
>   
>  **-ComputerName < string\ >** -STS サーバーのホスト名を指定します。 既定では、ローカル コンピューターです。 Windows Server 2012 R2 の AD FS に AD FS 2.0 または Windows Server 2012 での AD FS を移行する場合、このパラメーターはレガシ AD FS サーバーのホスト名に設定する必要があります。  
>   
>  **-Credential < PSCredential\ >**-この操作を実行するアクセス許可を持つユーザー アカウントを指定します。 既定では、現在のユーザーです。  
>   
>  **-強制**– ユーザーの確認プロンプトではなくするように指定します。  
>   
>  **-Certificatepassword < SecureString\ >** -AD FS 証明書の秘密キーをインポートするためのパスワードを指定します。 指定されていない場合は、プライベート キーを使用して、AD FS 証明書をインポートする必要がある場合、パスワードのスクリプトが求められます。  
>   
>  **入力:** string - このコマンドは、入力としてインポート フォルダーのパス。 このコマンドに Export-FederationConfiguration をパイプ処理することができます。  
>   
>  **出力:**なし。  
  
証明書利用者信頼の WSFedEndpoint プロパティの末尾のスペースには、インポート スクリプト エラーを可能性があります。 ここで、インポート前にファイルから、スペースを手動で削除します。 たとえば、これらのエントリには、エラーが発生します。  
  
    ```  
    <URI N="WSFedEndpoint">https://127.0.0.1:444 /</URI>  
    ```  
  
    ```  
    <URI N="WSFedEndpoint">https://myapp.cloudapp.net:83 /</URI>  
    ```  
  
     They must be edited to:  
  
    ```  
    <URI N="WSFedEndpoint">https://127.0.0.1:444/</URI>  
    ```  
  
    ```  
    <URI N="WSFedEndpoint">https://myapp.cloudapp.net:83/</URI>  
    ```  
> [!IMPORTANT]
>  ソース システムでは、Active Directory 要求プロバイダー信頼にカスタム要求規則 (AD FS の既定の規則以外の規則) があれば、これらは移行されません、スクリプトによってします。 これは、Windows Server 2012 R2 に新しい既定値があるためです。 カスタム規則はすべては、新しい Windows Server 2012 R2 ファーム内の Active Directory 要求プロバイダー信頼を手動で追加するでマージする必要があります。  
  
4.  すべてのカスタム AD FS エンドポイントの設定を構成します。 AD FS 管理コンソールで、次のように選択します。**エンドポイント**します。 AD FS の移行の準備中にファイルにエクスポートした有効な AD FS エンドポイントのリストに対して有効な AD FS エンドポイントを確認します。  
  
     \ - と -  
  
     カスタム要求記述をすべてを構成します。 AD FS 管理コンソールで、次のように選択します。**要求記述**します。 AD FS の移行の準備中にファイルにエクスポートした要求記述のリストと照合します AD FS 要求記述のリストを確認します。 カスタム要求記述をすべてのファイルに含まれていますが、AD FS の既定の一覧に含まれていないを追加します。 管理コンソール内の要求識別子は、ファイル内の ClaimType にマップされる注意してください。  
  
5.  インストールし、構成のバックアップしたすべてのカスタム属性ストアです。 管理者は、任意のカスタム属性ストアのバイナリがそれらをポイントする AD FS 構成を更新する前にアップグレードを .NET Framework 4.0 以上を確認します。  
  
6.  レガシ Web.config ファイル パラメーターにマップされるサービス プロパティを構成します。  
  
    -   場合**useRelayStateForIdpInitiatedSignOn**に追加された、 **Web.config**ファイルには、AD FS 2.0 または Windows Sever 2012 ファーム内の AD FS ファームを Windows Server 2012 R2 での AD FS で次のサービス プロパティを構成する必要があります。  
  
        -   Windows Server 2012 R2 の AD FS を含む、 **%systemroot%\ADFS\Microsoft.IdentityServer.Servicehost.exe.config**ファイル。 同じ構文で要素を作成、 **Web.config**ファイルの要素:`<useRelayStateForIdpInitiatedSignOn enabled="true" />`します。 一部としてこの要素を含める**< microsoft.identityserver.Web >**のセクションで、 **Microsoft.IdentityServer.Servicehost.exe.config**ファイル。  
  
    -   場合**< persistIdentityProviderInformation が有効になっている =「true & #124; false」lifetimeInDays =「90」enablewhrPersistence =「true & #124; false」/\ >**に追加された、 **Web.config**ファイルには、AD FS 2.0 または Windows Sever 2012 ファーム内の AD FS での AD FS ファームを Windows Server 2012 R2 では、次のサービス プロパティを構成する必要があります。  
  
        1.  Windows Server 2012 R2 での AD FS で次の Windows PowerShell コマンドを実行します:`Set-AdfsWebConfig –HRDCookieEnabled –HRDCookieLifetime`します。  
  
    -   場合**< シングル サインオンを有効になっている =「true & #124; false」/\ >**に追加された、 **Web.config** 、ファイルの AD fs 2.0 または Windows Sever 2012 ファーム内の AD FS は Windows Server 2012 R2 ファーム内の AD FS で追加のサービス プロパティを設定する必要はありません。 シングル サインオンが AD fs ファームを Windows Server 2012 R2 で既定で有効にします。  
  
    -   LocalAuthenticationTypes 設定に追加された場合、 **Web.config**ファイルには、AD FS 2.0 または Windows Sever 2012 ファーム内の AD FS ファームを Windows Server 2012 R2 での AD FS で次のサービス プロパティを構成する必要があります。  
  
        -   Integrated、Forms、TlsClient、Basic Transform の一覧には、Windows Server 2012 R2 で AD FS にはフェデレーション サービスと両方プロキシ認証の種類をサポートするグローバル認証ポリシーの設定。 AD fs 管理スナップインの下でこれらの設定を構成することができます、**認証ポリシー**します。  
  
 元の構成データをインポートした後、必要に応じて、AD FS のサインイン ページをカスタマイズできます。 詳細については、次を参照してください。 [AD FS サインイン ページのカスタマイズ](../operations/AD-FS-Customization-in-Windows-Server-2016.md)します。  
  
## <a name="next-steps"></a>次の手順
 [Windows Server 2012 R2 への Active Directory フェデレーション サービスの役割サービスを移行します。](migrate-ad-fs-service-role-to-windows-server-r2.md)   
 [AD FS フェデレーション サーバーの移行の準備](prepare-migrate-ad-fs-server-r2.md)   
 [AD FS フェデレーション サーバー プロキシの移行](migrate-fed-server-proxy-r2.md)   
 [Windows Server 2012 R2 への AD FS の移行の検証](verify-ad-fs-migration.md)