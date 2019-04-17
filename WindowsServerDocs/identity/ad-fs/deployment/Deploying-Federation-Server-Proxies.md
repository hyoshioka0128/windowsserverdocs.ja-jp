---
ms.assetid: 1b21b0a9-1fe6-4fd1-8a25-92e578d774ed
title: "フェデレーション サーバー プロキシを展開します。"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: b914141a0445febd3961b688aadc2f444b2eee7b
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="deploying-federation-server-proxies"></a>フェデレーション サーバー プロキシを展開します。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Active Directory フェデレーション サービス \(AD FS\) でフェデレーション サーバー プロキシを展開するには、各タスクを実行[チェックリスト: 設定をフェデレーション サーバー プロキシの](Checklist--Setting-Up-a-Federation-Server-Proxy.md)します。  
  
> [!NOTE]  
> フェデレーション サーバー プロキシの計画のガイダンスへの参照を最初に読むことをお勧めこのチェックリストを使用すると、[Windows Server 2012 で AD FS 設計ガイド](https://technet.microsoft.com/library/dd807036.aspx)、サーバーを構成するための手順を開始する前にします。 フェデレーションの設計と展開プロセスの詳細を把握サーバー プロキシは、次のチェックリストに、します。  
  
## <a name="about-federation-server-proxies"></a>フェデレーション サーバー プロキシの  
フェデレーション サーバー プロキシは、プロキシの役割で動作する手動で構成されている Windows Server® 2012 と AD FS ソフトウェアを実行しているコンピューターです。 インターネット クライアントと企業ネットワーク上のファイアウォールの背後にあるフェデレーション サーバーの間の仲介サービスを提供するのに、組織内のフェデレーション サーバー プロキシを使用することができます。  
  
> [!NOTE]  
> 同じコンピューターには、フェデレーション サーバーとフェデレーション サーバー プロキシの役割をインストールことはできません、フェデレーション サーバーは、フェデレーション サーバー プロキシの機能を実行できます。 詳細については、次を参照してください。[When to Create a Federation Server](https://technet.microsoft.com/library/dd807101.aspx)します。  
  
Windows Server® 2012 コンピューターに AD FS ソフトウェアをインストールして、プロキシの役割で提供するように構成するの機能により、そのコンピューターは、フェデレーション サーバー プロキシします。  
  

