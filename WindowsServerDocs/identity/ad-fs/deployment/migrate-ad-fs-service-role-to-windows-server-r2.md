---
title: "Windows Server 2012 R2 への Active Directory フェデレーション サービスの役割サービスを移行します。"
description: "Windows Server 2012 R2 への AD FS サービスの移行についてを説明します。"
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 478729a7b6560beba5f04a1a15ad035561ad31f0
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="migrate-active-directory-federation-services-role-services-to-windows-server-2012-r2"></a>Windows Server 2012 R2 への Active Directory フェデレーション サービスの役割サービスを移行します。
 このドキュメントでは、次の役割サービスを Windows Server 2012 R2 にインストールされている Active の Directory フェデレーション サービス (AD FS) に移行する手順。  
  
-   Windows Server 2008 または Windows Server 2008 R2 にインストールされている AD FS 2.0 フェデレーション サーバー  
  
-   Windows Server 2012 にインストールされている AD FS フェデレーション サーバー  
  
## <a name="supported-migration-scenarios"></a>サポートされている移行シナリオ  
 このガイドで説明する移行手順は、次のタスクで構成されます。  
  
-   Windows Server 2008、Windows Server 2008 R2、または Windows Server 2012 を実行しているサーバーから AD FS 2.0 の構成データをエクスポートします。  
  
-   Windows Server 2008、Windows Server 2008 R2 または Windows Server 2012 から Windows Server 2012 R2 へのこのサーバーのオペレーティング システムのインプレース アップグレードを実行します。 
  
-   元の AD FS 構成を再作成し、その他の AD FS の復元でサービスの設定このサーバーは、Windows Server 2012 R2 にインストールされている AD FS サーバー役割を実行しているようになりました。  
  
 このガイドでは、複数の役割を実行しているサーバーに移行する手順については取り上げません。 サーバーが複数の役割を実行している場合、その他の役割の移行ガイドで説明されている情報に基づいて、サーバー環境に固有のカスタムの移行プロセスを設計することをお勧めします。 他の役割の移行ガイドは、[Windows Server 移行ポータル](https://go.microsoft.com/fwlink/?LinkId=247608)します。  
  
### <a name="supported-operating-systems"></a>サポートされるオペレーティング システム  
 移行先サーバーのオペレーティング システム:  
  
 Windows Server 2012 R2 (Server Core とフル インストール オプション)  
  
 移行先サーバーのプロセッサ:  
  
 x64 ベース  
  
|移行元サーバーのプロセッサ|移行元サーバーのオペレーティング システム|  
|-----------------------------|------------------------------------|  
|x86-または x64-ベース| Windows Server 2008、フルおよび Server Core インストール オプションの両方|  
|x64 ベース|Windows Server 2008 R2|  
|x64 ベース|Windows Server 2008 R2 の Server Core インストール オプション|  
|x64 ベース|Server Core と Windows Server 2012 のフル インストール オプション|  
  
> [!NOTE]
>  -   上記の表に記載されているオペレーティング システムのバージョンは、オペレーティング システムとサポートされる service pack の最も古い組み合わせです。  
> -   Windows Server オペレーティング システムの Foundation、Standard、Enterprise、および Datacenter エディションは、移行元または移行先サーバーとしてサポートされます。  
> -   物理オペレーティング システムと仮想オペレーティング システム間の移行がサポートされます。  
  
### <a name="supported-ad-fs-role-services-and-features"></a>サポートされている AD FS 役割サービスと機能  
 次の表では、AD FS 役割サービスと、このガイドで説明されているそれぞれの設定の移行シナリオについて説明します。  
  
|差出人|Windows Server 2012 R2 にインストールされた AD FS|  
|----------|----------------------------------------------------------------------------------------------|  
|Windows Server 2008 または Windows Server 2008 R2 にインストールされている AD FS 2.0 フェデレーション サーバー|同じサーバーでの移行はサポートされています。 詳細についてを参照してください。<br /><br /> [AD FS フェデレーション サーバーの移行の準備](prepare-migrate-ad-fs-server-r2.md)<br /><br /> [AD FS フェデレーション サーバーの移行](migrate-ad-fs-fed-server-r2.md)|  
|Windows Server 2012 にインストールされている AD FS フェデレーション サーバー|同じサーバーでの移行はサポートされています。  詳細をご覧ください。<br /><br /> [AD FS フェデレーション サーバーの移行の準備](prepare-migrate-ad-fs-server-r2.md)<br /><br /> [AD FS フェデレーション サーバーの移行](migrate-ad-fs-fed-server-r2.md)|  
  
## <a name="next-steps"></a>次の手順
 [AD FS フェデレーション サーバーの移行の準備](prepare-migrate-ad-fs-server-r2.md)   
 [AD FS フェデレーション サーバーの移行](migrate-ad-fs-fed-server-r2.md)   
 [AD FS フェデレーション サーバー プロキシの移行](migrate-fed-server-proxy-r2.md)   
 [Windows Server 2012 R2 への AD FS の移行の検証](verify-ad-fs-migration.md)