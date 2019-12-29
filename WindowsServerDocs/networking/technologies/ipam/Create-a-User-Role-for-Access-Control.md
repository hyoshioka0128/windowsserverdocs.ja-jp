---
title: アクセス制御のユーザーの役割を作成する
description: このトピックは、Windows Server 2016 の IP アドレス管理 (IPAM) 管理ガイドに含まれています。
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ae6a42db-a104-401b-a8e6-b85c47d30b46
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 01e3216ca62cdb780342b477e575e00cdeedc6dd
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405708"
---
# <a name="create-a-user-role-for-access-control"></a>アクセス制御のユーザーの役割を作成する

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用して、IPAM クライアントコンソールで新しい Access Control ユーザーロールを作成できます。  
  
メンバーシップ **管理者**, 、同等の権限をこの手順を実行するために必要な最低限のですか。  
  
> [!NOTE]  
> ロールを作成した後、アクセスポリシーを作成して、特定のユーザーまたは Active Directory グループにロールを割り当てることができます。 詳細については、「[アクセスポリシーを作成する](../../technologies/ipam/Create-an-Access-Policy.md)」を参照してください。  
  
### <a name="to-create-a-role"></a>ロールを作成するには  
  
1.  サーバー マネージャーで、クリックして  **IPAM**します。 IPAM クライアントコンソールが表示されます。  
  
2.  ナビゲーションウィンドウで **[アクセス制御]** をクリックし、下のナビゲーションウィンドウで **[役割]** をクリックします。  
  
    ![アクセス制御ロール](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_01.jpg)  
  
3.  **[ロール]** を右クリックし、 **[ユーザーロールの追加]** をクリックします。  
  
    ![ユーザーロールの追加](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_02.jpg)  
  
4.  **[ロールの追加または編集]** ダイアログボックスが表示されます。 **[名前]** に、ロールの機能を明確にするロールの名前を入力します。 たとえば、管理者が DNS SRV リソースレコードを管理できるようにするロールを作成する場合は、ロールに**IPAMSrv**という名前を付けることができます。 必要に応じて、 **[操作]** を下にスクロールして、ロールに対して定義する操作の種類を探します。 この例では、 **[DNS リソースレコード管理操作]** まで下にスクロールします。  
  
    ![DNS リソースレコード管理操作](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_03.jpg)  
  
5.  **[DNS リソースレコード管理操作]** を展開し、 **SRV レコード操作**を探します。  
  
    ![SRV レコード操作](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_04.jpg)  
  
6.  **[SRV レコードの操作]** を展開して選択し、[ **OK]** をクリックします。  
  
    ![SRV レコード操作の選択](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_05.jpg)  
  
7.  IPAM クライアントコンソールで、先ほど作成したロールをクリックします。 [**詳細ビュー]** には、ロールに対して許可されている操作が表示されます。  
  
    ![新しいロールの詳細](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_06.jpg)  
  
## <a name="see-also"></a>関連項目  
[ロールベースの Access Control](Role-based-Access-Control.md)  
[IPAM の管理](Manage-IPAM.md)  
  


