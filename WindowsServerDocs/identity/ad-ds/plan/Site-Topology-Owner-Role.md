---
ms.assetid: af76ddbe-83a2-4a62-9989-873e3bb1c772
title: サイト トポロジの所有者の役割
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 69443c2fc1af855c7df002e0ac91d43986eff6da
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832113"
---
# <a name="site-topology-owner-role"></a>サイト トポロジの所有者の役割

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

サイトのトポロジを管理する管理者は、サイトのトポロジ所有者と呼ばれます。 サイトのトポロジ所有者は、サイト間のネットワークの条件を理解し、Active Directory Domain Services (AD DS) サイトのトポロジへの変更を実装する設定を変更する権限を持ちます。 サイトのトポロジへの変更では、レプリケーション トポロジの変更に影響します。 サイトのトポロジ所有者の責任は次のとおりです。  
  
-   ネットワーク接続が変更された場合は、サイトのトポロジへの変更を制御します。  
  
-   取得し、ネットワークのグループからのルーターとネットワーク接続に関する情報を管理します。 サイトのトポロジ所有者は、サブネット アドレス、サブネット マスク、およびそれぞれが属する場所の一覧を保持する必要があります。 サイトのトポロジ所有者は、サイト リンクのコストを効果的に設定するサイトのトポロジに影響を与える問題がネットワークの速度と容量についても理解する必要があります。  
  
-   別のサイトに別のサブネットにドメイン コント ローラーの IP アドレスが変更された場合、またはサブネット自体が別のサイトに割り当てられている場合は、サイト間のドメイン コント ローラーを表す Active Directory サーバー オブジェクトを移動します。 どちらの場合、サイトのトポロジ所有者は、新しいサイトにドメイン コント ローラーの Active Directory サーバー オブジェクトを手動で移動する必要があります。  
  


