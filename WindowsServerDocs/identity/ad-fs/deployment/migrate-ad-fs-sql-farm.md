---
title: AD FS 2.0 フェデレーションサーバーの SQL ファームを移行する
description: AD FS 2.0 server SQL ファームを Windows Server 2012 に移行する方法について説明します。
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 3c43d26868f39896ec8632397dc0fce1dfe2dd2a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408286"
---
# <a name="migrate-an-ad-fs-20-wid-farm"></a>AD FS 2.0 WID ファームの移行  
このドキュメントでは、AD FS 2.0 SQL ファームを Windows Server 2012 に移行する方法の詳細について説明します。


## <a name="migrate-a-sql-server-farm"></a>SQL Server ファームの移行  
 SQL Server ファームを Windows Server 2012 に移行するには、次の手順を実行します。  
  
1.  SQL Server ファーム内の各サーバーについて、「 [SQL Server ファームの移行](prepare-to-migrate-a-sql-server-farm.md)」の手順を確認して実行します。  
  
2.  SQL Server ファームのすべてのサーバーをロード バランサーから削除します。  
  
3.  SQL Server ファーム内のこのサーバーのオペレーティングシステムを Windows Server 2008 R2 または Windows Server 2008 から Windows Server 2012 にアップグレードします。 詳細については、「[Windows Server 2012 のインストール](https://technet.microsoft.com/library/jj134246.aspx)」を参照してください。  
  
> [!IMPORTANT]
>  オペレーティング システムをアップグレードすると、このサーバーの AD FS 構成が失われ、AD FS 2.0 サーバーの役割が削除されます。 代わりに、Windows Server 2012 AD FS サーバーロールがインストールされますが、構成されていません。 元の AD FS 構成を手動で作成し、その他の AD FS 設定を復元して、フェデレーション サーバーの移行を完了する必要があります。  
  
4. AD FS Windows PowerShell コマンドレットを使用して SQL Server ファームのこのサーバーで元の AD FS 構成を作成し、サーバーを既存のファームに追加します。  
  
> [!IMPORTANT]
>  SQL Server を使用して AD FS 構成データベースを格納する場合は、Windows PowerShell を使用して元の AD FS 構成を作成する必要があります。  

  - Windows PowerShell を開き、 `$fscredential = Get-Credential`コマンドを実行します。  
  - SQL Server ファームの移行の準備を行っているときに記録したサービス アカウントの名前とパスワードを入力します。  
  - `Add-AdfsFarmNode -ServiceAccountCredential $fscredential -SQLConnectionString "Data Source=<Data Source>;Integrated Security=True"`コマンドを実行します。 `Data Source` は `%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config`ファイルのポリシー ストア接続文字列値のデータ ソース値です。  
  
5. Windows Server 2012 にアップグレードしたばかりのサーバーをロードバランサーに追加します。  
  
6. SQL Server ファームのその他のノードについて、手順 2. ～ 6. を繰り返します。  
  
7. SQL Server ファーム内のすべてのサーバーを Windows Server 2012 にアップグレードする場合は、カスタム属性ストアなど、その他の AD FS カスタマイズを復元します。  

## <a name="next-steps"></a>次の手順
 [AD FS 2.0 フェデレーションサーバーの移行の準備](prepare-to-migrate-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーションサーバープロキシの移行の準備](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [AD FS 2.0 フェデレーションサーバー](migrate-the-ad-fs-fed-server.md)  を移行します。  
 [AD FS 2.0 フェデレーションサーバープロキシ   を移行します](migrate-the-ad-fs-2-fed-server-proxy.md)。  
 [AD FS 1.1 Web エージェントの移行](migrate-the-ad-fs-web-agent.md)



