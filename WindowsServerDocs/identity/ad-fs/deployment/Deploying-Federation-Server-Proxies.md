---
ms.assetid: 1b21b0a9-1fe6-4fd1-8a25-92e578d774ed
title: フェデレーション サーバー プロキシの展開
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: c6af319283de72963691ae3e91c3db5992bdec72
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408401"
---
# <a name="deploying-federation-server-proxies"></a>フェデレーション サーバー プロキシの展開

Active Directory フェデレーションサービス (AD FS) \(AD FS\)でフェデレーションサーバープロキシを展開するには、「[チェックリスト: フェデレーションサーバープロキシの](Checklist--Setting-Up-a-Federation-Server-Proxy.md)セットアップ」の各タスクを実行します。  
  
> [!NOTE]  
> このチェックリストを使用する場合は、まず、サーバーの構成手順を開始する前に、 [Windows server 2012 の AD FS 設計ガイド](https://technet.microsoft.com/library/dd807036.aspx)の「フェデレーションサーバープロキシの計画に関するガイダンス」を参照することをお勧めします。 このチェックリストに従うことで、フェデレーションサーバープロキシの設計と展開のプロセスについて理解を深めることができます。  
  
## <a name="about-federation-server-proxies"></a>フェデレーションサーバープロキシについて  
フェデレーションサーバープロキシは、Windows Server®2012を実行するコンピューターであり、プロキシの役割で動作するように手動で構成されたソフトウェア AD FS ます。 組織内のフェデレーション サーバー プロキシを使用して、インターネット クライアントと、企業ネットワーク上のファイアウォールの背後にあるフェデレーション サーバーの間で、仲介サービスを提供できます。  
  
> [!NOTE]  
> フェデレーションサーバーとフェデレーションサーバープロキシの役割を同じコンピューターにインストールすることはできませんが、フェデレーションサーバーはフェデレーションサーバープロキシ機能を実行できます。 詳細については、「 [When to Create a Federation Server](https://technet.microsoft.com/library/dd807101.aspx)」を参照してください。  
  
AD FS ソフトウェアを Windows Server®2012コンピューターにインストールし、プロキシの役割で動作するように構成すると、そのコンピューターはフェデレーションサーバープロキシになります。  
  

