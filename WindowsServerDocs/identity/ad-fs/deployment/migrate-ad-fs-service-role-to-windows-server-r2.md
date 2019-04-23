---
title: Windows Server 2012 R2 への Active Directory フェデレーション サービス (AD FS) 役割サービスの移行
description: Windows Server 2012 R2 に AD FS サービスを移行する方法について説明します。
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 478729a7b6560beba5f04a1a15ad035561ad31f0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847953"
---
# <a name="migrate-active-directory-federation-services-role-services-to-windows-server-2012-r2"></a>Windows Server 2012 R2 への Active Directory フェデレーション サービス (AD FS) 役割サービスの移行
 ここでは、Windows Server 2012 R2 と共にインストールされている Active の Directory フェデレーション サービス (AD FS) に次の役割サービスを移行する手順を説明します。  
  
-   Windows Server 2008 または Windows Server 2008 R2 にインストールされている AD FS 2.0 フェデレーション サーバー  
  
-   Windows Server 2012 にインストールされている AD FS フェデレーション サーバー  
  
## <a name="supported-migration-scenarios"></a>サポートされている移行のシナリオ  
 このガイドで説明する移行手順は次のタスクで構成されています。  
  
-   Windows Server 2008、Windows Server 2008 R2、または Windows Server 2012 を実行しているサーバーから AD FS 2.0 の構成データをエクスポートします。  
  
-   Windows Server 2008、Windows Server 2008 R2 または Windows Server 2012 から Windows Server 2012 R2 へのこのサーバーのオペレーティング システムのインプレース アップグレードを実行します。 
  
-   元の AD FS 構成を再作成し、その他の AD FS の復元のサービス設定でこのサーバーは、Windows Server 2012 R2 と共にインストールされる AD FS サーバーの役割を実行しているようになりました。  
  
 このガイドでは、複数の役割を実行しているサーバーを移行する手順は取り上げません。 サーバーで複数の役割が実行されている場合は、他の役割の移行ガイドで説明されている情報に基づいて、サーバー環境に合わせたカスタムの移行プロセスを設計することをお勧めします。 他の役割に関する移行ガイドは、「 [Windows Server の移行に関するポータル](https://go.microsoft.com/fwlink/?LinkId=247608)」を参照してください。  
  
### <a name="supported-operating-systems"></a>サポートされるオペレーティング システム  
 移行先サーバーのオペレーティング システム:  
  
 Windows Server 2012 R2 (Server Core とフル インストール オプション)  
  
 移行先サーバーのプロセッサ:  
  
 x64 ベース  
  
|移行元サーバーのプロセッサ|移行元サーバーのオペレーティング システム|  
|-----------------------------|------------------------------------|  
|x86 または x64 ベース| 完全と Server Core インストール オプションの両方に、Windows Server 2008|  
|x64 ベース|Windows Server 2008 R2|  
|x64 ベース|Windows Server 2008 R2 の server Core インストール オプション|  
|x64 ベース|Server Core と Windows Server 2012 のフル インストール オプション|  
  
> [!NOTE]
>  -   上の表で示したオペレーティング システムのバージョンは、サポートされている最も古い組み合わせでのオペレーティング システムとサービス パックについてのものです。  
> -   Windows Server オペレーティング システムの Foundation、Standard、Enterprise、および Datacenter エディションは、ソースまたは移行先サーバーとしてサポートされます。  
> -   物理的なオペレーティング システムと仮想化されたオペレーティング システム間での移行はサポートされています。  
  
### <a name="supported-ad-fs-role-services-and-features"></a>サポートされている AD FS 役割サービスと機能  
 次の表では、AD FS の役割サービスと、このガイドで説明されているそれぞれの設定の移行シナリオについて説明します。  
  
|From|AD FS を Windows Server 2012 R2 と共にインストールするには|  
|----------|----------------------------------------------------------------------------------------------|  
|Windows Server 2008 または Windows Server 2008 R2 にインストールされている AD FS 2.0 フェデレーション サーバー|同じサーバーでの移行がサポートされています。 詳しくは、次のトピックをご覧ください。<br /><br /> [AD FS フェデレーション サーバーの移行の準備](prepare-migrate-ad-fs-server-r2.md)<br /><br /> [AD FS フェデレーション サーバーの移行](migrate-ad-fs-fed-server-r2.md)|  
|Windows Server 2012 にインストールされている AD FS フェデレーション サーバー|同じサーバーでの移行がサポートされています。  詳しくは、次のトピックをご覧ください。<br /><br /> [AD FS フェデレーション サーバーの移行の準備](prepare-migrate-ad-fs-server-r2.md)<br /><br /> [AD FS フェデレーション サーバーの移行](migrate-ad-fs-fed-server-r2.md)|  
  
## <a name="next-steps"></a>次の手順
 [AD FS フェデレーション サーバーの移行の準備](prepare-migrate-ad-fs-server-r2.md)   
 [AD FS フェデレーション サーバーの移行](migrate-ad-fs-fed-server-r2.md)   
 [AD FS フェデレーション サーバー プロキシの移行](migrate-fed-server-proxy-r2.md)   
 [Windows Server 2012 R2 への AD FS の移行の検証](verify-ad-fs-migration.md)