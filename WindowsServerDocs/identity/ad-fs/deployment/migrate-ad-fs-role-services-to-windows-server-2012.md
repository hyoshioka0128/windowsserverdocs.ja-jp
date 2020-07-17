---
title: Windows Server 2012 への Active Directory フェデレーション サービス (AD FS) 役割サービスの移行
description: AD FS サービスを Windows Server 2012 に移行する手順について説明します。
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 36d37eb2cc886d9831b995aa8cfdda16765994b8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857515"
---
# <a name="migrate-active-directory-federation-services-role-services-to-windows-server-2012"></a>Windows Server 2012 への Active Directory フェデレーション サービス (AD FS) 役割サービスの移行

以下では、Windows Server 2012 の Active Directory フェデレーションサービス (AD FS) (AD FS) に次の役割サービスを移行する手順について説明します。  
  
-   AD FS 1.1 Windows トークンベースのエージェント、および Windows Server 2008 または Windows Server 2008 R2 と共にインストールされた1.1 信頼性情報を認識するエージェント AD FS  
  
-   AD FS 2.0 フェデレーションサーバーおよび AD FS 2.0 フェデレーションサーバープロキシが Windows Server 2008 または Windows Server 2008 R2 にインストールされている    
  
## <a name="supported-migration-scenarios"></a>サポートされている移行のシナリオ  
 移行手順には、次のタスクが含まれています。  
  
- Windows Server 2008 または Windows Server 2008 R2 を実行しているサーバーから AD FS 2.0 構成データをエクスポートする  
  
- Windows Server 2008 または Windows Server 2008 R2 から Windows Server 2012 への、このサーバーのオペレーティングシステムの一括アップグレードを実行します。
  
