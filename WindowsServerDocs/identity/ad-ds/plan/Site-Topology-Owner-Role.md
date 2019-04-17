---
ms.assetid: af76ddbe-83a2-4a62-9989-873e3bb1c772
title: "サイトのトポロジ所有者の役割"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 7c98d313cac28ab07380791a384a87bffacfbda2
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="site-topology-owner-role"></a>サイトのトポロジ所有者の役割

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

サイト トポロジを管理する管理者は、サイトのトポロジ所有者と呼ばれます。 サイトのトポロジ所有者は、サイト間のネットワークの条件を理解し、Active Directory ドメイン サービス (AD DS) サイト トポロジの変更を実装する設定を変更する権限を持ちます。 サイト トポロジの変更は、レプリケーション トポロジの変更に影響します。 サイトのトポロジ所有者の役割は次のとおりです。  
  
-   ネットワーク接続が変更された場合は、サイトのトポロジの変更を制御します。  
  
-   取得し、ネットワーク接続およびネットワーク グループからルーターに関する情報を管理します。 サイトのトポロジ所有者は、サブネット アドレス、サブネット マスク、および各が所属する場所の一覧を管理する必要があります。 サイトのトポロジ所有者は、サイトのトポロジを効果的にサイト リンクのコストを設定するのに影響を与えるネットワークの速度と容量に関する問題を理解も必要があります。  
  
-   別のサイトに別のサブネットにドメイン コントローラーの IP アドレスが変更された場合、またはサブネット自体が別のサイトに割り当てられている場合は、サイト間でのドメイン コントローラーを表す Active Directory サーバー オブジェクトを移動します。 どちらの場合、サイトのトポロジ所有者は、新しいサイトにドメイン コントローラーの Active Directory サーバー オブジェクトを手動で移動する必要があります。  
  


