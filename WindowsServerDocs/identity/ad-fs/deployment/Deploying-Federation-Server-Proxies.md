---
ms.assetid: 1b21b0a9-1fe6-4fd1-8a25-92e578d774ed
title: フェデレーション サーバー プロキシの展開
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: f348b7dbc9b786cfe401eb72b82592a51e1e6343
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855555"
---
# <a name="deploying-federation-server-proxies"></a>フェデレーション サーバー プロキシの展開

Active Directory フェデレーションサービス (AD FS) \(AD FS\)でフェデレーションサーバープロキシを展開するには、「[チェックリスト: フェデレーションサーバープロキシの](Checklist--Setting-Up-a-Federation-Server-Proxy.md)セットアップ」の各タスクを実行します。  
  
> [!NOTE]  
> このチェックリストを使用する場合は、まず、サーバーの構成手順を開始する前に、 [Windows server 2012 の AD FS 設計ガイド](https://technet.microsoft.com/library/dd807036.aspx)の「フェデレーションサーバープロキシの計画に関するガイダンス」を参照することをお勧めします。 このチェックリストに従うことで、フェデレーションサーバープロキシの設計と展開のプロセスについて理解を深めることができます。  
  
## <a name="about-federation-server-proxies"></a>フェデレーションサーバープロキシについて  
フェデレーションサーバープロキシは、Windows Server&reg; 2012 を実行するコンピューターであり、プロキシの役割で動作するように手動で構成されたソフトウェア AD FS ます。 組織内のフェデレーション サーバー プロキシを使用して、インターネット クライアントと、企業ネットワーク上のファイアウォールの背後にあるフェデレーション サーバーの間で、仲介サービスを提供できます。  
  
> [!NOTE]  
> フェデレーションサーバーとフェデレーションサーバープロキシの役割を同じコンピューターにインストールすることはできませんが、フェデレーションサーバーはフェデレーションサーバープロキシ機能を実行できます。 詳細については、「 [When to Create a Federation Server](https://technet.microsoft.com/library/dd807101.aspx)」を参照してください。  
  
AD FS ソフトウェアを Windows Server&reg; 2012 コンピューターにインストールし、プロキシの役割で動作するように構成すると、そのコンピューターはフェデレーションサーバープロキシになります。  
  

