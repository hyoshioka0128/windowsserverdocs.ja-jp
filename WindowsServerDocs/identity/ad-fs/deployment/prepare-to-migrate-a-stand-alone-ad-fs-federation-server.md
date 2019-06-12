---
title: スタンドアロン AD FS フェデレーション サーバーの移行を準備します。
description: スタンドアロン AD FS サーバーを Windows Server 2012 に移行するための準備について説明します。
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4d2b8a9c35b106a237b47d1bd062026469af59a0
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444480"
---
#  <a name="prepare-to-migrate-a-stand-alone-ad-fs-federation-server-or-a-single-node-ad-fs-farm"></a>スタンドアロン AD FS フェデレーション サーバーまたは単一ノード AD FS ファームの移行の準備  
 
(同じサーバーの移行) の移行の準備にスタンドアロン AD FS 2.0 フェデレーション サーバーまたは Windows Server 2012 では、単一ノード AD FS ファームをエクスポートしてこのサーバーから AD FS 構成データをバックアップします。  
  
AD FS の構成データをエクスポートするには、次の作業を実行します。  
  
-   [ステップ 1: サービス設定のエクスポート](#step-1-export-service-settings)  
  
-   [手順 2:要求プロバイダー信頼をエクスポートします。](#step-2-export-claims-provider-trusts)  
  
-   [手順 3:証明書利用者信頼をエクスポートします。](#step-3-export-relying-party-trusts)  
  
-   [手順 4:カスタム属性ストアをバックアップします。](#step-4-back-up-custom-attribute-stores)  
  
-   [手順 5:Web ページのカスタマイズをバックアップします。](#step-5-back-up-webpage-customizations)  
  
## <a name="step-1-export-service-settings"></a>手順 1:サービスの設定をエクスポートする  
 サービスの設定をエクスポートするには、次の手順を実行します。  
  
### <a name="to-export-service-settings"></a>サービスの設定をエクスポートするには  
  
1.  フェデレーション サービスによって使用される SSL 証明書の証明書サブジェクト名と拇印の値を記録します。 SSL 証明書を検索するには、インターネット インフォメーション サービス (IIS) 管理コンソールを開き、左ウィンドウで **[既定の Web サイト]** を選択します。 **[操作]** **アクション**ペイン、検索、および https バインドを選択します をクリックして**編集**、 をクリックし、**ビュー**します。  
  
> [!NOTE]
>  オプションで、フェデレーション サービスによって使用される SSL 証明書とその秘密キーを .pfx ファイルにエクスポートすることもできます。 詳細については、[サーバー認証証明書の秘密キー部分のエクスポートに関するページ](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md)を参照してください。  
>   
>  SSL 証明書は、ローカル コンピューターの [個人] 証明書ストアに格納されており、オペレーティング システムをアップグレードしても保持されます。したがって、SSL 証明書のエクスポートは省略可能です。  
  
2. AD FS サービス通信証明書、トークン暗号化解除証明書、およびトークン署名証明書の構成を記録します。  使用されているすべての証明書を表示するには、Windows PowerShell を開き、コマンド `PSH:>add-pssnapin “Microsoft.adfs.powershell”`を実行して、AD FS コマンドレットを Windows PowerShell セッションに追加します。 その後、コマンド `PSH:>Get-ADFSCertificate | Out-File “.\certificates.txt”` を実行して、使用中のすべての証明書の一覧をファイルに作成します。  
  
> [!NOTE]
>  オプションで、内部生成されない任意のトークン署名証明書/キー、トークン暗号化証明書/キー、サービス通信証明書/キーのほか、すべての自己署名証明書をエクスポートすることもできます。 サーバーで使用中のすべての証明書を表示するには、Windows PowerShell を使用します。 Windows PowerShell を開き、コマンド `PSH:>add-pssnapin “Microsoft.adfs.powershell`を実行して、AD FS コマンドレットを Windows PowerShell セッションに追加します。 次に、コマンド `PSH:>Get-ADFSCertificate` を実行し、サーバーで使用中のすべての証明書を表示します。 このコマンドの出力には、各証明書の格納場所を指定する StoreLocation および StoreName の値が含まれます。 その後、[サーバー認証証明書の秘密キー部分のエクスポートに関するページ](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md)のガイダンスを使用して、各証明書およびその秘密キーを .pfx ファイルにエクスポートできます。  
>   
>  オペレーティング システムをアップグレードしても、外部証明書はすべて保持されます。したがって、これらの証明書のエクスポートは省略可能です。  
  
3. AD FS 2.0 フェデレーション サービスのプロパティ (フェデレーション サービス名、フェデレーション サービス表示名、フェデレーション サーバー識別子など) をファイルにエクスポートします。  
  
フェデレーション サービスのプロパティをエクスポートするには、Windows PowerShell を開き、コマンド `PSH:>add-pssnapin “Microsoft.adfs.powershell”`を実行して AD FS コマンドレットを Windows PowerShell セッションに追加します。 次に、コマンド `PSH:> Get-ADFSProperties | Out-File “.\properties.txt”` を実行してフェデレーション サービスのプロパティをエクスポートします。  
  
出力ファイルには次の重要な構成値が含まれます。  
  
    
|**Get-adfsproperties によって報告された、フェデレーション サービスのプロパティ名**|**AD FS 管理コンソールで、フェデレーション サービスのプロパティ名**|
|------|------|
|HostName|フェデレーション サービス名|  
|識別子|フェデレーション サービスの識別子|  
|DisplayName|フェデレーション サービスの表示名|  
  
4. アプリケーション構成ファイルをバックアップします。 その他の設定として、このファイルにはポリシー データベースの接続文字列が含まれます。  
  
アプリケーション構成ファイルをバックアップするには、 `%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config` ファイルをバックアップ サーバーの安全な場所に手動でコピーする必要があります。  
  
> [!NOTE]
>  このファイル内で "policystore connectionstring=" の直後にあるデータベース接続文字列をメモしてください。 接続文字列で SQL Server データベースが指定されている場合、フェデレーション サーバーで元の AD FS 構成を復元するときに、この値が必要になります。  
>   
>  たとえば、WID 接続文字列は `“Data Source=\\.\pipe\mssql$microsoft##ssee\sql\query;Initial Catalog=AdfsConfiguration;Integrated Security=True"` となります。 SQL Server 接続文字列は `"Data Source=databasehostname;Integrated Security=True"` となります。  
  
5. AD FS 2.0 フェデレーション サービス アカウントの ID とこのアカウントのパスワードを記録します。  
  
ID 値を検索するには、 **[サービス]** コンソールで **[AD FS 2.0 Windows サービス]** の **[ログオン方法]** 列を調べ、この値を手動で記録します。  
  
> [!NOTE]
>  スタンドアロン フェデレーション サービスの場合、組み込みのネットワーク サービス アカウントが使用されます。  この場合、パスワードは必要ありません。  
  
6. 有効な AD FS エンドポイントのリストをファイルにエクスポートします。  
  
これを行うには、Windows PowerShell を開き、コマンド `PSH:>add-pssnapin “Microsoft.adfs.powershell”`を実行して AD FS コマンドレットを Windows PowerShell セッションに追加します。 次に、コマンド `PSH:> Get-ADFSEndpoint | Out-File “.\endpoints.txt”`を実行して、有効な AD FS エンドポイントの一覧をファイルにエクスポートします。  
  
7. カスタム要求記述をファイルにエクスポートします。  
  
これを行うには、Windows PowerShell を開き、コマンド `PSH:>add-pssnapin “Microsoft.adfs.powershell”`を実行して AD FS コマンドレットを Windows PowerShell セッションに追加します。 次に、コマンド `Get-ADFSClaimDescription | Out-File “.\claimtypes.txt”` を実行して、カスタム要求記述をファイルにエクスポートします。  
  
##  <a name="step-2-export-claims-provider-trusts"></a>手順 2:要求プロバイダー信頼をエクスポートする  
 要求プロバイダー信頼をエクスポートするには、次の手順を実行します。  
  
### <a name="to-export-claims-provider-trusts"></a>要求プロバイダー信頼をエクスポートするには  
  
1.  Windows PowerShell を使用して、すべての要求プロバイダー信頼をエクスポートできます。 Windows PowerShell を開き、コマンド `PSH:>add-pssnapin “Microsoft.adfs.powershell”`を実行して、AD FS コマンドレットを Windows PowerShell セッションに追加します。 次に、コマンド `PSH:>Get-ADFSClaimsProviderTrust | Out-File “.\cptrusts.txt”`を実行して、すべての要求プロバイダー信頼をエクスポートします。  
  
## <a name="step-3-export-relying-party-trusts"></a>手順 3:証明書利用者信頼をエクスポートする  
 証明書利用者信頼をエクスポートするには、次の手順を実行します。  
  
### <a name="to-export-relying-party-trusts"></a>証明書利用者信頼をエクスポートするには  
  
1.  すべての証明書利用者信頼をエクスポートするには、Windows PowerShell を開き、コマンド `PSH:>add-pssnapin “Microsoft.adfs.powershell”`を実行して AD FS コマンドレットを Windows PowerShell セッションに追加します。 次に、コマンド`PSH:>Get-ADFSRelyingPartyTrust | Out-File “.\rptrusts.txt”`を実行して、すべての証明書利用者信頼をエクスポートします。  
  
## <a name="step-4-back-up-custom-attribute-stores"></a>手順 4:カスタム属性ストアをバックアップする  
 AD FS によって使用中のカスタム属性ストアに関する情報を検索するには、Windows PowerShell を使用します。 Windows PowerShell を開き、コマンド `PSH:>add-pssnapin “Microsoft.adfs.powershell”`を実行して、AD FS コマンドレットを Windows PowerShell セッションに追加します。 次に、コマンド `PSH:>Get-ADFSAttributeStore`を実行してカスタム属性ストアに関する情報を検索します。 カスタム属性ストアのアップグレードまたは移行手順はさまざまです。  
  
## <a name="step-5-back-up-webpage-customizations"></a>手順 5:Web ページのカスタマイズをバックアップする  
 任意の Web ページのカスタマイズをバックアップするには、IIS で仮想パス **“/adfs/ls”** にマップされたディレクトリから AD FS Web ページと **web.config** ファイルをコピーします。 既定では、そのファイルは **%systemdrive%\inetpub\adfs\ls** ディレクトリにあります。  

## <a name="next-steps"></a>次の手順
 [AD FS 2.0 フェデレーション サーバーの移行を準備します。](prepare-to-migrate-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーション サーバー プロキシの移行を準備します。](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [AD FS 2.0 フェデレーション サーバーを移行します。](migrate-the-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーション サーバー プロキシを移行します。](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [AD FS 1.1 Web エージェントの移行](migrate-the-ad-fs-web-agent.md)