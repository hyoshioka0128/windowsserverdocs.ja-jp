---
title: サーバーへのユーザーアクセスを制限する
description: ユーザーおよびグループの MultiPoint サービスへのアクセスを許可または拒否する方法について説明します。
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4cabd4f1-a764-4be6-bc6e-0a5f5566390c
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 62f2a3f9b94ac3f0474636c34e8ec1f81c568cad
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71389057"
---
# <a name="limit-users-access-to-the-multipoint-server"></a>Multipoint サーバーへのユーザーのアクセスを制限する
MultiPoint server を Active Directory ドメインに参加させるか、ローカルユーザーアカウントを使用するかにかかわらず、既定ではすべてのユーザーが MultiPoint server にアクセスできます。 ユーザーが MultiPoint Services 環境でステーションにログオンできるようにするには、サーバーへのアクセスを制限する必要があります。  
  
Remote Desktop Users グループのすべてのユーザーが MultiPoint server にログオンできます。 既定では、ユーザーグループ Everyone は Remote Desktop Users グループのメンバであるため、すべてのローカルユーザーとドメインユーザーが MultiPoint サーバーにログオンできます。 MultiPoint Server へのアクセスを制限するには、Remote Desktop Users グループから Everyone ユーザーグループを削除してから、特定のユーザーまたはグループを Remote Desktop Users グループに追加します。  
  
## <a name="add-or-remove-users-or-groups-to-the-remote-desktop-users-group"></a>リモートデスクトップユーザーグループにユーザーまたはグループを追加または削除する  
  
1.  **[スタート]** 画面で、 **[コンピューターの管理]** を開きます。  
  
2.  コンソールツリーの **[ローカルユーザーとグループ]** で、 **[グループ]** をクリックします。  
  
3.  **[リモートデスクトップユーザー]** をダブルクリックし、指示に従ってユーザーを追加または削除します。  
  
    -   サーバーへの一般的なアクセスを制限するには、Everyone グループを削除します。  
  
    -   MultiPoint server ユーザーにステーションへのアクセスを許可するには、各ローカルアカウント、または各ドメインユーザーまたはグループアカウントを Remote Desktop Users グループに追加します。  