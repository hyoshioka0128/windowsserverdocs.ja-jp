---
title: Windows Server 2012 への Active Directory フェデレーション サービス (AD FS) 役割サービスの移行
description: Windows Server 2012 に AD FS サービスを移行する方法について説明します。
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 63dc9825b9c9b8a06d0946859e08a536589eb044
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445700"
---
# <a name="migrate-active-directory-federation-services-role-services-to-windows-server-2012"></a>Windows Server 2012 への Active Directory フェデレーション サービス (AD FS) 役割サービスの移行

次は、次の役割サービスを Active Directory フェデレーション サービス (AD FS) Windows Server 2012 に移行する方法の手順を示します。  
  
-   AD FS 1.1 Windows トークン ベースのエージェントと AD FS 1.1 クレーム認識エージェントを Windows Server 2008 または Windows Server 2008 R2 と共にインストール  
  
-   AD FS 2.0 フェデレーション サーバーと Windows Server 2008 または Windows Server 2008 R2 にインストールされている AD FS 2.0 フェデレーション サーバー プロキシ    
  
## <a name="supported-migration-scenarios"></a>サポートされている移行のシナリオ  
 移行の手順には、次のタスクが含まれています。  
  
- Windows Server 2008 R2 または Windows Server 2008 が実行されている、サーバーから AD FS 2.0 の構成データをエクスポートします。  
  
- Windows Server 2008 または Windows Server 2008 R2 から Windows Server 2012 へのこのサーバーのオペレーティング システムのインプレース アップグレードを実行します。
  
