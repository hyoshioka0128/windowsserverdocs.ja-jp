---
title: "AD FS 2.0 フェデレーション サーバーの SQL ファームを移行します。"
description: "Windows Server 2012 への AD FS 2.0 サーバー SQL ファームの移行に関する情報を提供します。"
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 8433219850793aa34b646a3bf14cba42d3de4988
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="migrate-an-ad-fs-20-wid-farm"></a>AD FS 2.0 WID ファームを移行します。  
このドキュメントでは、Windows Server 2012 への AD FS 2.0 SQL ファームの移行の詳細を提供します。


## <a name="migrate-a-sql-server-farm"></a>SQL Server ファームを移行します。  
 SQL Server ファームを Windows Server 2012 に移行するには、次の手順を実行します。  
  
1.  SQL Server ファームの各サーバーで確認し、手順を実行[SQL Server ファームの移行](prepare-to-migrate-a-sql-server-farm.md)します。  
  
2.  任意のサーバーを SQL Server ファームのロード バランサーから削除します。  
  
3.  Windows Server 2008 R2 または Windows Server 2008 から SQL Server ファーム内のこのサーバー上のオペレーティング システムを Windows Server 2012 にアップグレードします。 詳細については、次を参照してください。[Windows Server 2012 のインストール](https://technet.microsoft.com/library/jj134246.aspx)します。  
  
> [!IMPORTANT]
>  オペレーティング システムのアップグレードの結果、このサーバーの AD FS 構成が失われたと AD FS 2.0 サーバーの役割が削除されます。 Windows Server 2012 の AD FS サーバーの役割が代わりに、インストールされているが構成されていません。 手動で元の AD FS 構成を作成して、フェデレーション サーバーの移行を完了する他の AD FS 設定を復元する必要があります。  
  
4.  既存のファームにサーバーを追加する AD FS Windows PowerShell コマンドレットを使用して SQL Server ファームのこのサーバー上の元の AD FS 構成を作成します。  
  
> [!IMPORTANT]
>  Windows PowerShell を使用して、AD FS 構成データベースを格納する SQL Server を使用している場合は、元の AD FS 構成を作成する必要があります。  

  - Windows PowerShell を開き、次のコマンドを実行します。`$fscredential = Get-Credential`します。  
  - 名前と SQL Server ファームの移行の準備中に記録したサービス アカウントのパスワードを入力します。  
  - 次のコマンドを実行します。`Add-AdfsFarmNode -ServiceAccountCredential $fscredential -SQLConnectionString "Data Source=<Data Source>;Integrated Security=True"`ここで、`Data Source`は、次のファイルのポリシー ストア接続文字列値のデータ ソース値:`%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config`します。  
  
5.  ロード バランサーに Windows Server 2012 にアップグレードしたサーバーを追加します。  
  
6.  SQL Server ファームの残りのノードで、手順 2 ~ 6 を繰り返します。  
  
7.  すべての SQL Server ファームにサーバーが Windows Server 2012 にアップグレードするときに、カスタム属性ストアなどその他の AD FS カスタマイズを復元します。  

## <a name="next-steps"></a>次の手順
 [AD FS 2.0 フェデレーション サーバーの移行を準備します。](prepare-to-migrate-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーション サーバー プロキシの移行を準備します。](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [AD FS 2.0 フェデレーション サーバーを移行します。](migrate-the-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーション サーバー プロキシを移行します。](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [AD FS 1.1 Web エージェントを移行します。](migrate-the-ad-fs-web-agent.md)



