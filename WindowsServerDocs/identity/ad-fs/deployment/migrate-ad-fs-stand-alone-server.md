---
title: "スタンドアロン AD FS フェデレーション サーバーまたは単一ノード AD FS ファームを移行します。"
description: "スタンドアロン サーバーまたは単一ノード AD の移行に関する情報を提供する Windows Server 2012 FS 2.0 サーバー"
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 10371349fe19be92fb997c9c28f19def0ecad7e9
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="migrate-a-stand-alone-ad-fs-federation-server-or-a-single-node-ad-fs-farm"></a>スタンドアロン AD FS フェデレーション サーバーまたは単一ノード AD FS ファームを移行します。  
このドキュメントでは、Windows Server 2012 への AD FS 2.0 のスタンドアロン サーバーの移行の詳細を提供します。

## <a name="migrate-a-stand-alone-ad-fs-20-server"></a>移行、スタンドアロン AD FS 2.0 サーバー

次の手順を使用して AD FS 2.0 に移行するには、Windows Server 2012 のサーバー。
  
1.  確認し、手順を実行[スタンドアロン AD FS フェデレーション サーバーまたは単一ノード AD FS ファームの移行の準備](prepare-to-migrate-a-stand-alone-ad-fs-federation-server.md)します。  
  
2.  サーバーから Windows Server 2008 R2 または Windows Server 2012 への Windows Server 2008 オペレーティング システムのインプレース アップグレードを実行します。 詳細については、次を参照してください。[Windows Server 2012 のインストール](https://technet.microsoft.com/library/jj134246.aspx)します。  
  
> [!IMPORTANT]
>  オペレーティング システムのアップグレードの結果、このサーバーの AD FS 構成が失われたと AD FS 2.0 サーバーの役割が削除されます。 Windows Server 2012 の AD FS サーバーの役割が代わりに、インストールされているが構成されていません。 手動で元の AD FS 構成を作成して、フェデレーション サーバーの移行を完了する他の AD FS 設定を復元する必要があります。  
  
3.  元の AD FS 構成を作成します。 次のいずれかを使用して、元の AD FS 構成を作成できます。  
  
-   使用して、**AD FS フェデレーション サーバー構成ウィザード**新しいフェデレーション サーバーを作成します。 詳細については、次を参照してください。[フェデレーション サーバー ファームに最初のフェデレーション サーバーを作成する](Create-the-First-Federation-Server-in-a-Federation-Server-Farm.md)します。  
  
ウィザードを使用していくは、次のように、AD FS フェデレーション サーバーの移行の準備中に収集した情報を使用します。  
  
 |**フェデレーション サーバー構成ウィザードのオプション**|**次の値を使用してください。**| 
|-----|-----| 
|**SSL 証明書**上、**フェデレーション サービス名の指定**] ページ|サブジェクト名と拇印を AD FS フェデレーション サーバーの移行の準備中に記録した [SSL 証明書を選択します。|  
|**サービス アカウント**と**パスワード**上、**サービス アカウントの指定**] ページ|AD FS フェデレーション サーバーの移行の準備中に記録したサービス アカウント情報を入力します。 **注:**サービス アカウントとしてネットワーク サービスが自動的に使用、ウィザードの 2 ページ目でスタンドアロン フェデレーション サーバーを選択する場合。|  
  
> [!IMPORTANT] 
> スタンドアロン フェデレーション サーバーまたは単一ノード AD FS ファームの AD FS 構成データベースを格納する Windows Internal Database (WID) を使用している場合にのみ、このメソッドを使用することができます。  
>
>  単一ノード AD FS ファーム用の AD FS 構成データベースを格納する SQL Server を使用する場合は Windows PowerShell を使用して、フェデレーション サーバーで元の AD FS 構成を作成する必要があります。  
  
-   Windows PowerShell を使用して  
  
> [!IMPORTANT]
>  スタンドアロン フェデレーション サーバーまたは単一ノード AD FS ファームの AD FS 構成データベースを格納する SQL Server を使用している場合は、Windows PowerShell を使用する必要があります。  
  
Windows PowerShell を使用して、単一ノード SQL Server ファームにフェデレーション サーバーで元の AD FS 構成を作成する方法の例を次に示します。  Windows PowerShell モジュールを開き、次のコマンドを実行します。`$fscredential = Get-Credential`します。 名前と、SQL server ファームの移行の準備中に記録したサービス アカウントのパスワードを入力します。 次のコマンドを実行します。`C:\PS> Add-AdfsFarmNode -ServiceAccountCredential $fscredential -SQLConnectionString "Data Source=<Data Source>;Integrated Security=True"`場所`Data Source`ファイルのポリシー ストア接続文字列値のデータ ソースの値は、:`%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config`します。  
  
4.  その他の AD FS サービスの設定を復元し、信頼関係します。 これは、手動の手順をエクスポートしたファイルと、AD FS の移行の準備中に収集した値を使用することができます。 詳細については、他の AD FS ファーム構成の復元を参照してください。  
  
> [!NOTE]
>  この手順は、スタンドアロン フェデレーション サーバーまたは単一ノード WID ファームを移行するかどうかに必要なです。  フェデレーション サーバーは、構成ストアとして SQL Server データベースを使用している場合、サービスの設定と信頼関係はデータベースに保持されます。  
  
