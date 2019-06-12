---
title: AD FS web エージェントを移行します。
description: Windows Server 2012 に AD FS web エージェントの情報を提供します。
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 7cde62cb23c69a425522e40ed65ee2d40ef28268
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445600"
---
# <a name="migrate-the-ad-fs-web-agent"></a>AD FS web エージェントを移行します。

移行する AD FS 1.1 Windows トークン ベース エージェントまたは AD FS 1.1 クレーム認識エージェントは Windows Server 2008 R2 または Windows Server 2012、Windows Server 2008 と共にインストールされるエージェント ホストしているコンピューターのオペレーティング システムのインプレース アップグレードを実行します。Windows server 2012。 詳細については、「[Windows Server 2012 のインストール](https://technet.microsoft.com/library/jj134246.aspx)」を参照してください。 これ以上の構成は必要ありません。  
  
> [!IMPORTANT]
>  移行された AD FS 1.1 Windows トークン ベース エージェントは、Windows Server 2008 R2 または Windows Server 2008 にインストールされている AD FS 1.1 フェデレーション サービスでのみ機能します。 詳細については、「 [Interoperating with AD FS 1.x](Interoperating-with-AD-FS-1.x.md)」を参照してください。  
> 
>  移行された AD FS 1.1 クレーム認識 Web エージェントは、次のサービスで機能します。  
> 
> - Windows Server 2008 R2 または Windows Server 2008 にインストールされている AD FS 1.1 フェデレーション サービス  
>   -   Windows Server 2008 R2 または Windows Server 2008 にインストールされている AD FS 2.0 フェデレーション サービス  
>   -   Windows Server 2012 で AD FS フェデレーション サービスがインストールされています。  
> 
>   詳細については、「 [Interoperating with AD FS 1.x](Interoperating-with-AD-FS-1.x.md)」を参照してください。  
  
  
## <a name="next-steps"></a>次の手順
 [AD FS 2.0 フェデレーション サーバーの移行を準備します。](prepare-to-migrate-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーション サーバー プロキシの移行を準備します。](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [AD FS 2.0 フェデレーション サーバーを移行します。](migrate-the-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーション サーバー プロキシを移行します。](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [AD FS 1.1 Web エージェントの移行](migrate-the-ad-fs-web-agent.md)