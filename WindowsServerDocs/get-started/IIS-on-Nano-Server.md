---
title: Nano Server の IIS
description: Nano Server 上での IIS の構成の詳細
ms.prod: windows-server-threshold
ms.service: na
manager: DonGill
ms.technology: server-nano
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 09/06/2017
ms.assetid: 16984724-2d77-4d7b-9738-3dff375ed68c
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: 54c8d05c028cbca364b6a46052d12cdcb12c01b0
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66443615"
---
# <a name="iis-on-nano-server"></a>Nano Server の IIS

>適用先:Windows Server 2016

> [!IMPORTANT]
> Windows Server バージョン 1709 以降、Nano Server は[コンテナー基本 OS イメージ](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image)としてのみ提供されます。 その意味については、「[Nano Server に加えられる変更](nano-in-semi-annual-channel.md)」をご覧ください。 

-Package パラメーターと Microsoft-NanoServer-IIS-Package を使用して、Nano Server にインターネット インフォメーション サービス (IIS) のサーバーの役割をインストールできます。 パッケージのインストールなど、Nano Server の構成の詳細については、「[Nano Server のインストール](Getting-Started-with-Nano-Server.md)」を参照してください。  

Nano Server の今回のリリースでは、次の IIS 機能を使用できます。  

|機能|既定で有効|  
|-----------|----------------------|  
|**HTTP 共通機能**||  
|既定のドキュメント|○|  
|ディレクトリの参照|○|  
|HTTP エラー|○|  
|静的コンテンツ|○|  
|HTTP リダイレクト||  
|**正常性と診断**||  
|HTTP ログ|○|  
|カスタム ログ||  
|要求監視||  
|トレース||  
|**[パフォーマンス]**||  
|静的コンテンツの圧縮|○|  
|動的コンテンツの圧縮||  
|**セキュリティ**||  
|要求のフィルタリング|○|  
|[基本認証]||  
|クライアント証明書マッピング認証||  
|ダイジェスト認証||  
|IIS クライアント証明書マッピング認証||  
|IP とドメインの制限||  
|URL 承認||  
|Windows 認証||  
|**アプリケーションの開発**||  
|アプリケーションの初期化||  
|CGI||  
|ISAPI 拡張機能||  
|ISAPI フィルター||  
|サーバー側インクルード||  
|WebSocket プロトコル||  
|**管理ツール**||  
|Windows PowerShell 用 IISAdministration モジュール|○|  

