---
title: Active Directory 管理センターでのさまざまなドメインの管理
ms.prod: windows-server
description: Windows Server のセキュリティ
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.assetid: 166351c3-4076-48be-aa8f-797adf1e9d68
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 71edf6bb38cc665fe5c780ce986d0c0b8807d6ab
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386927"
---
# <a name="manage-different-domains-in-active-directory-administrative-center"></a>Active Directory 管理センターでのさまざまなドメインの管理

>適用先:Windows Server (半期チャネル)、Windows Server 2016

  Active Directory 管理を開くと、このコンピューターで現在ログオンしているドメイン @no__t、Active Directory 管理センターナビゲーションウィンドウに、左側のウィンドウの @ no__t に @no__t て、ローカルドメイン @ no__t が表示されます。 現在のログオン資格情報セットの権利に応じて、このローカルドメイン内の Active Directory オブジェクトを表示または管理できます。

 同じフォレスト内の他のドメインの Active Directory オブジェクト、またはローカルとの信頼関係が確立された別のフォレスト内のドメインで、同じログオン資格情報のセットと同じ Active Directory 管理センターインスタンスを使用して表示または管理することもできます。領域. @ No__t の信頼関係と、2つの @ no__t 方向の信頼がサポートされています。

> [!NOTE]
>  ドメイン A とドメイン B の間に1つの @ no__t の信頼がある場合 Active Directory 管理センター、ドメイン a のユーザーはドメイン B のリソースにアクセスできますが、ドメイン b のユーザーはドメイン A のリソースにアクセスできますが、ドメイン A はローカルドメインであり、現在のログオン資格情報のセットと Active Directory 管理センターの同じインスタンスでドメイン B に接続できます。 ただし、ドメイン B がローカルドメインであるコンピューターで Active Directory 管理センターを実行している場合は、Active Directory 管理センターの同じインスタンスにある同じ資格情報のセットを使用してドメイン A に接続することはできません。

 この手順を完了するために最低限必要なグループ メンバーシップはありません。

### <a name="windows-server-2012-to-manage-a-foreign-domain-in-the-selected-instance-of-active-directory-administrative-center-using-the-current-set-of-logon-credentials"></a>Windows Server 2012: 現在のログオン資格情報のセットを使用して Active Directory 管理センターの選択したインスタンスで外部ドメインを管理するには

1.  Active Directory 管理センターを開くには、**サーバーマネージャー**で **[ツール]** をクリックし、 **[Active Directory 管理センター]** をクリックします。

    > [!NOTE]
    >  Active Directory 管理センターを開く別の方法として、 **[スタート]** をクリックし、「 **dsac .exe**」と入力します。

2.  **[ナビゲーションノードの追加]** を開くには、次の図に示すように、 **[管理]** をクリックし、 **[ナビゲーションノードの追加]** をクリックします。

     ![\* * ナビゲーションノードの追加 * * UI を示すスクリーンショット](media/ADDS_ADACAddNavNode.gif)

3.  **[ナビゲーションノードの追加]** で、次の図に示すように、 **[他のドメインに接続する]** をクリックします。

     ![\* * ナビゲーションノードの追加 * * UI を示すスクリーンショット](media/ADDS_ADACConnectToDomain.gif)

4.  **[接続先]** で、@no__t 管理する外部ドメインの名前 (たとえば、 **contoso.com**\)) を入力し、 **[OK]** をクリックします。

5.  外部ドメインに正常に接続したら、**ナビゲーションノードの追加** ウィンドウの列を参照し、Active Directory 管理センターナビゲーションウィンドウに追加するコンテナーを選択し、OK をクリックします。.

### <a name="windows-server-2008-r2-to-manage-a-foreign-domain-in-the-selected-instance-of-active-directory-administrative-center-using-the-current-set-of-logon-credentials"></a>Windows Server 2008 R2:現在のログオン資格情報のセットを使用して Active Directory 管理センターの選択したインスタンスで外部ドメインを管理するには

1. Active Directory 管理センターを開くには、 **[スタート]** 、 **[管理ツール]** の順にクリックし、 **[Active Directory 管理センター]** をクリックします。

   > [!NOTE]
   >  Active Directory 管理センターを開く別の方法として、 **[スタート]** 、 **[実行]** の順にクリックして、「 **dsac .exe**」と入力します。

2. **[ナビゲーションノードの追加]** を開くには、次の図に示すように、Active Directory 管理センターウィンドウの上部にある **[ナビゲーションノードの追加]** をクリックします。

    ![\* * ナビゲーションノードの追加 * * UI を示すスクリーンショット](media/click_add_nav_nodes.gif)

   > [!NOTE]
   >  **[ナビゲーションノードの追加]** を開く別の方法として、右 @ no__t-1 をクリックして、Active Directory 管理センターナビゲーションウィンドウの空の領域の任意の場所をクリックし、 **[ナビゲーションノードの追加]** をクリックします。

3. **[ナビゲーションノードの追加]** で、次の図に示すように、 **[他のドメインに接続する]** をクリックします。

    ![ナビゲーションノードの追加 * * * * * * 他のドメインへの接続 * * UI を示すスクリーンショット](media/add_nav_nodes.gif)

4. **[接続先]** で、@no__t 管理する外部ドメインの名前 (たとえば、 **contoso.com**\)) を入力し、 **[OK]** をクリックします。

5. 外部ドメインに正常に接続したら、**ナビゲーションノードの追加** ウィンドウの列を参照し、Active Directory 管理センターナビゲーションウィンドウに追加するコンテナーを選択し、OK をクリックします。.

   Active Directory 管理センターナビゲーションウィンドウのカスタマイズの詳細については、「 [Active Directory 管理センターのナビゲーションウィンドウをカスタマイズ](customize-the-active-directory-administrative-center-navigation-pane.md)する」を参照してください。

   現在のログオン資格情報のセットとは異なるログオン資格情報のセットを使用して、Active Directory 管理センターを開くこともできます。 次の手順のコマンドは、通常のユーザー資格情報を使用して Active Directory 管理センターを実行しているコンピューターにログオンしているが、このコンピューターで Active Directory 管理センターを使用してを管理する場合に役立ちます。管理者としてのローカルドメイン。 \(This コマンドは、Active Directory 管理センターを使用して、現在のログオン資格情報のセットとは異なる資格情報のセットを使用して、ローカルドメインとは異なる外部ドメインをリモートで管理する場合にも便利です。 ただし、外部ドメインにはローカルドメインとの信頼関係が確立されている必要があります。 \)

   この手順を完了するために最低限必要なグループ メンバーシップはありません。

### <a name="to-manage-a-domain-using-logon-credentials-that-are-different-from-the-current-set-of-logon-credentials"></a>現在のログオン資格情報のセットとは異なるログオン資格情報を使用してドメインを管理するには

1.  Active Directory 管理センターを開くには、コマンドプロンプトで次のコマンドを入力し、enter キーを押します。

     `runas /user:<domain\user> dsac`

     ここで `<domain\user>` は、で Active Directory 管理センター開く資格情報のセットであり、`dsac` は Active Directory 管理センター実行可能ファイルの名前 @no__t 25 dsac .exe @ no__t です。

     たとえば、次のコマンドを入力して、Enter キーを押します。

     `runas /user:contoso\administrator dsac`

2.  Active Directory 管理センターが開いている場合は、ナビゲーションウィンドウを参照して、Active Directory ドメインを表示または管理します。

  

