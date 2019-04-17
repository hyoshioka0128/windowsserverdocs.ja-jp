---
title: "Windows Server 2012 への Active Directory フェデレーション サービスの役割サービスを移行します。"
description: "Windows Server 2012 に AD FS サービスを移行するための手順を示します。"
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 2b44ed504c2b3dc8a8ac0ca9648f1db9e362e075
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="migrate-active-directory-federation-services-role-services-to-windows-server-2012"></a>Windows Server 2012 への Active Directory フェデレーション サービスの役割サービスを移行します。

次に Active Directory フェデレーション サービス (AD FS) Windows Server 2012 で、次の役割サービスを移行するのに指示を提供します。  
  
-   AD FS 1.1 Windows トークン ベース エージェントと AD FS 1.1 要求に対応する Windows Server 2008 または Windows Server 2008 R2 にインストールされているエージェント  
  
-   AD FS 2.0 フェデレーション サーバーと Windows Server 2008 または Windows Server 2008 R2 にインストールされている AD FS 2.0 フェデレーション サーバー プロキシ    
  
## <a name="supported-migration-scenarios"></a>サポートされている移行シナリオ  
 移行の手順には、次のタスクが含まれています。  
  
-   Windows Server 2008 を実行しているサーバーまたは Windows Server 2008 R2 から AD FS 2.0 の構成データをエクスポートします。  
  
-   Windows Server 2008 または Windows Server 2008 R2 から Windows Server 2012 へのこのサーバーのオペレーティング システムのインプレース アップグレードを実行します。
  
-   元の AD FS 構成を再作成し、その他の AD FS の復元でサービスの設定このサーバーは、Windows Server 2012 にインストールされている AD FS サーバー役割を実行しているようになりました。  
  
 このガイドでは、複数の役割を実行しているサーバーに移行する手順については取り上げません。 サーバーが複数の役割を実行している場合、その他の役割の移行ガイドで説明されている情報に基づいて、サーバー環境に固有のカスタムの移行プロセスを設計することをお勧めします。 他の役割の移行ガイドは、[Windows Server 移行ポータル](https://go.microsoft.com/fwlink/?LinkId=247608)します。  
  
## <a name="supported-operating-systems"></a>サポートされるオペレーティング システム  
 **移行先サーバーのオペレーティング システム:**  
  

-  Windows Server 2012 または Windows Server 2008 R2 (Server Core とフル インストール オプション)  
  
 **移行先サーバーのプロセッサ:**  
  

-  x64 ベース  
  
|移行元サーバーのプロセッサ|移行元サーバーのオペレーティング システム|  
|-----|-----|  
|x86-または x64-ベース|Windows Server 2003 Service Pack 2|  
|x86-または x64-ベース|Windows Server 2003 R2|  
|x86-または x64-ベース|Windows Server 2008、フルおよび Server Core インストール オプションの両方|  
|x64 ベース|Windows Server 2008 R2|  
|x64 ベース|Windows Server 2008 R2 の Server Core インストール オプション|  
|x64 ベース|Server Core と Windows Server 2012 のフル インストール オプション|  
  
> [!NOTE]
>  -   上記の表に記載されているオペレーティング システムのバージョンは、オペレーティング システムとサポートされる service pack の最も古い組み合わせです。  
> -   Windows Server オペレーティング システムの Foundation、Standard、Enterprise、および Datacenter エディションは、移行元または移行先サーバーとしてサポートされます。  
> -   物理オペレーティング システムと仮想オペレーティング システム間の移行がサポートされます。  
  
### <a name="supported-ad-fs-role-services-and-features"></a>サポートされている AD FS 役割サービスと機能  
 次の表では、AD FS 役割サービスと、このガイドで説明されているそれぞれの設定の移行シナリオについて説明します。  
  
|差出人|Windows Server 2012 にインストールされた AD FS|  
|----------|-----|  
|Windows Server 2003 R2 にインストールされている AD FS 1.0 フェデレーション サーバー|移行がサポートされていません|  
|Windows Server 2003 R2 にインストールされている AD FS 1.0 フェデレーション サーバー プロキシ|移行がサポートされていません|  
|Windows Server 2003 R2 にインストールされている、[AD FS 1.0 Windows トークン ベース エージェント|移行がサポートされていません|  
|AD FS 1.0 要求に対応するエージェント Windows Server 2003 R2 にインストールされている)|移行がサポートされていません|  
|Windows Server 2008 または Windows Server 2008 R2 にインストールされている AD FS 1.1 フェデレーション サーバー|移行がサポートされていません|  
|Windows Server 2008 または Windows Server 2008 R2 にインストールされている AD FS 1.1 フェデレーション サーバー プロキシ|移行がサポートされていません|  
|Windows Server 2008 または Windows Server 2008 R2 にインストールされている、[AD FS 1.1 Windows トークン ベース エージェント|同じサーバーでの移行はサポートしますが、移行された AD FS Windows トークン ベース エージェントは Windows Server 2008 または Windows Server 2008 R2 にインストールされている AD FS 1.1 フェデレーション サービスでのみ機能します。 詳細についてを参照してください。<br /><br /> [AD FS 1.1 Web エージェントを移行します。](migrate-the-ad-fs-web-agent.md)<br /><br /> [Interoperating with AD FS 1.x](Interoperating-with-AD-FS-1.x.md)|  
|AD FS 1.1 要求に対応するエージェント Windows Server 2008 または Windows Server 2008 R2 にインストールされている)|同じサーバーでの移行はサポートされています。 移行された AD FS 1.1 クレーム認識 Web エージェントは、次のように機能します。<br /><br /> Windows Server 2008 または Windows Server 2008 R2 にインストールされている AD FS 1.1 フェデレーション サービス<br /><br /> Windows Server 2008 または Windows Server 2008 R2 にインストールされている AD FS 2.0 フェデレーション サービス<br /><br /> Windows Server 2012 にインストールされている AD FS フェデレーション サービス<br /><br /> 詳細についてを参照してください。<br /><br /> [AD FS 1.1 Web エージェントを移行します。](migrate-the-ad-fs-web-agent.md)<br /><br /> [Interoperating with AD FS 1.x](Interoperating-with-AD-FS-1.x.md)|  
|Windows Server 2008 または Windows Server 2008 R2 にインストールされている AD FS 2.0 フェデレーション サーバー|同じサーバーでの移行はサポートされています。 詳細についてを参照してください。<br /><br /> [AD FS 2.0 フェデレーション サーバーの移行を準備します。](prepare-to-migrate-ad-fs-fed-server.md)<br /><br /> [AD FS 2.0 フェデレーション サーバーを移行します。](migrate-the-ad-fs-fed-server.md)|  
|Windows Server 2008 または Windows Server 2008 R2 にインストールされている AD FS 2.0 フェデレーション サーバー プロキシ|同じサーバーでの移行はサポートされています。  詳細をご覧ください。<br /><br /> [AD FS 2.0 フェデレーション サーバー プロキシの移行を準備します。](prepare-to-migrate-ad-fs-fed-proxy.md)<br /><br /> [AD FS 2.0 フェデレーション サーバー プロキシを移行します。](migrate-the-ad-fs-2-fed-server-proxy.md)|  
  
## <a name="see-also"></a>参照してください。  
 [AD FS 2.0 フェデレーション サーバーの移行を準備します。](prepare-to-migrate-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーション サーバー プロキシの移行を準備します。](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [AD FS 2.0 フェデレーション サーバーを移行します。](migrate-the-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーション サーバー プロキシを移行します。](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [AD FS 1.1 Web エージェントを移行します。](migrate-the-ad-fs-web-agent.md)