---
title: アクセス制御のユーザーの役割を作成する
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
ms.openlocfilehash: 69d7acec19a460b51819bdc30ce40e21089c7bcf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823583"
---
# <a name="create-a-user-role-for-access-control"></a>アクセス制御のユーザーの役割を作成する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックを使用して、IPAM クライアント コンソールで新しいアクセス制御ユーザー ロールを作成することができます。  
  
メンバーシップ **管理者**, 、同等の権限をこの手順を実行するために必要な最低限のですか。  
  
> [!NOTE]  
> ロールを作成した後に特定のユーザーまたは Active Directory グループにロールを割り当てるアクセス ポリシーを作成できます。 詳細については、次を参照してください。[アクセス ポリシーを作成](../../technologies/ipam/Create-an-Access-Policy.md)です。  
  
### <a name="to-create-a-role"></a>ロールを作成するには  
  
1.  サーバー マネージャーで、クリックして  **IPAM**します。 IPAM クライアント コンソールに表示されます。  
  
2.  ナビゲーション ウィンドウで、**アクセス制御**、下部のナビゲーション ウィンドウで次のようにクリックします。**ロール**します。  
  
    ![アクセス制御役割](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_01.jpg)  
  
3.  右クリック**ロール**、 をクリックし、**ユーザー ロールの追加**します。  
  
    ![ユーザー ロールを追加します。](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_02.jpg)  
  
4.  **の追加とロールの編集** ダイアログ ボックスが表示されます。 **名前**役割の機能をオフにするロールの名前を入力します。 たとえば、DNS SRV リソース レコードを管理する管理者を許可するロールを作成する場合は、ロールを名前可能性があります**IPAMSrv**します。 必要な場合、下にスクロール**操作**ロールを定義する操作の種類を検索します。 この例では、下にスクロール**DNS リソース レコードの管理操作**します。  
  
    ![DNS リソース レコードの管理操作](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_03.jpg)  
  
5.  展開**DNS リソース レコードの管理操作**、見つけて**SRV レコードの操作**します。  
  
    ![SRV レコードの操作](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_04.jpg)  
  
6.  展開し、選択**SRV レコードの操作**、順にクリックします**OK**します。  
  
    ![SRV レコードの操作を選択します。](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_05.jpg)  
  
7.  IPAM クライアント コンソールで、先ほど作成したロールをクリックします。 **詳細ビューで**ロールに対して許可された操作が表示されます。  
  
    ![新しいロールの詳細](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_06.jpg)  
  
## <a name="see-also"></a>関連項目  
[ロール ベース Access Control](Role-based-Access-Control.md)  
[IPAM を管理します。](Manage-IPAM.md)  
  