- 元の AD FS 構成を再作成し、その他の AD FS の復元のサービス設定でこのサーバーは、Windows Server 2012 と共にインストールされる AD FS サーバーの役割を実行しているようになりました。  
  
  このガイドでは、複数の役割を実行しているサーバーを移行する手順は取り上げません。 サーバーで複数の役割が実行されている場合は、他の役割の移行ガイドで説明されている情報に基づいて、サーバー環境に合わせたカスタムの移行プロセスを設計することをお勧めします。 他の役割に関する移行ガイドは、「 [Windows Server の移行に関するポータル](https://go.microsoft.com/fwlink/?LinkId=247608)」を参照してください。  
  
## <a name="supported-operating-systems"></a>サポートされるオペレーティング システム  
 **移行先サーバーのオペレーティング システム:**  
  

- Windows Server 2012 または Windows Server 2008 R2 (Server Core とフル インストール オプション)  
  
  **移行先サーバーのプロセッサ:**  
  

- x64 ベース  
  
|移行元サーバーのプロセッサ|移行元サーバーのオペレーティング システム|  
|-----|-----|  
|x86 または x64 ベース|Windows Server 2003 Service Pack 2|  
|x86 または x64 ベース|Windows Server 2003 R2|  
|x86 または x64 ベース|完全と Server Core インストール オプションの両方に、Windows Server 2008|  
|x64 ベース|Windows Server 2008 R2|  
|x64 ベース|Windows Server 2008 R2 の server Core インストール オプション|  
|x64 ベース|Server Core と Windows Server 2012 のフル インストール オプション|  
  
> [!NOTE]
> - 上の表で示したオペレーティング システムのバージョンは、サポートされている最も古い組み合わせでのオペレーティング システムとサービス パックについてのものです。  
>   -   Windows Server オペレーティング システムの Foundation、Standard、Enterprise、および Datacenter エディションは、ソースまたは移行先サーバーとしてサポートされます。  
>   -   物理的なオペレーティング システムと仮想化されたオペレーティング システム間での移行はサポートされています。  
  
### <a name="supported-ad-fs-role-services-and-features"></a>サポートされている AD FS 役割サービスと機能  
 次の表では、AD FS の役割サービスと、このガイドで説明されているそれぞれの設定の移行シナリオについて説明します。  
  
|From|AD FS を Windows Server 2012 と共にインストールするには|  
|----------|-----|  
|Windows Server 2003 R2 にインストールされている AD FS 1.0 フェデレーション サーバー|移行はサポートされていません|  
|AD FS 1.0 フェデレーション サーバー プロキシの Windows Server 2003 R2 にインストールされています。|移行はサポートされていません|  
|Windows Server 2003 R2 にインストールされている、AD FS 1.0 Windows トークン ベース エージェント|移行はサポートされていません|  
|AD FS 1.0 要求に対応するエージェント Windows Server 2003 R2 にインストールされている)|移行はサポートされていません|  
|Windows Server 2008 または Windows Server 2008 R2 にインストールされている AD FS 1.1 フェデレーション サーバー|移行はサポートされていません|  
|AD FS 1.1 フェデレーション サーバー プロキシの Windows Server 2008 または Windows Server 2008 R2 と共にインストール|移行はサポートされていません|  
|Windows Server 2008 または Windows Server 2008 R2 でインストールされた、AD FS 1.1 Windows トークン ベース エージェント|同じサーバーでの移行がサポートされていますが、移行された AD FS Windows トークン ベース エージェントは Windows Server 2008 または Windows Server 2008 R2 にインストールされている AD FS 1.1 フェデレーション サービスでのみ機能します。 詳しくは、次のトピックをご覧ください。<br /><br /> [AD FS 1.1 Web エージェントの移行](migrate-the-ad-fs-web-agent.md)<br /><br /> [AD FS 1.x との相互運用](Interoperating-with-AD-FS-1.x.md)|  
|AD FS 1.1 クレーム認識エージェントと共に Windows Server 2008 または Windows Server 2008 R2 インストール)|同じサーバーでの移行がサポートされています。 移行された AD FS 1.1 クレーム認識 web エージェントは、次のように機能します。<br /><br /> Windows Server 2008 または Windows Server 2008 R2 で AD FS 1.1 フェデレーション サービスがインストールされています。<br /><br /> Windows Server 2008 または Windows Server 2008 R2 にインストールされている AD FS 2.0 フェデレーション サービス<br /><br /> Windows Server 2012 で AD FS フェデレーション サービスがインストールされています。<br /><br /> 詳しくは、次のトピックをご覧ください。<br /><br /> [AD FS 1.1 Web エージェントの移行](migrate-the-ad-fs-web-agent.md)<br /><br /> [AD FS 1.x との相互運用](Interoperating-with-AD-FS-1.x.md)|  
|Windows Server 2008 または Windows Server 2008 R2 にインストールされている AD FS 2.0 フェデレーション サーバー|同じサーバーでの移行がサポートされています。 詳しくは、次のトピックをご覧ください。<br /><br /> [AD FS 2.0 フェデレーション サーバーの移行の準備](prepare-to-migrate-ad-fs-fed-server.md)<br /><br /> [AD FS 2.0 フェデレーション サーバーの移行](migrate-the-ad-fs-fed-server.md)|  
|AD FS 2.0 フェデレーション サーバー プロキシの Windows Server 2008 または Windows Server 2008 R2 にインストールされています。|同じサーバーでの移行がサポートされています。  詳しくは、次のトピックをご覧ください。<br /><br /> [AD FS 2.0 フェデレーション サーバー プロキシの移行の準備](prepare-to-migrate-ad-fs-fed-proxy.md)<br /><br /> [AD FS 2.0 フェデレーション サーバー プロキシの移行](migrate-the-ad-fs-2-fed-server-proxy.md)|  
  
## <a name="see-also"></a>関連項目  
 [AD FS 2.0 フェデレーション サーバーの移行を準備します。](prepare-to-migrate-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーション サーバー プロキシの移行を準備します。](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [AD FS 2.0 フェデレーション サーバーを移行します。](migrate-the-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーション サーバー プロキシを移行します。](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [AD FS 1.1 Web エージェントの移行](migrate-the-ad-fs-web-agent.md)