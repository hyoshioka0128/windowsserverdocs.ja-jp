---
title: "AD FS Web エージェントを移行します。"
description: "AD FS Web エージェントの Windows Server 2012 の情報を提供します。"
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 945a5f4cf0e6c491479b095671ff5e77416c6fa3
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="migrate-the-ad-fs-web-agent"></a>AD FS Web エージェントを移行します。

移行 AD FS 1.1 Windows トークン ベース エージェントまたは AD FS 1.1 要求に対応するエージェントが Windows Server 2008 R2 または Windows Server 2012、Windows Server 2008 にインストールされているが Windows Server 2012 へのいずれかのエージェントをホストするコンピューターのオペレーティング システムのインプレース アップグレードを実行します。 詳細については、次を参照してください。[Windows Server 2012 のインストール](https://technet.microsoft.com/library/jj134246.aspx)します。 これ以上の構成は必要ありません。  
  
> [!IMPORTANT]
>  移行された AD FS 1.1 Windows トークン ベースのエージェントの関数が Windows Server 2008 R2 または Windows Server 2008 にインストールされている AD FS 1.1 フェデレーション サービスでのみです。 詳細については、次を参照してください。[Interoperating with AD FS 1.x](Interoperating-with-AD-FS-1.x.md)します。  
>   
>  移行された AD FS 1.1 クレーム認識 Web、次のようにエージェントの機能。  
>   
>  -   Windows Server 2008 R2 または Windows Server 2008 にインストールされている AD FS 1.1 フェデレーション サービス  
> -   Windows Server 2008 R2 または Windows Server 2008 にインストールされている AD FS 2.0 フェデレーション サービス  
> -   Windows Server 2012 にインストールされている AD FS フェデレーション サービス  
>   
>  詳細については、次を参照してください。[Interoperating with AD FS 1.x](Interoperating-with-AD-FS-1.x.md)します。  
  
  
## <a name="next-steps"></a>次の手順
 [AD FS 2.0 フェデレーション サーバーの移行を準備します。](prepare-to-migrate-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーション サーバー プロキシの移行を準備します。](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [AD FS 2.0 フェデレーション サーバーを移行します。](migrate-the-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーション サーバー プロキシを移行します。](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [AD FS 1.1 Web エージェントを移行します。](migrate-the-ad-fs-web-agent.md)