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
ms.openlocfilehash: 3c18e0a6a2e633c0fad0ce8585296afba8ce444c
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86966934"
---
# <a name="migrate-the-ad-fs-web-agent"></a>AD FS web エージェントを移行する

Windows Server 2008 R2 または Windows Server 2008 と共にインストールされている AD FS 1.1 Windows トークンベースのエージェントまたは AD FS 1.1 の要求に対応するエージェントを windows server 2012 に移行するには、エージェントを Windows Server 2012 にホストしているコンピューターのオペレーティングシステムのインプレースアップグレードを実行します。 詳細については、「[Windows Server 2012 のインストール](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj134246(v=ws.11))」を参照してください。 それ以上の構成は必要ありません。  
  
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
  
  
## <a name="next-steps"></a>次の手順
 [AD FS 2.0 フェデレーションサーバーの移行の準備](prepare-to-migrate-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーションサーバープロキシの移行の準備](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [AD FS 2.0 フェデレーションサーバーの移行](migrate-the-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーションサーバープロキシの移行](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [AD FS 1.1 Web エージェントの移行](migrate-the-ad-fs-web-agent.md)