- 元の AD FS 構成を再作成し、このサーバーの残りの AD FS サービス設定を復元します。これで、Windows Server 2012 と共にインストールされる AD FS サーバーロールが実行されます。  
  
  このガイドでは、複数の役割を実行しているサーバーを移行する手順は取り上げません。 サーバーで複数の役割が実行されている場合は、他の役割の移行ガイドで説明されている情報に基づいて、サーバー環境に合わせたカスタムの移行プロセスを設計することをお勧めします。 他の役割に関する移行ガイドは、「 [Windows Server の移行に関するポータル](https://go.microsoft.com/fwlink/?LinkId=247608)」を参照してください。  
  
## <a name="supported-operating-systems"></a>サポートされるオペレーティング システム  
 **移行先サーバーのオペレーティングシステム:**  
  

- Windows Server 2012 または Windows Server 2008 R2 (Server Core およびフルインストールオプション)  
  
  **移行先サーバーのプロセッサ:**  
  

- x64 ベース●x64べーす○  
  
|移行元サーバーのプロセッサ|移行元サーバーのオペレーティング システム|  
|-----|-----|  
|x86 または x64 ベース|Windows Server 2003 Service Pack 2|  
|x86 または x64 ベース|Windows Server 2003 R2|  
|x86 または x64 ベース|Windows Server 2008 (フルインストールオプションと Server Core インストールオプションの両方)|  
|x64 ベース●x64べーす○|Windows Server 2008 R2|  
|x64 ベース●x64べーす○|Windows Server 2008 R2 の server Core インストールオプション|  
|x64 ベース●x64べーす○|Windows Server 2012 の server Core およびフルインストールオプション|  
  
> [!NOTE]
> - 上の表で示したオペレーティング システムのバージョンは、サポートされている最も古い組み合わせでのオペレーティング システムとサービス パックについてのものです。  
>   -   Windows Server オペレーティングシステムの Foundation、Standard、Enterprise、Datacenter の各エディションは、移行元または移行先のサーバーとしてサポートされています。  
>   -   物理的なオペレーティング システムと仮想化されたオペレーティング システム間での移行はサポートされています。  
  
### <a name="supported-ad-fs-role-services-and-features"></a>サポートされている AD FS 役割サービスと機能  
 次の表では、このガイドで説明されている AD FS の役割サービスとそれぞれの設定の移行シナリオについて説明します。  
  
|移行元|Windows Server 2012 でインストールされた AD FS するには|  
|----------|-----|  
|Windows Server 2003 R2 と共にインストールされた AD FS 1.0 フェデレーションサーバー|移行はサポートされていません|  
|AD FS 1.0 フェデレーションサーバープロキシが Windows Server 2003 R2 と共にインストールされている|移行はサポートされていません|  
|Windows Server 2003 R2 と共にインストールされた Windows トークンベースのエージェント AD FS 1.0|移行はサポートされていません|  
|AD FS 1.0 Windows Server 2003 R2 と共にインストールされる要求に対応するエージェント)|移行はサポートされていません|  
|Windows Server 2008 または Windows Server 2008 R2 と共にインストールされた AD FS 1.1 フェデレーションサーバー|移行はサポートされていません|  
|Windows Server 2008 または Windows Server 2008 R2 と共にインストールされた AD FS 1.1 フェデレーションサーバープロキシ|移行はサポートされていません|  
|Windows Server 2008 または Windows Server 2008 R2 と共にインストールされた Windows トークンベースのエージェント AD FS 1.1|同じサーバーでの移行はサポートされていますが、移行された AD FS Windows トークンベースのエージェントは、Windows Server 2008 または Windows Server 2008 R2 と共にインストールされた AD FS 1.1 フェデレーションサービスでのみ機能します。 詳しくは、次のトピックをご覧ください。<p> [AD FS 1.1 Web エージェントの移行](migrate-the-ad-fs-web-agent.md)<p> [AD FS 1.x との相互運用](Interoperating-with-AD-FS-1.x.md)|  
|AD FS 1.1 Windows Server 2008 または Windows Server 2008 R2 と共にインストールされる要求対応エージェント)|同じサーバーでの移行がサポートされています。 移行された AD FS 1.1 要求に対応する web エージェントは、次の機能を備えています。<p> Windows Server 2008 または Windows Server 2008 R2 と共にインストールされた AD FS 1.1 フェデレーションサービス<p> Windows Server 2008 または Windows Server 2008 R2 にインストールされている AD FS 2.0 フェデレーションサービス<p> Windows Server 2012 にインストールされている AD FS フェデレーションサービス<p> 詳しくは、次のトピックをご覧ください。<p> [AD FS 1.1 Web エージェントの移行](migrate-the-ad-fs-web-agent.md)<p> [AD FS 1.x との相互運用](Interoperating-with-AD-FS-1.x.md)|  
|Windows Server 2008 または Windows Server 2008 R2 にインストールされている AD FS 2.0 フェデレーションサーバー|同じサーバーでの移行がサポートされています。 詳しくは、次のトピックをご覧ください。<p> [AD FS 2.0 フェデレーション サーバーの移行の準備](prepare-to-migrate-ad-fs-fed-server.md)<p> [AD FS 2.0 フェデレーション サーバーの移行](migrate-the-ad-fs-fed-server.md)|  
|Windows Server 2008 または Windows Server 2008 R2 にインストールされている AD FS 2.0 フェデレーションサーバープロキシ|同じサーバーでの移行がサポートされています。  詳細については、次のトピックを参照してください。<p> [AD FS 2.0 フェデレーション サーバー プロキシの移行の準備](prepare-to-migrate-ad-fs-fed-proxy.md)<p> [AD FS 2.0 フェデレーション サーバー プロキシの移行](migrate-the-ad-fs-2-fed-server-proxy.md)|  
  
## <a name="see-also"></a>参照  
 [AD FS 2.0 フェデレーションサーバー  の移行の準備](prepare-to-migrate-ad-fs-fed-server.md)  
 [AD FS 2.0 フェデレーションサーバープロキシの移行の準備](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [AD FS 2.0 フェデレーションサーバー  を移行します](migrate-the-ad-fs-fed-server.md)。  
 [AD FS 2.0 フェデレーションサーバープロキシ  を移行します](migrate-the-ad-fs-2-fed-server-proxy.md)。  
 [AD FS 1.1 Web エージェントの移行](migrate-the-ad-fs-web-agent.md)