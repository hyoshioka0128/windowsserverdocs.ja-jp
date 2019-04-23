---
title: AD FS 2.0 フェデレーション サーバーの SQL ファームを移行します。
description: Windows Server 2012 への AD FS 2.0 サーバー SQL ファームの移行に関する情報を提供します。
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 8433219850793aa34b646a3bf14cba42d3de4988
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843573"
---
# <a name="migrate-an-ad-fs-20-wid-farm"></a>AD FS 2.0 WID ファームを移行します。  
このドキュメントでは、Windows Server 2012 への AD FS 2.0 SQL ファームの移行に関する詳細情報を示します。


## <a name="migrate-a-sql-server-farm"></a>SQL Server ファームの移行  
 SQL Server ファームを Windows Server 2012 に移行するには、次の手順を実行します。  
  
1.  SQL Server ファームの各サーバーについて確認し、実行手順では、 [SQL Server ファームの移行](prepare-to-migrate-a-sql-server-farm.md)します。  
  
2.  SQL Server ファームのすべてのサーバーをロード バランサーから削除します。  
  
3.  Windows Server 2008 R2 または Windows Server 2008 から SQL Server ファーム内のこのサーバー上のオペレーティング システムを Windows Server 2012 にアップグレードします。 詳細については、「[Windows Server 2012 のインストール](https://technet.microsoft.com/library/jj134246.aspx)」を参照してください。  
  
> [!IMPORTANT]
>  オペレーティング システムをアップグレードすると、このサーバーの AD FS 構成が失われ、AD FS 2.0 サーバーの役割が削除されます。 Windows Server 2012 の AD FS サーバーの役割が代わりに、インストールされているが構成されていません。 元の AD FS 構成を手動で作成し、その他の AD FS 設定を復元して、フェデレーション サーバーの移行を完了する必要があります。  
  
4.  AD FS Windows PowerShell コマンドレットを使用して SQL Server ファームのこのサーバーで元の AD FS 構成を作成し、サーバーを既存のファームに追加します。  
  
> [!IMPORTANT]
>  SQL Server を使用して AD FS 構成データベースを格納する場合は、Windows PowerShell を使用して元の AD FS 構成を作成する必要があります。  

  - Windows PowerShell を開き、 `$fscredential = Get-Credential`コマンドを実行します。  
  - SQL Server ファームの移行の準備を行っているときに記録したサービス アカウントの名前とパスワードを入力します。  
  - `Add-AdfsFarmNode -ServiceAccountCredential $fscredential -SQLConnectionString "Data Source=<Data Source>;Integrated Security=True"`コマンドを実行します。 `Data Source` は `%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config`ファイルのポリシー ストア接続文字列値のデータ ソース値です。  
  
5.  ロード バランサーに Windows Server 2012 にアップグレードしたサーバーを追加します。  
  
6.  SQL Server ファームのその他のノードについて、手順 2. ～ 6. を繰り返します。  
  
7.  すべての SQL Server ファームにサーバーが Windows Server 2012 にアップグレードするときに、カスタム属性ストアなど、他の AD FS カスタマイズを復元します。  

## <a name="next-steps"></a>次の手順
 [AD FS 2.0 フェデレーション サーバーの移行を準備します。](prepare-to-migrate-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーション サーバー プロキシの移行を準備します。](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [AD FS 2.0 フェデレーション サーバーを移行します。](migrate-the-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーション サーバー プロキシを移行します。](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [AD FS 1.1 Web エージェントを移行します。](migrate-the-ad-fs-web-agent.md)



