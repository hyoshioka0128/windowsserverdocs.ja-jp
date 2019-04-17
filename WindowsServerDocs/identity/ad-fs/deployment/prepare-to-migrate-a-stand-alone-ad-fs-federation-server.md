---
title: "スタンドアロン AD FS フェデレーション サーバーの移行を準備します。"
description: "Windows Server 2012 へのスタンドアロン AD FS サーバーの移行の準備について説明します。"
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 0c1fd2bc1026d9aee25c591cf5c91a1c59f66ee0
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
#  <a name="prepare-to-migrate-a-stand-alone-ad-fs-federation-server-or-a-single-node-ad-fs-farm"></a>スタンドアロン AD FS フェデレーション サーバーまたは単一ノード AD FS ファームの移行を準備します。  
 
(同じサーバーの移行) の移行の準備をスタンドアロン AD FS 2.0 フェデレーション サーバーまたは単一ノード AD FS ファームを Windows Server 2012 では、必要がありますエクスポートしてこのサーバーから AD FS 構成データをバックアップします。  
  
AD FS 構成データをエクスポートするには、次のタスクを実行します。  
  
-   [手順 1: サービスの設定をエクスポートします。](#step-1-export-service-settings)  
  
-   [手順 2: 要求プロバイダー信頼をエクスポート](#step-2-export-claims-provider-trusts)  
  
-   [手順 3: 証明書利用者信頼をエクスポートします。](#step-3-export-relying-party-trusts)  
  
-   [手順 4: カスタム属性ストアをバックアップします。](#step-4-back-up-custom-attribute-stores)  
  
-   [手順 5: Web ページのカスタマイズをバックアップします。](#step-5-back-up-webpage-customizations)  
  
## <a name="step-1-export-service-settings"></a>手順 1: サービスの設定をエクスポートします。  
 サービスの設定をエクスポートするには、次の手順を実行します。  
  
### <a name="to-export-service-settings"></a>サービスの設定をエクスポートするには  
  
1.  フェデレーション サービスによって使用される SSL 証明書の証明書のサブジェクト名と拇印値を記録します。 SSL 証明書を見つけるには、インターネット インフォメーション サービス (IIS) 管理を開きますコンソールで、選択**既定の Web サイト**左側のウィンドウで [**バインドしています.** **アクション**、ウィンドウの検索と選択、https バインド] をクリックして**編集**、] をクリックし、**ビュー**します。  
  
> [!NOTE]
>  必要に応じて、フェデレーション サービスとその秘密キーを .pfx ファイルで使用される SSL 証明書をエクスポートすることもできます。 詳細については、次を参照してください。[サーバー認証証明書の秘密キー部分のエクスポート](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md)します。  
>   
>  この証明書がローカル コンピューターの個人証明書ストアに格納され、オペレーティング システムのアップグレードでは維持されますので、SSL 証明書のエクスポートはオプションです。  
  
2.  AD FS サービス通信の構成、トークン暗号化解除とトークン署名証明書を記録します。  使用されているすべての証明書を表示するには、Windows PowerShell を開き、AD FS のコマンドレットを Windows PowerShell セッションに追加するには、次のコマンドを実行します。`PSH:>add-pssnapin “Microsoft.adfs.powershell”`します。 ファイルで使用中のすべての証明書の一覧を作成する次のコマンドを実行し、 `PSH:>Get-ADFSCertificate | Out-File “.\certificates.txt”`  
  
> [!NOTE]
>  必要に応じて、内部生成されない、すべての自己署名証明書だけでなくキー、トークン署名、トークン暗号化、またはサービス通信証明書をエクスポートすることもできます。 Windows PowerShell を使用して、サーバーで使用されているすべての証明書を表示することができます。 Windows PowerShell を開き、AD FS のコマンドレットを Windows PowerShell セッションに追加するには、次のコマンドを実行します。`PSH:>add-pssnapin “Microsoft.adfs.powershell`します。 サーバーで使用されているすべての証明書を表示するのには、次のコマンドを実行し、`PSH:>Get-ADFSCertificate`します。 このコマンドの出力には、各証明書の格納場所を指定する StoreLocation および StoreName の値が含まれています。 ガイダンスを使用することができます、[サーバー認証証明書の秘密キー部分のエクスポート](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md)各証明書とその秘密キーを .pfx ファイルにエクスポートします。  
>   
>  すべての外部証明書は、オペレーティング システムのアップグレード中に保存されるため、これらの証明書のエクスポートは省略可能です。  
  
3.  エクスポート AD FS 2.0 フェデレーション サービスのプロパティ、フェデレーション サービス名、フェデレーション サービス表示名、ファイルへのフェデレーション サーバー識別子などです。  
  
フェデレーション サービスのプロパティをエクスポートする Windows PowerShell を開き、AD FS のコマンドレットを Windows PowerShell セッションに追加するには、次のコマンドを実行します。`PSH:>add-pssnapin “Microsoft.adfs.powershell”`します。 フェデレーション サービスのプロパティをエクスポートするのには、次のコマンドを実行し、:`PSH:> Get-ADFSProperties | Out-File “.\properties.txt”`します。  
  
出力ファイルは、次の重要な構成値が表示されます。  
  
    
|**Get-ADFSProperties によってレポートされるフェデレーション サービスのプロパティ名**|**AD FS 管理コンソールで、フェデレーション サービスのプロパティ名**|
|------|------|
|ホスト名|フェデレーション サービス名|  
|識別子|フェデレーション サービス識別子|  
|DisplayName|フェデレーション サービスの表示名|  
  
4.  アプリケーション構成ファイルをバックアップします。 その他の設定の間では、このファイルにはポリシー データベース接続文字列が含まれています。  
  
アプリケーション構成ファイルをバックアップする必要があります手動でコピーする、`%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config`ファイルをバックアップ サーバー上の安全な場所です。  
  
> [!NOTE]
>  メモ データベース接続文字列のこのファイルの直後にある"policystore connectionstring =")。 接続文字列は、SQL Server データベースを指定する場合は、フェデレーション サーバーで元の AD FS 構成を復元するときに、値が必要です。  
>   
>  WID 接続文字列の例を次に示します:`“Data Source=\\.\pipe\mssql$microsoft##ssee\sql\query;Initial Catalog=AdfsConfiguration;Integrated Security=True"`します。 SQL Server 接続文字列の例を次に示します:`"Data Source=databasehostname;Integrated Security=True"`します。  
  
5.  AD FS 2.0 フェデレーション サービス アカウントの ID とこのアカウントのパスワードを記録します。  
  
Id 値を検索するを調べて、**ログとして**の列**AD FS 2.0 Windows サービス**で、**サービス**コンソールを手動でこの値を記録します。  
  
> [!NOTE]
>  スタンドアロン フェデレーション サービスでは、組み込みの NETWORK SERVICE アカウントが使用されます。  この場合、パスワードを保持する必要はありません。  
  
6.  有効な AD FS エンドポイントの一覧をファイルにエクスポートします。  
  
これを行うには、Windows PowerShell を開き、AD FS のコマンドレットを Windows PowerShell セッションに追加するには、次のコマンドを実行します。`PSH:>add-pssnapin “Microsoft.adfs.powershell”`します。 有効な AD FS エンドポイントの一覧をファイルにエクスポートするには、次のコマンドを実行し、:`PSH:> Get-ADFSEndpoint | Out-File “.\endpoints.txt”`します。  
  
7.  カスタム要求記述をすべてをファイルにエクスポートします。  
  
これを行うには、Windows PowerShell を開き、AD FS のコマンドレットを Windows PowerShell セッションに追加するには、次のコマンドを実行します。`PSH:>add-pssnapin “Microsoft.adfs.powershell”`します。 カスタム要求記述をすべてをファイルにエクスポートするのには、次のコマンドを実行します。`Get-ADFSClaimDescription | Out-File “.\claimtypes.txt”`します。  
  
##  <a name="step-2-export-claims-provider-trusts"></a>手順 2: 要求プロバイダー信頼をエクスポート  
 要求プロバイダー信頼をエクスポートするには、次の手順を実行します。  
  
### <a name="to-export-claims-provider-trusts"></a>要求プロバイダー信頼をエクスポートするには  
  
1.  Windows PowerShell を使用して、すべての要求プロバイダー信頼をエクスポートすることができます。 Windows PowerShell を開き、AD FS のコマンドレットを Windows PowerShell セッションに追加するには、次のコマンドを実行します。`PSH:>add-pssnapin “Microsoft.adfs.powershell”`します。 すべての要求プロバイダー信頼をエクスポートするのには、次のコマンドを実行し、:`PSH:>Get-ADFSClaimsProviderTrust | Out-File “.\cptrusts.txt”`します。  
  
## <a name="step-3-export-relying-party-trusts"></a>手順 3: 証明書利用者信頼をエクスポートします。  
 証明書利用者信頼をエクスポートするには、次の手順を実行します。  
  
### <a name="to-export-relying-party-trusts"></a>証明書利用者信頼をエクスポートするには  
  
1.  すべての証明書利用者信頼をエクスポートする、Windows PowerShell を開き、AD FS のコマンドレットを Windows PowerShell セッションに追加するには、次のコマンドを実行する:`PSH:>add-pssnapin “Microsoft.adfs.powershell”`します。 すべての証明書利用者信頼をエクスポートするのには、次のコマンドを実行し、:`PSH:>Get-ADFSRelyingPartyTrust | Out-File “.\rptrusts.txt”`します。  
  
## <a name="step-4-back-up-custom-attribute-stores"></a>手順 4: カスタム属性ストアをバックアップします。  
 Windows PowerShell を使用して AD FS によって使用中のカスタム属性ストアに関する情報を見つけることができます。 Windows PowerShell を開き、AD FS のコマンドレットを Windows PowerShell セッションに追加するには、次のコマンドを実行します。`PSH:>add-pssnapin “Microsoft.adfs.powershell”`します。 カスタム属性ストアの情報を見つけるには、次のコマンドを実行し、:`PSH:>Get-ADFSAttributeStore`します。 アップグレードまたはカスタム属性ストアを移行する手順は異なります。  
  
## <a name="step-5-back-up-webpage-customizations"></a>手順 5: Web ページのカスタマイズをバックアップします。  
 任意の Web ページのカスタマイズをバックアップするには、AD FS Web ページをコピーし、**Web.config**仮想パスにマップされているディレクトリからファイル**"/adfs/ls"** IIS でします。 既定では、**%systemdrive%\inetpub\adfs\ls**ディレクトリ。  

## <a name="next-steps"></a>次の手順
 [AD FS 2.0 フェデレーション サーバーの移行を準備します。](prepare-to-migrate-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーション サーバー プロキシの移行を準備します。](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [AD FS 2.0 フェデレーション サーバーを移行します。](migrate-the-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーション サーバー プロキシを移行します。](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [AD FS 1.1 Web エージェントを移行します。](migrate-the-ad-fs-web-agent.md)