---
title: 役割ベースのアクセス制御
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
ms.openlocfilehash: 86a57e5a74073ecf749c4ec8209999e8ace31508
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838903"
---
# <a name="role-based-access-control"></a>役割ベースのアクセス制御

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックでは、IPAM でのロールベースのアクセス制御の使用に関する情報を提供します。  
  
> [!NOTE]  
> このトピックに加え次の IPAM アクセスの制御ドキュメントは、このセクションでは使用可能です。  
>   
> -   [ロール ベースの管理アクセス制御サーバー マネージャーを使用](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Server-Manager.md)  
> -   [ロール ベースの管理 Windows PowerShell を使用したコントロールへのアクセス](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Windows-PowerShell.md)  
  
ロール ベース access control を使用すると、DNS サーバー、DNS ゾーン、DNS リソース レコード レベルなど、さまざまなレベルでのアクセス権限を指定することができます。  
ロール ベース アクセス制御を使用すると、作成、編集、およびさまざまな種類の DNS リソース レコードを削除する操作の詳細な制御を持つユーザーを指定できます。  
  
ユーザーは、次のアクセス許可を制限できるように、アクセス制御を構成できます。  
  
-   ユーザーが特定の DNS リソース レコードのみを編集できます。  
  
-   ユーザーが PTR または MX などの特定の種類の DNS リソース レコードを編集できます。  
  
-   ユーザーが特定のゾーンの DNS リソース レコードを編集できます。  
  
## <a name="see-also"></a>関連項目  
[ロール ベースの管理アクセス制御サーバー マネージャーを使用](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Server-Manager.md)  
[ロール ベースの管理 Windows PowerShell を使用したコントロールへのアクセス](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Windows-PowerShell.md)  
[IPAM を管理します。](Manage-IPAM.md)  
  