その他の IIS (を使用して ASP.NET、PHP、および Java) などの他の構成に関する記事の一連の関連コンテンツを公開する[ http://iis.net/learn](http://iis.net/learn)します。  

## <a name="installing-iis-on-nano-server"></a>Nano Server での IIS のインストール  
このサーバーの役割は、オフライン (Nano Server が停止した状態) でもオンライン (Nano Server が実行中) でもインストールできますが、オフライン インストールをお勧めします。  

オフライン インストールの場合は、次の例に示すように、New-NanoServerImage の -Packages パラメーターを使用してパッケージを追加します。  

`New-NanoServerImage -Edition Standard -DeploymentType Guest -MediaPath f:\ -BasePath .\Base -TargetPath .\Nano1.vhd -ComputerName Nano1 -Package Microsoft-NanoServer-IIS-Package`  

既存の VHD ファイルがある場合は、DISM.exe を使用して IIS をオフラインでインストールできます。これには、VHD をマウントし、**Add-Package** オプションを使用します。   
次の例の手順では、BasePath オプションで指定されたディレクトリから実行していることを前提としています。このディレクトリは、New-NanoServerImage の実行後に作成されました。  

1.  mkdir mountdir
2.  .\Tools\dism.exe /Mount-Image /ImageFile:.\NanoServer.vhd /Index:1 /MountDir:.\mountdir
3.  .\Tools\dism.exe /Add-Package /PackagePath:.\packages\Microsoft-NanoServer-IIS-Package.cab /Image:.\mountdir
4.  .\Tools\dism.exe /Add-Package /PackagePath:.\packages\en-us\Microsoft-NanoServer-IIS-Package_en-us.cab /Image:.\mountdir
5.  .\Tools\dism.exe /Unmount-Image /MountDir:.\MountDir /Commit


> [!NOTE]  
> 手順 4. で言語パックがインストールされます。この例では、EN-US をインストールしています。  

この時点で、IIS がインストールされた Nano Server を起動できます。  

### <a name="installing-iis-on-nano-server-online"></a>Nano Server での IIS のオンライン インストール  
サーバーの役割のインストールはオフラインで実行することをお勧めしますが、コンテナー シナリオでは (Nano Server の実行中に) オンラインでインストールすることが必要になる場合があります。 これを行うには、次の手順に従います。  

1.  Packages フォルダーをインストール メディアから実行中の Nano Server (たとえば、C:\packages) にローカルにコピーします。  

2.  別のコンピューター上に新しい Unattend.xml ファイルを作成し、Nano Server にコピーします。 この XML の内容をコピーして、作成した XML ファイルに貼り付けることができます。  



```  

    <unattend xmlns="urn:schemas-microsoft-com:unattend">  
    <servicing>  
        <package action="install">  
            <assemblyIdentity name="Microsoft-NanoServer-IIS-Package" version="10.0.14393.0" processorArchitecture="amd64" publicKeyToken="31bf3856ad364e35" language="neutral" />  
            <source location="c:\packages\Microsoft-NanoServer-IIS-Package.cab" />  
        </package>  
        <package action="install">  
            <assemblyIdentity name="Microsoft-NanoServer-IIS-Package" version="10.0.14393.0" processorArchitecture="amd64" publicKeyToken="31bf3856ad364e35" language="en-US" />  
            <source location="c:\packages\en-us\Microsoft-NanoServer-IIS-Package_en-us.cab" />  
        </package>  
    </servicing>  
    <cpi:offlineImage cpi:source="" xmlns:cpi="urn:schemas-microsoft-com:cpi" />  
</unattend>  
```  




3. 作成 (またはコピー) した新しい XML ファイルを編集して、"C:\packages" を、Packages の内容をコピーしたディレクトリに変更します。  

4. 新しく作成した XML ファイルがあるディレクトリに移動し、以下を実行します。  

   **dism /online /apply-unattend:.\unattend.xml**  


5. 以下を実行して、IIS パッケージと関連する言語パックが正しくインストールされていることを確認します。  

   **dism/online/get-packages**  

   表示する必要があります"Package Identity:Microsoft NanoServer IIS パッケージ ~ 31bf3856ad364e35 ~ amd64 ~ ~ 10.0.14393.1000"2 回一覧表示、1 回 Release type:言語パックと Release type:Feature Pack。  

6. **net start w3svc** を実行するか、Nano Server を再起動して、W3SVC サービスを開始します。  

## <a name="starting-iis"></a>IIS の起動  
IIS がインストールされ実行された状態になると、Web 要求を処理できるようになります。 http://\<Nano Server の IP アドレス> で既定の IIS Web ページを参照することで、IIS が実行されていることを確認します。 物理コンピューターでは、回復コンソールを使用して IP アドレスを特定できます。 仮想マシンでは、Windows PowerShell プロンプトを使用して以下を実行することで、IP アドレスを取得できます。  

`Get-VM -name <VM name> | Select -ExpandProperty networkadapters | select IPAddresses`  

既定の IIS Web ページにアクセスできない場合は、Nano Server の **c:\inetpub** ディレクトリを探して、IIS のインストールを再確認します。  

## <a name="enabling-and-disabling-iis-features"></a>IIS 機能の有効化と無効化  
IIS の役割をインストールすると、多くの IIS 機能が既定で有効になります (このトピックの「Nano Server の IIS の概要」セクションの表を参照)。 DISM.exe を使用すると、追加の機能を有効 (または無効) にすることができます。

IIS の各機能は、構成要素のセットとして存在します。 たとえば、Windows 認証の機能は、次の要素で構成されています。  

|セクション|構成要素|  
|-----------|--------------------------|  
|`<globalModules>`|`<add name="WindowsAuthenticationModule" image="%windir%\System32\inetsrv\authsspi.dll`|  
|`<modules>`|`<add name="WindowsAuthenticationModule" lockItem="true" \/>`|  
|`<windowsAuthentication>`|`<windowsAuthentication enabled="false" authPersistNonNTLM\="true"><providers><add value="Negotiate" /><add value="NTLM" /><br /></providers><br /></windowsAuthentication>`|  

IIS のすべてのサブ機能はこのトピックの付録 1 に記載されており、それに対応する構成要素は付録 2 に記載されています。  


### <a name="example-installing-windows-authentication"></a>例: Windows 認証のインストール  

1.  Nano Server で Windows PowerShell リモート セッション コンソールを開きます。  

2.  `DISM.exe` を使用して Windows 認証モジュールをインストールします。

    ```
    dism /Enable-Feature /online /featurename:IIS-WindowsAuthentication /all
    ```

    `/all` スイッチを使用すると、選択した機能が依存しているすべての機能がインストールされます。

### <a name="example-uninstalling-windows-authentication"></a>例: Windows 認証のアンインストール  

1.  Nano Server で Windows PowerShell リモート セッション コンソールを開きます。  

2.  `DISM.exe` を使用して Windows 認証モジュールをアンインストールします。

    ```
    dism /Disable-Feature /online /featurename:IIS-WindowsAuthentication
    ```

## <a name="other-common-iis-configuration-tasks"></a>その他の一般的な IIS 構成タスク  
**Web サイトの作成**  

次のコマンドレットを使用します。  

`PS D:\> New-IISSite -Name TestSite -BindingInformation "*:80:TestSite" -PhysicalPath c:\test`  

次に `Get-IISSite` を実行すると、サイトの状態を確認できます (Web サイトの名前、ID、状態、物理パス、バインドが返されます)。  

**Web サイトの削除**  

`Remove-IISSite -Name TestSite -Confirm:$false` を実行します。  

**仮想ディレクトリの作成**  

Get-IISServerManager によって返された IISServerManager オブジェクトを使用して、仮想ディレクトリを作成できます。これにより、NET Microsoft.Web.Administration.ServerManager API が公開されます。 この例では、次のコマンドがサイト コレクションの "Default Web Site" 要素とアプリケーション セクションのルート アプリケーション要素 ("/") にアクセスします。 その後、そのアプリケーション要素の VirtualDirectories コレクションの Add() メソッドを呼び出して、新しいディレクトリを作成します。  

```  
PS C:\> $sm = Get-IISServerManager  
PS C:\> $sm.Sites["Default Web Site"].Applications["/"].VirtualDirectories.Add("/DemoVirtualDir1", "c:\test\virtualDirectory1")  
PS C:\> $sm.Sites["Default Web Site"].Applications["/"].VirtualDirectories.Add("/DemoVirtualDir2", "c:\test\virtualDirectory2")  
PS C:\> $sm.CommitChanges()  
```  

**アプリケーション プールの作成**  

同様に、Get-IISServerManager を使用してアプリケーション プールを作成できます。  

```  
PS C:\> $sm = Get-IISServerManager  
PS C:\> $sm.ApplicationPools.Add("DemoAppPool")  
```  

**HTTPS と証明書を構成します。**  

次の例に示すように、Certoc.exe ユーティリティを使用して証明書をインポートします。これは、Nano Server 上の Web サイトの HTTPS の構成を示します。  

1.  Nano Server が実行されていない別のコンピューターで、(独自の証明書名とパスワードを使用して) 証明書を作成し、c:\temp\test.pfx にエクスポートします。  

    `$newCert = New-SelfSignedCertificate -DnsName "www.foo.bar.com" -CertStoreLocation cert:\LocalMachine\my`  

    `$mypwd = ConvertTo-SecureString -String "YOUR_PFX_PASSWD" -Force -AsPlainText`  

    `Export-PfxCertificate -FilePath c:\temp\test.pfx -Cert $newCert -Password $mypwd`  

2.  この test.pfx ファイルを Nano Server コンピューターにコピーします。  

3.  Nano Server で、次のコマンドを使用して証明書を "マイ" ストアにインポートします。  

    **certoc.exe-importpfx-p YOUR_PFX_PASSWD、c:\temp\test.pfx**  

4.  `Get-ChildItem Cert:\LocalMachine\my` を使用して、この新しい証明書の拇印 (この例では 61E71251294B2A7BB8259C2AC5CF7BA622777E73) を取得します。  

5.  次の Windows PowerShell コマンドを使用して、既定の Web サイト (またはバインドの追加先にしたい任意の Web サイト) に HTTPS バインドを追加します。  

    ```  
    $certificate = get-item Cert:\LocalMachine\my\61E71251294B2A7BB8259C2AC5CF7BA622777E73  
    # Use your actual thumbprint instead of this example  
    $hash = $certificate.GetCertHash()  

    Import-Module IISAdministration  
    $sm = Get-IISServerManager  
    $sm.Sites["Default Web Site"].Bindings.Add("*:443:", $hash, "My", "0")    # My is the certificate store name  
    $sm.CommitChanges()  
    ```  

    この構文を使用して特定のホスト名と Server Name Indication (SNI) を使用することもできます。 `$sm.Sites["Default Web Site"].Bindings.Add("*:443:www.foo.bar.com", $hash, "My", "Sni".`  

## <a name="appendix-1-list-of-iis-sub-features"></a>付録 1:IIS サブ機能の一覧

- IIS-WebServer
- IIS-CommonHttpFeatures
- IIS-StaticContent
- IIS-DefaultDocument
- IIS-DirectoryBrowsing
- IIS-HttpErrors
- IIS-HttpRedirect
- IIS-ApplicationDevelopment
- IIS-CGI
- IIS-ISAPIExtensions
- IIS-ISAPIFilter
- IIS-ServerSideIncludes
- IIS-WebSockets
- IIS-ApplicationInit
- IIS-Security
- IIS-BasicAuthentication
- IIS-WindowsAuthentication
- IIS-DigestAuthentication
- IIS-ClientCertificateMappingAuthentication
- IIS-IISCertificateMappingAuthentication
- IIS-URLAuthorization
- IIS-RequestFiltering
- IIS-IPSecurity
- IIS-CertProvider
- IIS-Performance
- IIS-HttpCompressionStatic
- IIS-HttpCompressionDynamic
- IIS-HealthAndDiagnostics
- IIS-HttpLogging
- IIS-LoggingLibraries
- IIS-RequestMonitor
- IIS-HttpTracing
- IIS-CustomLogging

## <a name="appendix-2-elements-of-http-features"></a>付録 2: HTTP 機能の要素  
IIS の各機能は、構成要素のセットとして存在します。 この付録では、Nano Server の今回のリリースに含まれるすべての機能の構成要素の一覧を示します。  

### <a name="common-http-features"></a>一般的な HTTP 機能  
**既定のドキュメント**  

|セクション|構成要素|  
|----------------|--------------------------|  
|`<globalModules>`|`<add name="DefaultDocumentModule" image="%windir%\System32\inetsrv\defdoc.dll" />`|  
|`<modules>`|`<add name="DefaultDocumentModule" lockItem="true" />`|  
|`<handlers>`|`<add name="StaticFile" path="*" verb="*" modules="DefaultDocumentModule" resourceType="EiSecther" requireAccess="Read" />`|  
|`<defaultDocument>`|`<defaultDocument enabled="true"><br /><files><br /> <add value="Default.htm" /><br />        <add value="Default.asp" /><br />        <add value="index.htm" /><br />        <add value="index.html" /><br />        <add value="iisstart.htm" /><br />    </files><br /></defaultDocument>`|  

`StaticFile <handlers>` エントリが既に存在する場合は、単に "DefaultDocumentModule" を \<modules> 属性にコンマで区切って追加します。  

**ディレクトリの参照**  

|セクション|構成要素|  
|----------------|--------------------------|   
|`<globalModules>`|`<add name="DirectoryListingModule" image="%windir%\System32\inetsrv\dirlist.dll" />`|  
|`<modules>`|`<add name="DirectoryListingModule" lockItem="true" />`|  
|`<handlers>`|`<add name="StaticFile" path="*" verb="*" modules="DirectoryListingModule" resourceType="Either" requireAccess="Read" />`|  

`StaticFile <handlers>` エントリが既に存在する場合は、単に "DirectoryListingModule" を \<modules> 属性にコンマで区切って追加します。  

**HTTP エラー**  

|セクション|構成要素|  
|----------------|--------------------------|   
|`<globalModules>`|`<add name="CustomErrorModule" image="%windir%\System32\inetsrv\custerr.dll" />`|  
|`<modules>`|`<add name="CustomErrorModule" lockItem="true" />`|  
|`<httpErrors>`|`<httpErrors lockAttributes="allowAbsolutePathsWhenDelegated,defaultPath"><br />    <error statusCode="401"    prefixLanguageFilePath="%SystemDrive%\inetpub\custerr" path="401.htm" ><br />    <error statusCode="403" prefixLanguageFilePath="%SystemDrive%\inetpub\custerr" path="403.htm" /><br />    <error statusCode="404" prefixLanguageFilePath="%SystemDrive%\inetpub\custerr" path="404.htm" /><br />    <error statusCode="405" prefixLanguageFilePath="%SystemDrive%\inetpub\custerr" path="405.htm" /><br />    <error statusCode="406" prefixLanguageFilePath="%SystemDrive%\inetpub\custerr" path="406.htm" /><br />    <error statusCode="412" prefixLanguageFilePath="%SystemDrive%\inetpub\custerr" path="412.htm" /><br />    <error statusCode="500" prefixLanguageFilePath="%SystemDrive%\inetpub\custerr" path="500.htm" /><br />    <error statusCode="501" prefixLanguageFilePath="%SystemDrive%\inetpub\custerr" path="501.htm" /><br />    <error statusCode="502" prefixLanguageFilePath="%SystemDrive%\inetpub\custerr" path="502.htm" /><br /></httpErrors>`|  

**静的コンテンツ**  

|セクション|構成要素|  
|----------------|--------------------------|  
|`<globalModules>`|`<add name="StaticFileModule" image="%windir%\System32\inetsrv\static.dll" />`|  
|`<modules>`|`<add name="StaticFileModule" lockItem="true" />`|  
|`<handlers>`|`<add name="StaticFile" path="*" verb="*" modules="StaticFileModule" resourceType="Either" requireAccess="Read" />`|  

`StaticFile \<handlers>` エントリが既に存在する場合は、単に "StaticFileModule" を \<modules> 属性にコンマで区切って追加します。  

**HTTP リダイレクト**  

|セクション|構成要素|  
|----------------|--------------------------|    
|`<globalModules>`|`<add name="HttpRedirectionModule" image="%windir%\System32\inetsrv\redirect.dll" />`|  
|`<modules>`|`<add name="HttpRedirectionModule" lockItem="true" />`|  
|`<httpRedirect>`|`<httpRedirect enabled="false" />`|  

### <a name="health-and-diagnostics"></a>正常性と診断  
**HTTP ログ**  

|セクション|構成要素|  
|----------------|--------------------------|   
|`<globalModules>`|`<add name="HttpLoggingModule" image="%windir%\System32\inetsrv\loghttp.dll" />`|  
|`<modules>`|`<add name="HttpLoggingModule" lockItem="true" />`|  
|`<httpLogging>`|`<httpLogging dontLog="false" />`|  

**カスタム ログ**  

|セクション|構成要素|  
|----------------|--------------------------|  
|`<globalModules>`|`<add name="CustomLoggingModule" image="%windir%\System32\inetsrv\logcust.dll" />`|  
|`<modules>`|`<add name="CustomLoggingModule" lockItem="true" />`|  

**要求監視**  

|セクション|構成要素|  
|----------------|--------------------------|  
|`<globalModules>`|`<add name="RequestMonitorModule" image="%windir%\System32\inetsrv\iisreqs.dll" />`|  

**トレース**  

|セクション|構成要素|  
|----------------|--------------------------|  
|`<globalModules>`|`<add name="TracingModule" image="%windir%\System32\inetsrv\iisetw.dll" \/><br /><add name="FailedRequestsTracingModule" image="%windir%\System32\inetsrv\iisfreb.dll" />`|  
|`<modules>`|`<add name="FailedRequestsTracingModule" lockItem="true" />`|  
|`<traceProviderDefinitions>`|`<traceProviderDefinitions><br />    <add name="WWW Server" guid\="{3a2a4e84-4c21-4981-ae10-3fda0d9b0f83}"><br />        <areas><br />            <clear /><br />            <add name="Authentication" value="2" /><br />            <add name="Security" value="4" /><br />            <add name="Filter" value="8" /><br />            <add name="StaticFile" value="16" /><br />            <add name="CGI" value="32" /><br />            <add name="Compression" value="64" /><br />            <add name="Cache" value="128" /><br />            <add name="RequestNotifications" value="256" /><br />            <add name="Module" value="512" /><br />            <add name="FastCGI" value="4096" /><br />            <add name="WebSocket" value="16384" /><br />        </areas><br />    </add><br />    <add name="ISAPI Extension" guid="{a1c2040e-8840-4c31-ba11-9871031a19ea}"><br />        <areas><br />            <clear /><br />        </areas><br />    </add><br /></traceProviderDefinitions>`|  

### <a name="performance"></a>パフォーマンス  
**静的コンテンツの圧縮**  

|セクション|構成要素|  
|----------------|--------------------------|  
|`<globalModules>`|`<add name="StaticCompressionModule" image="%windir%\System32\inetsrv\compstat.dll" />`|  
|`<modules>`|`<add name="StaticCompressionModule" lockItem="true" />`|  
|`<httpCompression>`|`<httpCompression directory="%SystemDrive%\inetpub\temp\IIS Temporary Compressed Files"><br />    <scheme name="gzip" dll="%Windir%\system32\inetsrv\gzip.dll" /><br />   <staticTypes><br />        <add mimeType="text/*" enabled="true" /><br />        <add mimeType="message/*" enabled="true" /><br />        <add mimeType="application/javascript" enabled="true" \/><br />        <add mimeType="application/atom+xml" enabled="true" /><br />        <add mimeType="application/xaml+xml" enabled="true" /><br />        <add mimeType="\*\*" enabled="false" /><br />    </staticTypes><br /></httpCompression>`|  

**動的なコンテンツ圧縮**  

|セクション|構成要素|  
|-----------|--------------------------|  
|`<globalModules>`|`<add name="DynamicCompressionModule" image="%windir%\System32\inetsrv\compdyn.dll" />`|  
|`<modules>`|`<add name="DynamicCompressionModule" lockItem="true" />`|  
|`<httpCompression>`|`<httpCompression directory\="%SystemDrive%\inetpub\temp\IIS Temporary Compressed Files"><br />    <scheme name="gzip" dll="%Windir%\system32\inetsrv\gzip.dll" \/><br />    \<dynamicTypes><br />        <add mimeType="text/*" enabled="true" \/><br />        <add mimeType="message/*" enabled="true" /><br />        <add mimeType="application/x-javascript" enabled="true" /><br />        <add mimeType="application/javascript" enabled="true" /><br />        <add mimeType="*/*" enabled="false" /><br />    <\/dynamicTypes><br /></httpCompression>`|  

### <a name="security"></a>セキュリティ  
**要求のフィルタ リング**  


|       セクション        |                                                                                                                                        構成要素                                                                                                                                        |
|----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  `<globalModules>`   |                                                                                                        `<add name="RequestFilteringModule" image="%windir%\System32\inetsrv\modrqflt.dll" />`                                                                                                        |
|     `<modules>`      |                                                                                                                       `<add name="RequestFilteringModule" lockItem="true" />`                                                                                                                        |
| \`<requestFiltering> | `<requestFiltering><br />    <fileExtensions allowUnlisted="true" applyToWebDAV="true" /><br />    <verbs allowUnlisted="true" applyToWebDAV="true" /><br />    <hiddenSegments applyToWebDAV="true"><br />        <add segment="web.config" /><br />    </hiddenSegments><br /></requestFiltering>` |

**基本認証**  

|セクション|構成要素|  
|----------------|--------------------------|   
|`<globalModules>`|`<add name="BasicAuthenticationModule" image="%windir%\System32\inetsrv\authbas.dll" />`|  
|`<modules>`|`<add name="WindowsAuthenticationModule" lockItem="true" />`|  
|`<basicAuthentication>`|`<basicAuthentication enabled="false" />`|  

**クライアント証明書マッピング認証**  

|セクション|構成要素|  
|----------------|--------------------------|  
|`<globalModules>`|`<add name="CertificateMappingAuthentication" image="%windir%\System32\inetsrv\authcert.dll" />`|  
|`<modules>`|`<add name="CertificateMappingAuthenticationModule" lockItem="true" />`|  
|`<clientCertificateMappingAuthentication>`|`<clientCertificateMappingAuthentication enabled="false" />`|  

**ダイジェスト認証**  

|セクション|構成要素|  
|----------------|--------------------------|  
|`<globalModules>`|`<add name="DigestAuthenticationModule" image="%windir%\System32\inetsrv\authmd5.dll" />`|  
|`<modules>`|`<add name="DigestAuthenticationModule" lockItem="true" />`|  
|`<other>`|`<digestAuthentication enabled="false" />`|  

**IIS クライアント証明書マッピング認証**  


|                  セクション                   |                                         構成要素                                         |
|--------------------------------------------|--------------------------------------------------------------------------------------------------------|
|             `<globalModules>`              | `<add name="CertificateMappingAuthenticationModule" image="%windir%\System32\inetsrv\authcert.dll" />` |
|                `<modules>`                 |               `<add name="CertificateMappingAuthenticationModule" lockItem="true" `/>\`                |
| `<clientCertificateMappingAuthentication>` |                      `<clientCertificateMappingAuthentication enabled="false" />`                      |

**IP およびドメインの制限**  

|セクション|構成要素|  
|----------------|--------------------------|  
|`<globalModules>`|```<add name="IpRestrictionModule" image="%windir%\System32\inetsrv\iprestr.dll" /><br /><add name="DynamicIpRestrictionModule" image="%windir%\System32\inetsrv\diprestr.dll" />```|  
|`<modules>`|`<add name="IpRestrictionModule" lockItem="true" \/><br /><add name="DynamicIpRestrictionModule" lockItem="true" \/>`|  
|`<ipSecurity>`|`<ipSecurity allowUnlisted="true" />`|  

**URL 承認**  

|セクション|構成要素|  
|----------------|--------------------------|  
|`<globalModules>`|`<add name="UrlAuthorizationModule" image="%windir%\System32\inetsrv\urlauthz.dll" />`|  
|`<modules>`|`<add name="UrlAuthorizationModule" lockItem="true" />`|  
|`<authorization>`|`<authorization><br />    <add accessType="Allow" users="*" /><br /></authorization>`|  

**Windows 認証**  

|セクション|構成要素|  
|----------------|--------------------------|    
|`<globalModules>`|`<add name="WindowsAuthenticationModule" image="%windir%\System32\inetsrv\authsspi.dll" />`|  
|`<modules>`|`<add name="WindowsAuthenticationModule" lockItem="true" />`|  
|`<windowsAuthentication>`|`<windowsAuthentication enabled="false" authPersistNonNTLM\="true"><br />    <providers><br />        <add value="Negotiate" /><br />        <add value="NTLM" /><br />    <\providers><br /><\windowsAuthentication><windowsAuthentication enabled="false" authPersistNonNTLM\="true"><br />    <providers><br />        <add value="Negotiate" /><br />        <add value="NTLM" /><br />    <\/providers><br /><\/windowsAuthentication>`|  

### <a name="application-development"></a>アプリケーションの開発  
**アプリケーションの初期化**  

|セクション|構成要素|  
|----------------|--------------------------|  
|`<globalModules>`|`<add name="ApplicationInitializationModule" image="%windir%\System32\inetsrv\warmup.dll" />`|  
|`<modules>`|`<add name="ApplicationInitializationModule" lockItem="true" />`|  

**CGI**  

|セクション|構成要素|  
|----------------|--------------------------|  
|`<globalModules>`|`<add name="CgiModule" image="%windir%\System32\inetsrv\cgi.dll" /><br /><add name="FastCgiModule" image="%windir%\System32\inetsrv\iisfcgi.dll" />`|  
|`<modules>`|`<add name="CgiModule" lockItem="true" /><br /><add name="FastCgiModule" lockItem="true" />`|  
|`<handlers>`|`<add name="CGI-exe" path="*.exe" verb="\*" modules="CgiModule" resourceType="File" requireAccess="Execute" allowPathInfo="true" />`|  

**ISAPI 拡張機能**  

|セクション|構成要素|  
|----------------|--------------------------|    
|`<globalModules>`|`<add name="IsapiModule" image="%windir%\System32\inetsrv\isapi.dll" />`|  
|`<modules>`|`<add name="IsapiModule" lockItem="true" />`|  
|`<handlers>`|`<add name="ISAPI-dll" path="*.dll" verb="*" modules="IsapiModule" resourceType="File" requireAccess="Execute" allowPathInfo="true" />`|  

**ISAPI フィルター**  

|セクション|構成要素|  
|----------------|--------------------------|    
|`<globalModules>`|`<add name="IsapiFilterModule" image="%windir%\System32\inetsrv\filter.dll" />`|  
|`<modules>`|`<add name="IsapiFilterModule" lockItem="true" />`|  

**サーバー側インクルードします。**  

|セクション|構成要素|  
|----------------|--------------------------|  
|`<globalModules>`|<`add name="ServerSideIncludeModule" image="%windir%\System32\inetsrv\iis_ssi.dll" />`|  
|`<modules>`|`<add name="ServerSideIncludeModule" lockItem="true" />`|  
|`<handlers>`|`<add name="SSINC-stm" path="*.stm" verb="GET,HEAD,POST" modules="ServerSideIncludeModule" resourceType="File" \/><br /><add name="SSINC-shtm" path="*.shtm" verb="GET,HEAD,POST" modules="ServerSideIncludeModule" resourceType="File" /><br /><add name="SSINC-shtml" path="*.shtml" verb="GET,HEAD,POST" modules="ServerSideIncludeModule" resourceType="File" />`|  
|`<serverSideInclude>`|`<serverSideInclude ssiExecDisable="false" />`|  

**WebSocket プロトコル**  

|セクション|構成要素|  
|----------------|--------------------------|    
|`<globalModules>`|`<add name="WebSocketModule" image="%windir%\System32\inetsrv\iiswsock.dll" />`|  
|`<modules>`|`<add name="WebSocketModule" lockItem="true" />`|  