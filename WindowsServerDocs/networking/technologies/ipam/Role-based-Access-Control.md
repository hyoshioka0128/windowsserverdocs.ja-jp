---
title: 役割ベースのアクセス制御
description: このトピックは、Windows Server 2016 の IP アドレス管理 (IPAM) 管理ガイドに含まれています。
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ecdfc589-fa14-4bb3-ab7e-456ebc719385
ms.author: pashort
author: shortpatti
ms.openlocfilehash: cf6b8418482b606c86bac77b2790e3365e80bf5d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71355159"
---
# <a name="role-based-access-control"></a>役割ベースのアクセス制御

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、IPAM でのロールベースのアクセス制御の使用について説明します。  
  
> [!NOTE]  
> このトピックに加えて、次の IPAM アクセス制御ドキュメントを参照してください。  
>   
> -   [サーバーマネージャーを使用してロールベースの Access Control を管理する](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Server-Manager.md)  
> -   [Windows PowerShell を使用して役割ベースの Access Control を管理する](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Windows-PowerShell.md)  
  
ロールベースのアクセス制御を使用すると、DNS サーバー、DNS ゾーン、DNS リソースレコードレベルなど、さまざまなレベルでアクセス権限を指定できます。  
ロールベースのアクセス制御を使用すると、さまざまな種類の DNS リソースレコードを作成、編集、および削除する操作をきめ細かく制御できるユーザーを指定できます。  
  
アクセス制御を構成して、ユーザーが次のアクセス許可に制限されるようにすることができます。  
  
-   ユーザーは、特定の DNS リソースレコードのみを編集できます  
  
-   ユーザーは、PTR や MX など、特定の種類の DNS リソースレコードを編集できます。  
  
-   ユーザーは、特定のゾーンの DNS リソースレコードを編集できます。  
  
## <a name="see-also"></a>関連項目  
[サーバーマネージャーを使用してロールベースの Access Control を管理する](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Server-Manager.md)  
[Windows PowerShell を使用して役割ベースの Access Control を管理する](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Windows-PowerShell.md)  
[IPAM の管理](Manage-IPAM.md)  
  


