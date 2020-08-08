---
title: ロールベースのアクセス制御
description: このトピックは、Windows Server 2016 の IP アドレス管理 (IPAM) 管理ガイドに含まれています。
manager: brianlic
ms.topic: article
ms.assetid: ecdfc589-fa14-4bb3-ab7e-456ebc719385
ms.author: lizross
author: eross-msft
ms.openlocfilehash: f79dc7ab4283de5ab1ec63861d5f543658947964
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87944674"
---
# <a name="role-based-access-control"></a>ロールベースのアクセス制御

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、IPAM でのロールベースのアクセス制御の使用について説明します。

> [!NOTE]
> このトピックに加えて、次の IPAM アクセス制御ドキュメントを参照してください。
>
> -   [サーバー マネージャーで役割ベースのアクセス制御を管理する](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Server-Manager.md)
> -   [Windows PowerShell で役割ベースのアクセス制御を管理する](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Windows-PowerShell.md)

ロールベースのアクセス制御を使用すると、DNS サーバー、DNS ゾーン、DNS リソースレコードレベルなど、さまざまなレベルでアクセス権限を指定できます。
ロールベースのアクセス制御を使用すると、さまざまな種類の DNS リソースレコードを作成、編集、および削除する操作をきめ細かく制御できるユーザーを指定できます。

アクセス制御を構成して、ユーザーが次のアクセス許可に制限されるようにすることができます。

-   ユーザーは、特定の DNS リソースレコードのみを編集できます

-   ユーザーは、PTR や MX など、特定の種類の DNS リソースレコードを編集できます。

-   ユーザーは、特定のゾーンの DNS リソースレコードを編集できます。

## <a name="see-also"></a>参照
[サーバーマネージャーを使用してロールベースの Access Control を管理](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Server-Manager.md) 
 する[Windows PowerShell を使用して役割ベースの Access Control を管理](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Windows-PowerShell.md) 
 する[IPAM の管理](Manage-IPAM.md)



