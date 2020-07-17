---
title: Active Directory 管理センターでのさまざまなドメインの管理
description: Windows Server のセキュリティ
ms.prod: windows-server
ms.assetid: 166351c3-4076-48be-aa8f-797adf1e9d68
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 6690ffbc558db4026c3fe67168907ca953ad4081
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856985"
---
# <a name="manage-different-domains-in-active-directory-administrative-center"></a>Active Directory 管理センターでのさまざまなドメインの管理

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

  Active Directory 管理を開くと、このコンピューターで現在ログオンしているドメイン \(ローカルドメイン\) Active Directory 管理センターナビゲーションウィンドウの左側のウィンドウ \(に表示されます。\) 現在のログオン資格情報セットの権利に応じて、このローカルドメイン内の Active Directory オブジェクトを表示または管理できます。

 同じフォレスト内の他のドメインにある Active Directory オブジェクト、またはローカルドメインとの信頼関係が確立されている別のフォレスト内のドメインで、同じログオン資格情報のセットと同じインスタンス Active Directory 管理センターを使用して表示または管理することもできます。 1つの\-方向の信頼と2つの\-方向の信頼の両方がサポートされています。

> [!NOTE]
>  ドメイン a とドメイン B の間に\-一方向の信頼がある場合、ドメイン a のユーザーはドメイン B のリソースにアクセスできますが、ドメイン B のユーザーはドメイン A のリソースにアクセスできません。ドメイン A がローカルドメインであるコンピューターで Active Directory 管理センターを実行している場合は、現在のログオン資格情報のセットと同じ Active Directory 管理センターのインスタンスでドメイン B に ただし、ドメイン B がローカルドメインであるコンピューターで Active Directory 管理センターを実行している場合は、Active Directory 管理センターの同じインスタンスにある同じ資格情報のセットを使用してドメイン A に接続することはできません。

 この手順を完了するために最低限必要なグループ メンバーシップはありません。

### <a name="windows-server-2012-to-manage-a-foreign-domain-in-the-selected-instance-of-active-directory-administrative-center-using-the-current-set-of-logon-credentials"></a>Windows Server 2012: 現在のログオン資格情報のセットを使用して Active Directory 管理センターの選択したインスタンスで外部ドメインを管理するには

1.  Active Directory 管理センターを開くには、**サーバーマネージャー**で **[ツール]** をクリックし、 **[Active Directory 管理センター]** をクリックします。

    > [!NOTE]
    >  Active Directory 管理センターを開く別の方法として、 **[スタート]** をクリックし、「 **dsac .exe**」と入力します。

2.  **[ナビゲーションノードの追加]** を開くには、次の図に示すように、 **[管理]** をクリックし、 **[ナビゲーションノードの追加]** をクリックします。

     ![\* * ナビゲーションノードの追加 * * UI を示すスクリーンショット](media/ADDS_ADACAddNavNode.gif)

3.  **[ナビゲーションノードの追加]** で、次の図に示すように、 **[他のドメインに接続する]** をクリックします。

     ![\* * ナビゲーションノードの追加 * * UI を示すスクリーンショット](media/ADDS_ADACConnectToDomain.gif)

4.  **[接続先]** に \(管理する外部ドメインの名前 (たとえば、 **contoso.com**\)) を入力し、[ **OK]** をクリックします。

5.  外部ドメインに正常に接続したら、 **[ナビゲーションノードの追加]** ウィンドウの列を参照し、Active Directory 管理センターナビゲーションウィンドウに追加するコンテナーを選択し、 **[OK]** をクリックします。

### <a name="windows-server-2008-r2-to-manage-a-foreign-domain-in-the-selected-instance-of-active-directory-administrative-center-using-the-current-set-of-logon-credentials"></a>Windows Server 2008 R2: 現在のログオン資格情報のセットを使用して Active Directory 管理センターの選択したインスタンスで外部ドメインを管理するには

1. Active Directory 管理センターを開くには、 **[スタート]** 、 **[管理ツール]** の順にクリックし、 **[Active Directory 管理センター]** をクリックします。

   > [!NOTE]
   >  Active Directory 管理センターを開く別の方法として、 **[スタート]** 、 **[実行]** の順にクリックして、「 **dsac .exe**」と入力します。

2. **[ナビゲーションノードの追加]** を開くには、次の図に示すように、Active Directory 管理センターウィンドウの上部にある **[ナビゲーションノードの追加]** をクリックします。

    ![\* * ナビゲーションノードの追加 * * UI を示すスクリーンショット](media/click_add_nav_nodes.gif)

   > [!NOTE]
   >  **[ナビゲーションノードの追加]** を開くもう1つの方法は、右\-Active Directory 管理センターのナビゲーションウィンドウの空の領域内の任意の場所をクリックし、 **[ナビゲーションノードの追加]** をクリックする方法です。

3. **[ナビゲーションノードの追加]** で、次の図に示すように、 **[他のドメインに接続する]** をクリックします。

    ![ナビゲーションノードの追加 * * * * * * 他のドメインへの接続 * * UI を示すスクリーンショット](media/add_nav_nodes.gif)

4. **[接続先]** に \(管理する外部ドメインの名前 (たとえば、 **contoso.com**\)) を入力し、[ **OK]** をクリックします。

5. 外部ドメインに正常に接続したら、 **[ナビゲーションノードの追加]** ウィンドウの列を参照し、Active Directory 管理センターナビゲーションウィンドウに追加するコンテナーを選択し、 **[OK]** をクリックします。

   Active Directory 管理センターナビゲーションウィンドウのカスタマイズの詳細については、「 [Active Directory 管理センターのナビゲーションウィンドウをカスタマイズ](customize-the-active-directory-administrative-center-navigation-pane.md)する」を参照してください。

   現在のログオン資格情報のセットとは異なるログオン資格情報のセットを使用して、Active Directory 管理センターを開くこともできます。 次の手順のコマンドは、通常のユーザー資格情報を使用して Active Directory 管理センターを実行しているコンピューターにログオンしているが、このコンピューターで Active Directory 管理センターを使用して、ローカルドメインを管理者として管理する場合に役立ちます。 このコマンド \(、Active Directory 管理センターを使用して、現在のログオン資格情報のセットとは異なる資格情報のセットを使用して、ローカルドメインとは異なる外部ドメインをリモートで管理する場合にも役立ちます。 ただし、外部ドメインには、ローカルドメインとの信頼関係が確立されている必要があります。\)

   この手順を完了するために最低限必要なグループ メンバーシップはありません。

### <a name="to-manage-a-domain-using-logon-credentials-that-are-different-from-the-current-set-of-logon-credentials"></a>現在のログオン資格情報のセットとは異なるログオン資格情報を使用してドメインを管理するには

1.  Active Directory 管理センターを開くには、コマンドプロンプトで次のコマンドを入力し、enter キーを押します。

     `runas /user:<domain\user> dsac`

     ここで `<domain\user>` は Active Directory 管理センターで開く必要がある資格情報のセットであり、`dsac` は Active Directory 管理センター実行可能ファイルの名前 \(Dsac .exe\)です。

     たとえば、次のコマンドを入力して、Enter キーを押します。

     `runas /user:contoso\administrator dsac`

2.  Active Directory 管理センターが開いている場合は、ナビゲーションウィンドウを参照して、Active Directory ドメインを表示または管理します。

  

