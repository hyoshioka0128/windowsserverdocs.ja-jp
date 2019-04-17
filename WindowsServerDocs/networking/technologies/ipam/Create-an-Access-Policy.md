---
title: アクセス ポリシーを作成します。
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
ms.assetid: 854bd064-2f86-4678-a940-a04b3e48ae10
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ac8229952c7e038f9af8fc4f9287b1821db887ac
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="create-an-access-policy"></a>アクセス ポリシーを作成します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用すると、IPAM クライアント コンソールでのアクセス ポリシーを作成します。  
  
メンバーシップ**管理者**、相当するものでは、この手順を実行するために必要な最低限またはします。  
  
> [!NOTE]  
> Active Directory 内の特定のユーザーまたはユーザー グループのアクセス ポリシーを作成できます。 アクセス ポリシーを作成する場合は、組み込みの IPAM ロールまたは作成したカスタムの役割を選択する必要があります。 カスタムの役割の詳細については、次を参照してください。[アクセス制御のユーザー ロールを作成](../../technologies/ipam/Create-a-User-Role-for-Access-Control.md)します。  
  
### <a name="to-create-an-access-policy"></a>アクセス ポリシーを作成するには  
  
1.  サーバー マネージャーで、クリックして**IPAM**します。 IPAM クライアント コンソールに表示されます。  
  
2.  ナビゲーション ウィンドウで、をクリックして**アクセス制御**します。 下部のナビゲーション ウィンドウで右クリック**アクセス ポリシー**、] をクリックし、**アクセス ポリシーの追加**します。  
  
    ![アクセス ポリシーを追加します。](../../media/Create-an-Access-Policy/ipam_CreateAP_01.jpg)  
  
3.  **アクセス ポリシーの追加**] ダイアログ ボックスが開きます。 **ユーザー設定**、] をクリックして**追加**します。  
  
    ![アクセス ポリシーを追加します。](../../media/Create-an-Access-Policy/ipam_CreateAP_02.jpg)  
  
4.  **[ユーザーまたはグループ**] ダイアログ ボックスが開きます。 をクリックして**場所**します。  
  
    ![ユーザーまたはグループの場所](../../media/Create-an-Access-Policy/ipam_CreateAP_03.jpg)  
  
5.  **場所**] ダイアログ ボックスが開きます。 ユーザー アカウントが含まれている場所を参照しの場所を選択し、[クリックして**OK**します。 **場所**] ダイアログ ボックスを閉じます。  
  
    ![場所を選択します。](../../media/Create-an-Access-Policy/ipam_CreateAP_04.jpg)  
  
6.  **[ユーザーまたはグループ**] ダイアログ ボックスで、**を選択するオブジェクト名を入力**、アクセス ポリシーを作成するユーザー アカウント名を入力します。 をクリックして**OK**します。  
  
7.  **アクセス ポリシーの追加**で、**ユーザー設定**、**ユーザー エイリアス**、ポリシーを適用するユーザー アカウントが含まれています。 **アクセス設定**、] をクリックして**新規**します。  
  
    ![新しいアクセス設定](../../media/Create-an-Access-Policy/ipam_CreateAP_05.jpg)  
  
8.  **アクセス ポリシーの追加**、**アクセス設定**変更**新しい設定**します。  
  
    ![ダイアログ ボックスの名前を新しい設定を変更します。](../../media/Create-an-Access-Policy/ipam_CreateAP_06.jpg)  
  
9. をクリックして**選択役割**役割の一覧を展開します。 組み込みのロールのいずれかを選択または、新しいロールを作成した場合に作成したロールのいずれかを選択します。 たとえば、作成した場合、ユーザーに適用する IPAMSrv ロール、] をクリックして**IPAMSrv**します。  
  
    ![役割を選択します。](../../media/Create-an-Access-Policy/ipam_CreateAP_07.jpg)  
  
10. をクリックして**設定を追加**します。  
  
    ![新しい設定を追加します。](../../media/Create-an-Access-Policy/ipam_CreateAP_08.jpg)  
  
11. ロールは、アクセス ポリシーに追加されます。 追加のアクセス ポリシーを作成する] をクリックして**適用**、および作成するポリシーごとに次の手順を繰り返します。 追加ポリシーを作成しない場合はクリックして**OK**します。  
  
    ![[適用] または [OK]](../../media/Create-an-Access-Policy/ipam_CreateAP_09.jpg)  
  
12. IPAM クライアント コンソールの表示ウィンドウで、新しいアクセス ポリシーが作成されたことを確認します。  
  
    ![新しいアクセス ポリシーを表示します。](../../media/Create-an-Access-Policy/ipam_CreateAP_09a.jpg)  
  
## <a name="see-also"></a>参照してください。  
[役割に基づいたアクセス制御](Role-based-Access-Control.md)  
[IPAM を管理します。](Manage-IPAM.md)  
  


