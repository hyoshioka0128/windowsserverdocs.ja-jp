---
title: AD FS SQL ファームの移行の準備
description: AD FS server SQL ファームを Windows Server 2012 に移行するための準備について説明します。
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 2d8bbe5021b876712862c992b643b7828095e869
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408219"
---
# <a name="prepare-to-migrate-a-sql-server-farm"></a>SQL Server ファームの移行の準備  
 SQL Server ファームに属している AD FS 2.0 フェデレーションサーバーを Windows Server 2012 に移行する準備を行うには、これらのサーバーから AD FS 構成データをエクスポートしてバックアップする必要があります。  
  
 AD FS の構成データをエクスポートするには、次の作業を実行します。  
  
-   [ステップ 1: サービス設定のエクスポート @ no__t-0  
  
-   [手順 2:カスタム属性ストアのバックアップ @ no__t-0  
  
-   [手順 3:Web ページのカスタマイズをバックアップする @ no__t-0  
  
## <a name="step-1-export-service-settings"></a>手順 1:サービスの設定をエクスポートする  
 サービスの設定をエクスポートするには、次の手順を実行します。  
  
### <a name="to-export-service-settings"></a>サービスの設定をエクスポートするには  
  
1.  フェデレーション サービスによって使用される SSL 証明書の証明書サブジェクト名と拇印の値を記録します。 To find the SSL certificate, open the Internet Information Services (IIS) management console, select **[既定の Web サイト]** を選択します。 **[操作]** **[操作]** ウィンドウで、https バインドを検索して選択し、 **[編集]** をクリックして、 **[表示]** をクリックします。  
  
> [!NOTE]
>  オプションで、SSL 証明書とその秘密キーを .pfx ファイルにエクスポートすることもできます。 詳細については、[サーバー認証証明書の秘密キー部分のエクスポートに関するページ](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md)を参照してください。  
>   
>  SSL 証明書は、ローカル コンピューターの [個人] 証明書ストアに格納されており、オペレーティング システムをアップグレードしても保持されます。したがって、この手順は省略可能です。  
  
2. AD FS によって内部生成されない他の任意のトークン署名証明書/キー、トークン暗号化証明書/キー、サービス通信証明書/キーをエクスポートします。  
  
サーバーで AD FS によって使用中のすべての証明書を表示するには、Windows PowerShell を使用します。 Windows PowerShell を開き、コマンド `PSH:>add-pssnapin “Microsoft.adfs.powershell”`を実行して、AD FS コマンドレットを Windows PowerShell セッションに追加します。 次に、コマンド `PSH:>Get-ADFSCertificate` を実行し、サーバーで使用中のすべての証明書を表示します。 このコマンドの出力には、各証明書の格納場所を指定する StoreLocation および StoreName の値が含まれます。  
  
> [!NOTE]
>  その後、オプションで、[サーバー認証証明書の秘密キー部分のエクスポートに関するページ](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md)のガイダンスを使用して、各証明書およびその秘密キーを .pfx ファイルにエクスポートできます。 オペレーティング システムをアップグレードしても、外部証明書はすべて保持されます。したがって、この手順は省略可能です。  
  
3. アプリケーション構成ファイルをバックアップします。 その他の設定として、このファイルにはポリシー データベースの接続文字列が含まれます。  
  
アプリケーション構成ファイルをバックアップするには、 `%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config` ファイルをバックアップ サーバーの安全な場所に手動でコピーする必要があります。  
  
> [!NOTE]
>  `%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config`のファイルの “policystore connectionstring=” の直後にある SQL Server 接続文字列を記録します。 この文字列は、フェデレーション サーバーで元の AD FS 構成を復元するときに必要です。  
  
4. AD FS 2.0 フェデレーション サービス アカウントの ID とこのアカウントのパスワードを記録します。  
  
ID 値を検索するには、 **[サービス]** コンソールで **[AD FS 2.0 Windows サービス]** の **[ログオン方法]** 列を調べ、値を手動で記録します。  
  
## <a name="step-2-back-up-custom-attribute-stores"></a>手順 2:カスタム属性ストアをバックアップする  
 AD FS によって使用中のカスタム属性ストアに関する情報を検索するには、Windows PowerShell を使用します。 Windows PowerShell を開き、コマンド `PSH:>add-pssnapin “Microsoft.adfs.powershell”`を実行して、AD FS コマンドレットを Windows PowerShell セッションに追加します。 次に、コマンド `PSH:>Get-ADFSAttributeStore`を実行してカスタム属性ストアに関する情報を検索します。 カスタム属性ストアのアップグレードまたは移行手順はさまざまです。  
  
## <a name="step-3-back-up-webpage-customizations"></a>手順 3:Web ページのカスタマイズをバックアップする  
 任意の Web ページのカスタマイズをバックアップするには、IIS で仮想パス **“/adfs/ls”** にマップされたディレクトリから AD FS Web ページと **web.config** ファイルをコピーします。 既定では、そのファイルは **%systemdrive%\inetpub\adfs\ls** ディレクトリにあります。  
  
## <a name="next-steps"></a>次の手順
 [AD FS 2.0 フェデレーションサーバーの移行の準備](prepare-to-migrate-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーションサーバープロキシの移行の準備](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [AD FS 2.0 フェデレーションサーバー](migrate-the-ad-fs-fed-server.md)  を移行します。  
 [AD FS 2.0 フェデレーションサーバープロキシ   を移行します](migrate-the-ad-fs-2-fed-server-proxy.md)。  
 [AD FS 1.1 Web エージェントの移行](migrate-the-ad-fs-web-agent.md)