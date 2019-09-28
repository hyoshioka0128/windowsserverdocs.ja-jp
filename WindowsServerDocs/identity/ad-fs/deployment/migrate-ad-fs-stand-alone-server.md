---
title: スタンドアロン AD FS フェデレーション サーバーまたは単一ノード AD FS ファームの移行
description: スタンドアロンまたは単一ノードの AD FS 2.0 サーバーを Windows Server 2012 に移行する方法について説明します。
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: b8029d67a9f21e5189322692b8f1316306542c96
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359384"
---
# <a name="migrate-a-stand-alone-ad-fs-federation-server-or-a-single-node-ad-fs-farm"></a>スタンドアロン AD FS フェデレーション サーバーまたは単一ノード AD FS ファームの移行  
このドキュメントでは、AD FS 2.0 のスタンドアロンサーバーを Windows Server 2012 に移行する方法について詳しく説明します。

## <a name="migrate-a-stand-alone-ad-fs-20-server"></a>スタンドアロン AD FS 2.0 サーバーを移行する

AD FS 2.0 サーバーを Windows Server 2012 に移行するには、次の手順を使用します。
  
1.  「[スタンドアロン AD FS フェデレーションサーバーまたは単一ノード AD FS ファームの移行の準備](prepare-to-migrate-a-stand-alone-ad-fs-federation-server.md)」の手順を確認して実行します。  
  
