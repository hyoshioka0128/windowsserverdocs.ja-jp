---
ms.assetid: 1b21b0a9-1fe6-4fd1-8a25-92e578d774ed
title: フェデレーション サーバー プロキシの展開
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 02311522ee229eeaf0b27ce8d39090a9529b99ae
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192199"
---
# <a name="deploying-federation-server-proxies"></a>フェデレーション サーバー プロキシの展開

Active Directory フェデレーション サービスでフェデレーション サーバー プロキシをデプロイする\(AD FS\)、それぞれのタスクの完了[チェックリスト。フェデレーション サーバー プロキシを設定する](Checklist--Setting-Up-a-Federation-Server-Proxy.md)します。  
  
> [!NOTE]  
> フェデレーション サーバー プロキシの計画のガイダンスへの参照を最初に読むことをお勧めこのチェックリストを使用すると、 [Windows Server 2012 で AD FS 設計ガイド](https://technet.microsoft.com/library/dd807036.aspx)サーバーを構成する手順を開始する前にします。 次のチェックリストと、サーバー プロキシ、フェデレーションの設計と展開プロセスの理解を深めるが提供します。  
  
## <a name="about-federation-server-proxies"></a>フェデレーション サーバー プロキシについて  
フェデレーション サーバー プロキシは、プロキシの役割で動作する手動で構成されている Windows Server® 2012 および AD FS ソフトウェアを実行するコンピューターです。 組織内のフェデレーション サーバー プロキシを使用して、インターネット クライアントと、企業ネットワーク上のファイアウォールの背後にあるフェデレーション サーバーの間で、仲介サービスを提供できます。  
  
> [!NOTE]  
> フェデレーション サーバーとフェデレーション サーバー プロキシの役割は、同じコンピューターにインストールすることはできません、フェデレーション サーバーは、フェデレーション サーバー プロキシの機能を実行できます。 詳細については、「 [When to Create a Federation Server](https://technet.microsoft.com/library/dd807101.aspx)」を参照してください。  
  
Windows Server® 2012 コンピューターに AD FS ソフトウェアをインストールし、プロキシの役割サービスを提供するように構成の動作により、そのコンピューターは、フェデレーション サーバー プロキシ。  
  

