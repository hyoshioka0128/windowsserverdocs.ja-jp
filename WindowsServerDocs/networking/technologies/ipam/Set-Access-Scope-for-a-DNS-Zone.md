---
title: DNS ゾーンのアクセス スコープを設定する
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
ms.assetid: 6a211dde-80eb-4888-b5bb-4e28fe8dc7df
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 73d96a9be7c13afbe4c96d46fffefc0096046c8c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813983"
---
# <a name="set-access-scope-for-a-dns-zone"></a>DNS ゾーンのアクセス スコープを設定する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックでは、IPAM クライアント コンソールを使用して DNS ゾーンのアクセス スコープの設定を使用できます。  
  
メンバーシップ **管理者**, 、同等の権限をこの手順を実行するために必要な最低限のですか。  
  
### <a name="to-set-the-access-scope-for-a-dns-zone"></a>DNS ゾーンのアクセス スコープを設定するには  
  
1.  サーバー マネージャーで、クリックして  **IPAM**します。 IPAM クライアント コンソールに表示されます。  
  
2.  ナビゲーション ウィンドウで、 **DNS ゾーン**します。 表示ウィンドウをクリックして、変更のアクセス スコープ、DNS ゾーンを右クリックして**アクセス スコープの設定**します。  
  
    ![アクセス スコープの設定](../../media/Set-Access-Scope-for-a-DNS-Zone/ipam_SetAccessScopeOfZone_02.jpg)  
  
3.  **アクセス スコープの設定** ダイアログ ボックスが表示されます。 展開に、必要な場合は、選択を解除する をクリックして**親から継承されたアクセス スコープ**します。 **アクセス スコープの選択**、項目を選択し、をクリックし、 **OK**します。  
  
    ![アクセス スコープを選択します。](../../media/Set-Access-Scope-for-a-DNS-Zone/ipam_SetAccessScopeOfZone_03.jpg)  
  
4.  IPAM クライアント コンソールの表示ウィンドウで、ゾーンのアクセス スコープが変更されたことを確認します。  
  
    ![ゾーンのアクセス スコープが変更されたことを確認します。](../../media/Set-Access-Scope-for-a-DNS-Zone/ipam_SetAccessScopeOfZone_04.jpg)  
  
## <a name="see-also"></a>関連項目  
[ロール ベース Access Control](Role-based-Access-Control.md)  
[IPAM を管理します。](Manage-IPAM.md)  
  