2.  サーバー上のオペレーティングシステムを windows server 2008 R2 または Windows Server 2008 から Windows Server 2012 にインプレースアップグレードします。 詳細については、「[Windows Server 2012 のインストール](https://technet.microsoft.com/library/jj134246.aspx)」を参照してください。  
  
> [!IMPORTANT]
>  オペレーティング システムをアップグレードすると、このサーバーの AD FS 構成が失われ、AD FS 2.0 サーバーの役割が削除されます。 代わりに、Windows Server 2012 AD FS サーバーロールがインストールされますが、構成されていません。 元の AD FS 構成を手動で作成し、その他の AD FS 設定を復元して、フェデレーション サーバーの移行を完了する必要があります。  
  
3. 元の AD FS 構成を作成します。 元の AD FS 構成を作成するには、次のいずれかの方法を使用します。  
  
-   **AD FS フェデレーション サーバー構成ウィザード** を使用して、新しいフェデレーション サーバーを作成する。 詳細については、[フェデレーション サーバー ファームでの最初のフェデレーション サーバーの作成に関するページ](Create-the-First-Federation-Server-in-a-Federation-Server-Farm.md)を参照してください。  
  
このウィザードでは、AD FS フェデレーション サーバーの移行の準備を行っているときに収集した次の情報を使用します。  
  
 |**フェデレーションサーバー構成ウィザードの入力オプション**|**次の値を使用します。**| 
|-----|-----| 
|**[フェデレーション サービス名の指定]** ページの **[SSL 証明書]**|AD FS フェデレーション サーバーの移行の準備を行っているときに記録したサブジェクト名と拇印が含まれる SSL 証明書を選択します。|  
|**[サービス アカウントの指定]** ページの **[サービス アカウント]** と **[パスワード]**|AD FS フェデレーション サーバーの移行の準備を行っているときに記録したサービス アカウント情報を入力します。 **注:** ウィザードの 2 ページ目でスタンドアロン フェデレーション サーバーを選択すると、ネットワーク サービスがサービス アカウントとして自動的に使用されます。|  
  
> [!IMPORTANT] 
> この方法は、Windows Internal Database (WID) を使って、スタンドアロン フェデレーション サーバーまたは単一ノード AD FS ファーム用の AD FS 構成データベースを格納している場合にのみ使用できます。  
>
>  SQL Server を使用して単一 AD FS ファーム用の AD FS 構成データベースを格納している場合は、Windows PowerShell を使って、元の AD FS 構成をフェデレーション サーバーに作成する必要があります。  
  
-   Windows PowerShell を使用する  
  
> [!IMPORTANT]
>  SQL Serer を使ってスタンドアロン フェデレーション サーバーまたは単一ノード AD FS ファーム用の AD FS 構成データベースを格納している場合は、Windows PowerShell を使用する必要があります。  
  
次の例は、Windows PowerShell を使用して、単一ノード SQL Server ファームのフェデレーション サーバーに元の AD FS 構成を作成する方法を示しています。  Windows PowerShell モジュールを開き、 `$fscredential = Get-Credential`コマンドを実行します。 SQL Server ファームの移行の準備を行っているときに記録したサービス アカウントの名前とパスワードを入力します。 次に `C:\PS> Add-AdfsFarmNode -ServiceAccountCredential $fscredential -SQLConnectionString "Data Source=<Data Source>;Integrated Security=True"` コマンドを実行します。 `Data Source` は `%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config`ファイルのポリシー ストア接続文字列値のデータ ソース値です。  
  
4. その他の AD FS サービスの設定と信頼関係を復元します。 これは手動で行います。エクスポートしたファイルと、AD FS の移行の準備中に収集した値は、この手順で使用できます。 詳細な手順については、「その他の AD FS ファーム構成の復元」を参照してください。  
  
> [!NOTE]
>  この手順は、スタンドアロン フェデレーション サーバーまたは単一ノード WID ファームを移行する場合にのみ必要です。  フェデレーション サーバーで SQL Server データベースが構成ストアとして使用されている場合、サービスの設定と信頼関係はデータベースに保持されます。  
  
5. AD FS Web ページを更新します。 これは手動で行います。 移行の準備中にカスタマイズした AD FS web ページをバックアップした場合は、バックアップデータを使用して、 **%systemdrive%\inetpub\adfs\ls**ディレクトリに既定で作成された既定の AD FS web ページを AD FS の結果として上書きします。Windows Server 2012 の構成。  
  
6. カスタム属性ストアなど、その他の AD FS カスタマイズを復元します。  
  
## <a name="restoring-the-remaining-ad-fs-farm-configuration"></a>その他の AD FS ファーム構成の復元  
  
-   次の AD FS サービスの設定を、次のように、単一ノード WID ファームまたはスタンドアロン フェデレーション サービスに復元します。  
  
    -   AD FS 管理コンソールで、 **[サービス]** を選択し、 **[フェデレーション サービスの編集]** をクリックします。 各値を、移行の準備中に properties.txt ファイルにエクスポートした値と照合して、フェデレーション サービスの設定を確認します。  
  
    
|**Set-adfsproperties によって報告されたフェデレーションサービスプロパティ名**|**AD FS 管理コンソールのフェデレーションサービスプロパティ名**|  
|-----|-----|
|DisplayName|フェデレーション サービスの表示名|  
|HostName|フェデレーション サービス名|  
|識別子|フェデレーション サービスの識別子|  
  
-   AD FS 管理コンソールで、 **[証明書]** を選択します。 サービス通信証明書、トークン暗号化解除証明書、およびトークン署名証明書を、移行の準備中に certificates.txt ファイルにエクスポートした値と照合して、各証明書を確認します。  
  
トークン暗号化解除証明書またはトークン署名証明書を既定の自己署名証明書から外部証明書に変更するには、まず、既定で有効になっている自動証明書ロールオーバー機能を無効にする必要があります。  これを行うには、 `PSH: Set-ADFSProperties –AutoCertificateRollover $false`Windows PowerShell コマンドを使用できます。  
  
-   AD FS 管理コンソールで、 **[エンドポイント]** を選択します。 有効な AD FS エンドポイントを、AD FS の移行の準備中にファイルにエクスポートした有効な AD FS エンドポイントのリストと照合します。  
  
-   AD FS 管理コンソールで、 **[要求記述]** を選択します。 AD FS の要求記述のリストを、AD FS の移行の準備中にファイルにエクスポートした要求記述のリストと照合します。 ファイルに含まれるが AD FS の既定のリストに含まれないカスタム要求記述をすべて追加します。  管理コンソール内の要求識別子はファイル内の ClaimType にマップされることに注意してください。  要求記述の追加の詳細については、[要求記述の追加に関するページ](../operations/add-a-claim-description.md)を参照してください。 詳細については、「AD FS 2.0 フェデレーション サーバーの移行の準備」の「手順 1: サービスの設定をエクスポートする」を参照してください。  
  
-   AD FS 管理コンソールで、 **[要求プロバイダー信頼]** を選択します。 **要求プロバイダー信頼の追加ウィザード**を使用して、各要求プロバイダー信頼を手動で再作成する必要があります。  AD FS の移行の準備中にエクスポートして記録した要求プロバイダー信頼のリストを使用します。 ファイル内の識別子 "AD AUTHORITY" を持つ要求プロバイダー信頼は、既定の AD FS 構成に含まれる “Active Directory” 要求プロバイダー信頼であるため無視できます。  ただし、移行の前に、Active Directory 信頼に追加した可能性があるカスタム要求規則を確認してください。 要求プロバイダー信頼の作成の詳細については、「[フェデレーション メタデータを使用した要求プロバイダー信頼の作成](../operations/create-a-claims-provider-trust.md#to-create-a-claims-provider-trust-using-federation-metadata)」または「[要求プロバイダー信頼の手動作成](../operations/create-a-claims-provider-trust.md#to-create-a-claims-provider-trust-manually)」を参照してください。  
  
-   AD FS 管理コンソールで、 **[証明書利用者信頼]** を選択します。 **証明書利用者信頼の追加ウィザード**を使用して、各証明書利用者信頼を手動で再作成する必要があります。 AD FS の移行の準備中にエクスポートして記録した証明書利用者信頼のリストを使用します。 証明書利用者信頼の作成の詳細については、「[フェデレーション メタデータを使って証明書利用者信頼を作成する](../operations/create-a-relying-party-trust.md#to-create-a-claims-aware-relying-party-trust-using-federation-metadata)」または「[証明書利用者信頼を手動で作成する](../operations/create-a-relying-party-trust.md#to-create-a-claims-aware-relying-party-trust-manually)」を参照してください。 

## <a name="next-steps"></a>次の手順
 [AD FS 2.0 フェデレーションサーバーの移行の準備](prepare-to-migrate-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーションサーバープロキシの移行の準備](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [AD FS 2.0 フェデレーションサーバー](migrate-the-ad-fs-fed-server.md)  を移行します。  
 [AD FS 2.0 フェデレーションサーバープロキシ   を移行します](migrate-the-ad-fs-2-fed-server-proxy.md)。  
 [AD FS 1.1 Web エージェントの移行](migrate-the-ad-fs-web-agent.md)




-   
-    