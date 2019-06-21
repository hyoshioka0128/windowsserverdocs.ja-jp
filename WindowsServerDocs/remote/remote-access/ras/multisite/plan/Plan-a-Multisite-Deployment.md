---
title: マルチサイト展開を計画する
description: このトピックは、ガイドの一部複数リモート アクセス サーバーの展開で Windows Server 2016 の Multisite 展開します。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8387eabe-7363-4367-b5b1-03c67baa2933
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ba813fc5da53e9635e9ef1363f1a559a29419312
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282601"
---
# <a name="plan-a-multisite-deployment"></a>マルチサイト展開を計画する

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

 Windows Server 2016、Windows Server 2012 は、DirectAccess およびルーティングとリモート アクセス サービス (RRAS) VPN を 1 つのリモート アクセス役割に結合します。 この概要では、マルチサイト構成で Windows Server 2016 または Windows Server 2012 のリモート アクセスを展開するために必要な計画手順を紹介します。  
  
1.  [高度な設定で単一の DirectAccess サーバーをデプロイ](https://technet.microsoft.com/library/hh831436(v=ws.11).aspx)します。 この手順には、単一サーバーの展開に必要なインフラストラクチャの計画が含まれます。 これは、ネットワークとサーバーの設定、証明書の要件、DNS 設定、ネットワーク ロケーション サーバーの展開、DirectAccess 管理サーバー、Active Directory 設定、およびグループ ポリシー オブジェクト (Gpo) の計画が含まれます。  
  
2.  [手順 2 は、マルチサイトのインフラストラクチャを計画](Step-2-Plan-the-Multisite-Infrastructure.md)します。 この手順には、Active Directory と GPO の計画、および DNS の構成が含まれています。  
  
3.  [手順 3、マルチサイト展開を計画する](Step-3-Plan-the-Multisite-Deployment.md)します。 この手順には、証明書の設定、ネットワーク ロケーション サーバーの構成、クライアントのエントリ ポイントの設定、IPv6 プレフィックスの設定、および必要に応じてグローバル負荷分散の設定の計画が含まれます。  
  
> [!NOTE]  
> 展開を高度なリモート アクセスの計画の決定を記録します。 このレコードは、展開の手順の完了にかかわる全員がジョブエイドとして使用できます。  
  
これらの計画手順を完了したら後、は、次を参照してください。[マルチサイト展開を構成する](../configure/Configure-a-Multisite-Deployment.md)します。  
  


