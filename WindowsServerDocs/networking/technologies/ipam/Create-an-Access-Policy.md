---
title: アクセス ポリシーを作成する
description: このトピックは、Windows Server 2016 の IP アドレス管理 (IPAM) 管理ガイドに含まれています。
manager: brianlic
ms.topic: article
ms.assetid: 854bd064-2f86-4678-a940-a04b3e48ae10
ms.author: lizross
author: eross-msft
ms.openlocfilehash: d454bef1a6bc15b5f8a6f2e6f78773785ad5af69
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87966569"
---
# <a name="create-an-access-policy"></a>アクセス ポリシーを作成する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用して、IPAM クライアントコンソールでアクセスポリシーを作成できます。

この手順を実行するには、**Administrators** のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。

> [!NOTE]
> Active Directory では、特定のユーザーまたはユーザーグループのアクセスポリシーを作成できます。 アクセスポリシーを作成するときは、組み込みの IPAM ロールまたは作成したカスタムロールのいずれかを選択する必要があります。 カスタムロールの詳細については、「 [Create a User Role for Access Control](../../technologies/ipam/Create-a-User-Role-for-Access-Control.md)」を参照してください。

### <a name="to-create-an-access-policy"></a>アクセスポリシーを作成するには

1.  サーバー マネージャーで、クリックして  **IPAM**します。 IPAM クライアントコンソールが表示されます。

2.  ナビゲーションウィンドウで、[**アクセス制御**] をクリックします。 下のナビゲーションウィンドウで、[**アクセスポリシー**] を右クリックし、[**アクセスポリシーの追加**] をクリックします。

    ![アクセスポリシーの追加](../../media/Create-an-Access-Policy/ipam_CreateAP_01.jpg)

3.  [**アクセスポリシーの追加**] ダイアログボックスが表示されます。 [**ユーザー設定**] で、[**追加**] をクリックします。

    ![アクセスポリシーの追加](../../media/Create-an-Access-Policy/ipam_CreateAP_02.jpg)

4.  **[ユーザーまたはグループの選択**] ダイアログボックスが表示されます。 **[場所]** をクリックします。

    ![ユーザーまたはグループの場所](../../media/Create-an-Access-Policy/ipam_CreateAP_03.jpg)

5.  [**場所**] ダイアログボックスが表示されます。 ユーザーアカウントが格納されている場所を参照して場所を選択し、[ **OK]** をクリックします。 [**場所**] ダイアログボックスが閉じます。

    ![場所を選択する](../../media/Create-an-Access-Policy/ipam_CreateAP_04.jpg)

6.  [**ユーザーまたはグループの選択**] ダイアログボックスの **[選択するオブジェクト名を入力してください**] に、アクセスポリシーを作成するユーザーアカウント名を入力します。 **[OK]** をクリックします。

7.  [**アクセスポリシーの追加**] の [**ユーザー設定**] には、ポリシーが適用されるユーザーアカウントが**ユーザーエイリアス**に含まれるようになりました。 [**アクセス設定**] で、[**新規**] をクリックします。

    ![新しいアクセス設定](../../media/Create-an-Access-Policy/ipam_CreateAP_05.jpg)

8.  [**アクセスポリシーの追加**] で、[**アクセス設定**] が [**新しい設定**] に変わります。

    ![ダイアログボックスの名前が新しい設定に変更される](../../media/Create-an-Access-Policy/ipam_CreateAP_06.jpg)

9. [**ロールの選択**] をクリックして、ロールの一覧を展開します。 組み込みのロールのいずれかを選択するか、新しいロールを作成した場合は、作成したロールのいずれかを選択します。 たとえば、ユーザーに適用する IPAMSrv ロールを作成した場合は、[ **IPAMSrv**] をクリックします。

    ![ロールの選択](../../media/Create-an-Access-Policy/ipam_CreateAP_07.jpg)

10. [**設定の追加**] をクリックします。

    ![新しい設定の追加](../../media/Create-an-Access-Policy/ipam_CreateAP_08.jpg)

11. ロールがアクセスポリシーに追加されます。 追加のアクセスポリシーを作成するには、[**適用**] をクリックし、作成するポリシーごとにこれらの手順を繰り返します。 追加のポリシーを作成しない場合は、[ **OK]** をクリックします。

    ![[適用] または [OK] をクリック](../../media/Create-an-Access-Policy/ipam_CreateAP_09.jpg)

12. IPAM クライアントコンソールの表示ウィンドウで、新しいアクセスポリシーが作成されていることを確認します。

    ![新しいアクセスポリシーを表示する](../../media/Create-an-Access-Policy/ipam_CreateAP_09a.jpg)

## <a name="see-also"></a>参照
[ロールベースの Access Control](Role-based-Access-Control.md) 
[IPAM の管理](Manage-IPAM.md)



