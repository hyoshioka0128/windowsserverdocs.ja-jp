---
title: 役割に基づいたアクセス制御
description: このトピックでは、Windows Server 2016 での IP アドレス管理 (IPAM) の管理ガイドの一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ecdfc589-fa14-4bb3-ab7e-456ebc719385
ms.author: pashort
author: shortpatti
ms.openlocfilehash: eec6d2a89b24d4847cb993bab31d86881f2cae0f
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="role-based-access-control"></a>役割に基づいたアクセス制御

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、IPAM で役割に基づいたアクセス制御の使用に関する情報を示します。  
  
> [!NOTE]  
> このトピックに加えは次の IPAM アクセスの制御ドキュメントはこのセクションで使用します。  
>   
> -   [役割ベースの管理アクセス制御 with Server Manager](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Server-Manager.md)  
> -   [役割ベースの管理アクセスを Windows PowerShell での制御](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Windows-PowerShell.md)  
  
役割に基づいたアクセス制御では、DNS サーバー、DNS ゾーン、DNS リソース レコードのレベルなど、さまざまなレベルでのアクセス権限を指定することができます。  
役割に基づいたアクセス制御を使用すると、作成、編集、およびさまざまな種類の DNS リソース レコードを削除する操作をより細かく制御を持つユーザーを指定できます。  
  
ユーザーは、次のアクセス許可を制限できるように、アクセス制御を構成することができます。  
  
-   ユーザーが特定の DNS リソース レコードのみを編集できます。  
  
-   ユーザーが PTR や MX など、特定の種類の DNS リソース レコードを編集できます。  
  
-   ユーザーが特定のゾーンの DNS リソース レコードを編集できます。  
  
## <a name="see-also"></a>参照してください。  
[役割ベースの管理アクセス制御 with Server Manager](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Server-Manager.md)  
[役割ベースの管理アクセスを Windows PowerShell での制御](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Windows-PowerShell.md)  
[IPAM を管理します。](Manage-IPAM.md)  
  