5.  AD FS Web ページを更新します。 これは、手動で行います。 移行の準備中、カスタマイズされた AD FS Web ページをバックアップした場合は、既定では既定で作成された AD FS Web ページを上書きする、バックアップ データを使用して、**%systemdrive%\inetpub\adfs\ls**ディレクトリに Windows Server 2012 で AD FS 構成の結果。  
  
6.  カスタム属性ストアなどその他の AD FS カスタマイズを復元します。  
  
## <a name="restoring-the-remaining-ad-fs-farm-configuration"></a>残りの AD FS ファーム構成を復元します。  
  
-   次のように、単一ノード WID ファームまたはスタンドアロン フェデレーション サービスに次の AD FS サービスの設定を復元します。  
  
    -   AD FS 管理コンソールで、次のように選択します**サービス**] をクリック**フェデレーション サービスの編集.。**. 各移行の準備中に properties.txt ファイルにエクスポートした値と比較値をチェックして、フェデレーション サービスの設定を確認します。  
  
    
|**Get-ADFSProperties によってレポートされるフェデレーション サービスのプロパティ名**|**AD FS 管理コンソールで、フェデレーション サービスのプロパティ名**|  
|-----|-----|
|DisplayName|フェデレーション サービスの表示名|  
|ホスト名|フェデレーション サービス名|  
|識別子|フェデレーション サービス識別子|  
  
-   AD FS 管理コンソールで、次のように選択します。**証明書**します。 各移行の準備中に certificates.txt ファイルにエクスポートした値と比較して、サービス通信、トークン暗号化解除、およびトークン署名証明書を確認します。  
  
トークン暗号化解除またはトークン署名証明書を既定の自己署名証明書から外部証明書を変更するには、最初に既定で有効になっている証明書の自動ロール オーバー機能を無効にする必要があります。  これを行うには、次の Windows PowerShell コマンドを使用することができます:`PSH: Set-ADFSProperties –AutoCertificateRollover $false`します。  
  
-   AD FS 管理コンソールで、次のように選択します。**エンドポイント**します。 AD FS の移行の準備中にファイルにエクスポートした有効な AD FS エンドポイントのリストに対して有効な AD FS エンドポイントを確認します。  
  
-   AD FS 管理コンソールで、次のように選択します。**要求記述**します。 AD FS の移行の準備中にファイルにエクスポートした要求記述のリストと照合します AD FS 要求記述のリストを確認します。 カスタム要求記述をすべてのファイルに含まれていますが、AD FS の既定の一覧に含まれていないを追加します。  管理コンソール内の要求識別子は、ファイル内の ClaimType にマップされる注意してください。  要求記述の追加について詳しくは、次を参照してください。[要求記述の追加](../operations/add-a-claim-description.md)します。 詳細については、広告の移行の準備」の「手順 1-サービス設定のエクスポート」セクションを参照して FS 2.0 フェデレーション サーバー。  
  
-   AD FS 管理コンソールで、次のように選択します。**要求プロバイダー信頼**します。 各要求プロバイダー信頼を使用して手動で再作成する必要があります、**要求プロバイダー信頼のウィザードの追加**します。  エクスポートして、AD FS の移行の準備中に記録される要求プロバイダー信頼のリストを使用します。 これは、"Active Directory"要求プロバイダー信頼の既定の AD FS 構成の一部であるために、ファイル内の識別子"AD AUTHORITY"を持つ要求プロバイダー信頼を無視できます。  ただし、移行の前に Active Directory 信頼に追加したカスタム要求規則を確認します。 要求プロバイダー信頼の作成の詳細についてを参照してください。[、要求プロバイダー信頼を使用してフェデレーション メタデータを作成する](../operations/create-a-claims-provider-trust.md#to-create-a-claims-provider-trust-using-federation-metadata)または[、要求プロバイダー信頼を手動で作成](../operations/create-a-claims-provider-trust.md#to-create-a-claims-provider-trust-manually)します。  
  
-   AD FS 管理コンソールで、**証明書利用者信頼を選択**します。 各証明書利用者信頼を使用して手動で再作成する必要があります、**信頼の追加証明書利用者のパーティ ウィザード**します。 証明書利用者信頼をエクスポートして、AD FS の移行の準備中に記録のリストを使用します。 証明書利用者信頼を作成する方法について詳しくは、次を参照してください。[、証明書利用者のパーティを使用してフェデレーション メタデータ信頼を作成する](../operations/create-a-relying-party-trust.md#to-create-a-claims-aware-relying-party-trust-using-federation-metadata)または[、証明書利用者信頼を手動で作成](../operations/create-a-relying-party-trust.md#to-create-a-claims-aware-relying-party-trust-manually)します。 

## <a name="next-steps"></a>次の手順
 [AD FS 2.0 フェデレーション サーバーの移行を準備します。](prepare-to-migrate-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーション サーバー プロキシの移行を準備します。](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [AD FS 2.0 フェデレーション サーバーを移行します。](migrate-the-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーション サーバー プロキシを移行します。](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [AD FS 1.1 Web エージェントを移行します。](migrate-the-ad-fs-web-agent.md)




-   
-    