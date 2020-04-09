---
title: Windows Server 2012 R2 への Active Directory フェデレーション サービス (AD FS) 役割サービスの移行
description: AD FS サービスを Windows Server 2012 R2 に移行する手順について説明します。
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 6c2f9c8079eb2dfaf208c8835940351a925d0a16
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857505"
---
# <a name="migrate-active-directory-federation-services-role-services-to-windows-server-2012-r2"></a>Windows Server 2012 R2 への Active Directory フェデレーション サービス (AD FS) 役割サービスの移行
 このドキュメントでは、Windows Server 2012 R2 と共にインストールされる Active Directory フェデレーションサービス (AD FS) (AD FS) に次の役割サービスを移行する手順について説明します。  
  
-   Windows Server 2008 または Windows Server 2008 R2 にインストールされている AD FS 2.0 フェデレーションサーバー  
  
-   Windows Server 2012 にインストールされている AD FS フェデレーションサーバー  
  
## <a name="supported-migration-scenarios"></a>サポートされている移行のシナリオ  
 このガイドで説明する移行手順は次のタスクで構成されています。  
  
- Windows Server 2008、Windows Server 2008 R2、または Windows Server 2012 を実行しているサーバーから AD FS 2.0 構成データをエクスポートする  
  
- Windows Server 2008、Windows Server 2008 R2、または Windows Server 2012 から Windows Server 2012 R2 への、このサーバーのオペレーティングシステムの一括アップグレードを実行します。 
  
- 元の AD FS 構成を再作成し、このサーバーの残りの AD FS サービス設定を復元します。これで、Windows Server 2012 R2 と共にインストールされる AD FS サーバーロールが実行されます。  
  
  このガイドでは、複数の役割を実行しているサーバーを移行する手順は取り上げません。 サーバーで複数の役割が実行されている場合は、他の役割の移行ガイドで説明されている情報に基づいて、サーバー環境に合わせたカスタムの移行プロセスを設計することをお勧めします。 他の役割に関する移行ガイドは、「 [Windows Server の移行に関するポータル](https://go.microsoft.com/fwlink/?LinkId=247608)」を参照してください。  
  
### <a name="supported-operating-systems"></a>サポートされるオペレーティング システム  
 移行先サーバーのオペレーティングシステム:  
  
 Windows Server 2012 R2 (Server Core およびフルインストールオプション)  
  
 移行先サーバーのプロセッサ:  
  
 x64 ベース●x64べーす○  
  
|移行元サーバーのプロセッサ|移行元サーバーのオペレーティング システム|  
|-----------------------------|------------------------------------|  
|x86 または x64 ベース| Windows Server 2008 (フルインストールオプションと Server Core インストールオプションの両方)|  
|x64 ベース●x64べーす○|Windows Server 2008 R2|  
|x64 ベース●x64べーす○|Windows Server 2008 R2 の server Core インストールオプション|  
|x64 ベース●x64べーす○|Windows Server 2012 の server Core およびフルインストールオプション|  
  
> [!NOTE]
> - 上の表で示したオペレーティング システムのバージョンは、サポートされている最も古い組み合わせでのオペレーティング システムとサービス パックについてのものです。  
>   -   Windows Server オペレーティングシステムの Foundation、Standard、Enterprise、Datacenter の各エディションは、移行元または移行先のサーバーとしてサポートされています。  
>   -   物理的なオペレーティング システムと仮想化されたオペレーティング システム間での移行はサポートされています。  
  
### <a name="supported-ad-fs-role-services-and-features"></a>サポートされている AD FS 役割サービスと機能  
 次の表では、このガイドで説明されている AD FS の役割サービスとそれぞれの設定の移行シナリオについて説明します。  
  
|移行元|Windows Server 2012 R2 と共にインストール AD FS には|  
|----------|----------------------------------------------------------------------------------------------|  
|Windows Server 2008 または Windows Server 2008 R2 にインストールされている AD FS 2.0 フェデレーションサーバー|同じサーバーでの移行がサポートされています。 詳しくは、次のトピックをご覧ください。<p> [AD FS フェデレーションサーバーを移行する準備をしています](prepare-migrate-ad-fs-server-r2.md)<p> [AD FS フェデレーションサーバーの移行](migrate-ad-fs-fed-server-r2.md)|  
|Windows Server 2012 にインストールされている AD FS フェデレーションサーバー|同じサーバーでの移行がサポートされています。  詳細については、次のトピックを参照してください。<p> [AD FS フェデレーションサーバーを移行する準備をしています](prepare-migrate-ad-fs-server-r2.md)<p> [AD FS フェデレーションサーバーの移行](migrate-ad-fs-fed-server-r2.md)|  
  
## <a name="next-steps"></a>次の手順
 [AD FS フェデレーションサーバー  を移行する準備をしています](prepare-migrate-ad-fs-server-r2.md)  
 [AD FS フェデレーションサーバー  の移行](migrate-ad-fs-fed-server-r2.md)  
 [AD FS フェデレーションサーバープロキシ  の移行](migrate-fed-server-proxy-r2.md)  
 [Windows Server 2012 R2 への AD FS 移行の検証](verify-ad-fs-migration.md)