---
title: サーバーへのユーザー アクセスを制限します。
description: MultiPoint Services のユーザーやグループへのアクセスを拒否または許可する方法について説明します
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4cabd4f1-a764-4be6-bc6e-0a5f5566390c
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 1466e19152847a6c7d88f77162c50ec73a5a7d27
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830813"
---
# <a name="limit-users-access-to-the-multipoint-server"></a>Multipoint サーバーへのユーザー アクセスを制限します。
MultiPoint server を Active Directory ドメインに参加するか、ローカル ユーザー アカウントを使用するかどうかは、既定で MultiPoint サーバーへのアクセスがあるすべてのユーザー。 MultiPoint サービス環境内でステーションにログオンするユーザーを許可する前に、サーバーへのアクセスを制限する必要があります。  
  
Remote Desktop Users グループの他のユーザーは MultiPoint サーバーにログオンできます。 既定では、ユーザーはグループのすべてのユーザー、Remote Desktop Users グループのメンバーであるし、そのためすべてのローカル ユーザーとドメイン ユーザーにログオンできます MultiPoint Server。 MultiPoint サーバーへのアクセスを制限するには、ユーザーは、リモート デスクトップ ユーザー グループからグループ化し、Remote Desktop Users グループに特定のユーザーまたはグループを追加で、Everyone を削除します。  
  
## <a name="add-or-remove-users-or-groups-to-the-remote-desktop-users-group"></a>ユーザーまたはグループを Remote Desktop Users グループに追加または削除  
  
1.  **開始** 画面で、開いている**コンピュータの管理**します。  
  
2.  コンソール ツリーで [**ローカル ユーザーとグループ**、] をクリックして**グループ**します。  
  
3.  ダブルクリック**Remote Desktop Users**、しを追加または削除する指示に従います。  
  
    -   サーバーへの一般的なアクセスを制限するには、Everyone グループを削除します。  
  
    -   ステーションを MultiPoint サーバー ユーザーへのアクセスを付与するには、Remote Desktop Users グループに各ローカル アカウントまたは各ドメイン ユーザーまたはグループ アカウントを追加します。  