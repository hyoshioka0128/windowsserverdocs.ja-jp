---
title: マルチサイト展開を構成する
description: このトピックは、ガイドの一部複数リモート アクセス サーバーの展開で Windows Server 2016 の Multisite 展開します。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cb84920e-7cf5-4266-b071-d09e3d5e1f10
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 28fcb2506e59ff2afb501a2c8bc74da2d6f0cd15
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280986"
---
# <a name="configure-a-multisite-deployment"></a>マルチサイト展開を構成する

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

 Windows Server 2016 では、単一のリモート アクセス役割に DirectAccess とリモート アクセス サービス (RAS) VPN を結合します。 この概要では、単一 Windows Server 2016 または Windows Server 2012 のリモート アクセスのマルチサイト展開を展開するために必要な構成手順を紹介します。  
  
-   手順 1:[高度な設定で単一の DirectAccess サーバーをデプロイ](https://technet.microsoft.com/windows-server-docs/networking/remote-access/directaccess/single-server-advanced/deploy-a-single-directaccess-server-with-advanced-settings)します。 インストールし、単一のリモート アクセス サーバーを構成します。 マルチサイト展開では、マルチサイト展開を構成する前に、単一のサーバーをインストールする必要があります。  
  
-   [手順 2:マルチサイトのインフラストラクチャを構成する](Step-2-Configure-the-Multisite-Infrastructure.md)します。 マルチサイト展開の追加の Active Directory サイトとドメイン コント ローラーを構成する必要があります。 追加のセキュリティ グループとグループ ポリシー オブジェクト (Gpo) は自動的に構成された Gpo を使用していない場合にも必要です。  
  
-   [手順 3:マルチサイト展開を構成する](Step-3-Configure-the-Multisite-Deployment.md)-追加のリモート アクセス サーバーにリモート アクセスの役割をインストール、マルチサイト展開では、有効にして、展開用のエントリ ポイントとしてその他のサーバーを構成します。  
  
-   [手順 4:マルチサイト展開を確認します。](Step-4-Verify-the-Multisite-Deployment.md) 
  


