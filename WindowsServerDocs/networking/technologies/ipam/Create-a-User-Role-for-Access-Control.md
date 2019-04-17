---
title: アクセス制御のユーザー ロールを作成します。
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
ms.assetid: ae6a42db-a104-401b-a8e6-b85c47d30b46
ms.author: pashort
author: shortpatti
ms.openlocfilehash: fa0ed71d399ad638a648946952fe170d93f69ceb
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="create-a-user-role-for-access-control"></a>アクセス制御のユーザー ロールを作成します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用して、IPAM クライアント コンソールで新しいアクセス制御のユーザー ロールを作成することができます。  
  
メンバーシップ**管理者**、相当するものでは、この手順を実行するために必要な最低限またはします。  
  
> [!NOTE]  
> ロールを作成した後は、特定のユーザーまたは Active Directory グループに、役割を割り当てるアクセス ポリシーを作成できます。 詳細については、次を参照してください。[アクセス ポリシーを作成する](../../technologies/ipam/Create-an-Access-Policy.md)します。  
  
### <a name="to-create-a-role"></a>ロールを作成するには  
  
1.  サーバー マネージャーで、クリックして**IPAM**します。 IPAM クライアント コンソールに表示されます。  
  
2.  ナビゲーション ウィンドウで、をクリックして**アクセス制御**、下部のナビゲーション ウィンドウでをクリックして**役割**します。  
  
    ![アクセス制御役割](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_01.jpg)  
  
3.  右クリック**役割**、] をクリックし、**ユーザー ロールの追加**します。  
  
    ![ユーザー ロールを追加します。](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_02.jpg)  
  
4.  **追加または編集ロール**] ダイアログ ボックスが開きます。 **名**、オフの役割の機能は、ロールの名前を入力します。 たとえば、により、DNS SRV リソース レコードを管理する管理者ロールを作成する場合は、という名前、役割**IPAMSrv**します。 必要な場合、下方向にスクロール**Operations**ロールを定義する操作のタイプを検索します。 この例では、下にスクロールして**DNS リソース レコードの管理操作**します。  
  
    ![DNS リソース レコードの管理操作](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_03.jpg)  
  
5.  展開**DNS リソース レコードの管理操作**、見つけて**SRV レコード operations**します。  
  
    ![SRV レコードの操作](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_04.jpg)  
  
6.  展開し、選択**SRV レコード operations**、] をクリックし、**OK**します。  
  
    ![SRV レコードの操作を選択します。](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_05.jpg)  
  
7.  IPAM クライアント コンソールで、作成した役割] をクリックします。 **詳細ビュー、**ロールの許可された操作が表示されます。  
  
    ![新しいロールの詳細](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_06.jpg)  
  
## <a name="see-also"></a>参照してください。  
[役割に基づいたアクセス制御](Role-based-Access-Control.md)  
[IPAM を管理します。](Manage-IPAM.md)  
  


