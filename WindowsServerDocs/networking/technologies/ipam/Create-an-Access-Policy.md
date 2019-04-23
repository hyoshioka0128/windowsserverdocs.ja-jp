---
title: アクセス ポリシーを作成する
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
ms.openlocfilehash: c8a97cd145a695bc8755f9111291e5c8bba2e572
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881903"
---
# <a name="create-an-access-policy"></a>アクセス ポリシーを作成する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックの「を使用して、IPAM クライアント コンソールで、アクセス ポリシーを作成することができます。  
  
メンバーシップ **管理者**, 、同等の権限をこの手順を実行するために必要な最低限のですか。  
  
> [!NOTE]  
> Active Directory では、特定のユーザーまたはユーザー グループのアクセス ポリシーを作成できます。 アクセス ポリシーを作成するときに、組み込みの IPAM の役割または作成したカスタム ロールのいずれかを選択する必要があります。 カスタム ロールの詳細については、次を参照してください。[アクセス制御のユーザー ロールの作成](../../technologies/ipam/Create-a-User-Role-for-Access-Control.md)です。  
  
### <a name="to-create-an-access-policy"></a>アクセス ポリシーを作成するには  
  
1.  サーバー マネージャーで、クリックして  **IPAM**します。 IPAM クライアント コンソールに表示されます。  
  
2.  ナビゲーション ウィンドウで、**アクセス制御**します。 下のナビゲーション ウィンドウで右クリック**アクセス ポリシー**、 をクリックし、**アクセス ポリシーの追加**します。  
  
    ![アクセス ポリシーを追加します。](../../media/Create-an-Access-Policy/ipam_CreateAP_01.jpg)  
  
3.  **アクセス ポリシーの追加** ダイアログ ボックスが表示されます。 **ユーザー設定**、 をクリックして**追加**します。  
  
    ![アクセス ポリシーを追加します。](../../media/Create-an-Access-Policy/ipam_CreateAP_02.jpg)  
  
4.  **[ユーザーまたはグループ**] ダイアログ ボックスが表示されます。 クリックして**場所**します。  
  
    ![ユーザーまたはグループの場所](../../media/Create-an-Access-Policy/ipam_CreateAP_03.jpg)  
  
5.  **場所** ダイアログ ボックスが表示されます。 ユーザー アカウントが含まれている場所を参照の場所を選択およびクリックして**OK**します。 **場所** ダイアログ ボックスを閉じます。  
  
    ![場所を選択します](../../media/Create-an-Access-Policy/ipam_CreateAP_04.jpg)  
  
6.  **[ユーザーまたはグループ**] ダイアログ ボックスで**を選択するオブジェクト名を入力**、アクセス ポリシーを作成するユーザー アカウント名を入力します。 **[OK]** をクリックします。  
  
7.  **アクセス ポリシーの追加**の**ユーザー設定**、**ユーザー エイリアス**ポリシーを適用するユーザー アカウントが含まれています。 **アクセス設定**、 をクリックして**新規**します。  
  
    ![新しいアクセス設定](../../media/Create-an-Access-Policy/ipam_CreateAP_05.jpg)  
  
8.  **アクセス ポリシーの追加**、**アクセス設定**変更**新しい設定**します。  
  
    ![ダイアログ ボックスの名前を新しい設定を変更します。](../../media/Create-an-Access-Policy/ipam_CreateAP_06.jpg)  
  
9. クリックして**役割を選択し**ロールの一覧を展開します。 組み込みのロールのいずれかを選択するか、新しいロールを作成した場合に作成したロールのいずれかを選択します。 します。 たとえば、ユーザーに適用する IPAMSrv ロールを作成した場合 をクリックして**IPAMSrv**します。  
  
    ![ロールを選択します。](../../media/Create-an-Access-Policy/ipam_CreateAP_07.jpg)  
  
10. クリックして**設定の追加**します。  
  
    ![新しい設定を追加します。](../../media/Create-an-Access-Policy/ipam_CreateAP_08.jpg)  
  
11. ロールは、アクセス ポリシーに追加されます。 追加のアクセス ポリシーを作成する をクリックして**適用**ポリシーを作成するごとに次の手順を繰り返します。 追加のポリシーを作成しない場合はクリックして**OK**します。  
  
    ![[適用] または [ok]](../../media/Create-an-Access-Policy/ipam_CreateAP_09.jpg)  
  
12. IPAM クライアント コンソールの表示ウィンドウで、新しいアクセス ポリシーが作成されたことを確認します。  
  
    ![新しいアクセス ポリシーを表示します。](../../media/Create-an-Access-Policy/ipam_CreateAP_09a.jpg)  
  
## <a name="see-also"></a>関連項目  
[ロール ベース Access Control](Role-based-Access-Control.md)  
[IPAM を管理します。](Manage-IPAM.md)  
  


