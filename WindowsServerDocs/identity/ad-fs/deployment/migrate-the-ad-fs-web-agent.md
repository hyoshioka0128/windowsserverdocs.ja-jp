---
title: AD FS web エージェントを移行する
description: Windows Server 2012 に AD FS web エージェントに関する情報を提供します。
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: ddba9668b54e325dae6dfc0cf67d50d3ae5d90be
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408190"
---
# <a name="migrate-the-ad-fs-web-agent"></a>AD FS web エージェントを移行する

Windows Server 2008 R2 または Windows Server 2008 と共にインストールされている AD FS 1.1 Windows トークンベースエージェントまたは AD FS 1.1 要求対応エージェントを Windows Server 2012 に移行するには、いずれかのエージェントをホストするコンピューターのオペレーティングシステムのインプレースアップグレードを実行します。Windows Server 2012 に。 詳細については、「[Windows Server 2012 のインストール](https://technet.microsoft.com/library/jj134246.aspx)」を参照してください。 これ以上の構成は必要ありません。  
  
> [!IMPORTANT]
>  移行された AD FS 1.1 Windows トークン ベース エージェントは、Windows Server 2008 R2 または Windows Server 2008 にインストールされている AD FS 1.1 フェデレーション サービスでのみ機能します。 詳細については、「 [Interoperating with AD FS 1.x](Interoperating-with-AD-FS-1.x.md)」を参照してください。  
> 
>  移行された AD FS 1.1 クレーム認識 Web エージェントは、次のサービスで機能します。  
> 
> - Windows Server 2008 R2 または Windows Server 2008 にインストールされている AD FS 1.1 フェデレーション サービス  
>   -   Windows Server 2008 R2 または Windows Server 2008 にインストールされている AD FS 2.0 フェデレーション サービス  
>   -   Windows Server 2012 にインストールされている AD FS フェデレーションサービス  
> 
>   詳細については、「 [Interoperating with AD FS 1.x](Interoperating-with-AD-FS-1.x.md)」を参照してください。  
  
  
## <a name="next-steps"></a>次のステップ
 [AD FS 2.0 フェデレーションサーバー  の移行の準備](prepare-to-migrate-ad-fs-fed-server.md)  
 [AD FS 2.0 フェデレーションサーバープロキシの移行の準備](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [AD FS 2.0 フェデレーションサーバー  を移行します](migrate-the-ad-fs-fed-server.md)。  
 [AD FS 2.0 フェデレーションサーバープロキシ  を移行します](migrate-the-ad-fs-2-fed-server-proxy.md)。  
 [AD FS 1.1 Web エージェントの移行](migrate-the-ad-fs-web-agent.md)