---
title: Active Directory 管理センターでのさまざまなドメインの管理
description: Windows Server のセキュリティ
ms.assetid: 166351c3-4076-48be-aa8f-797adf1e9d68
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 8ccd183e3450fd6c520790d9130d27b99b06a5ed
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971449"
---
# <a name="manage-different-domains-in-active-directory-administrative-center"></a>Active Directory 管理センターでのさまざまなドメインの管理

>適用先:Windows Server (半期チャネル)、Windows Server 2016

  Active Directory 管理を開くと、このコンピューターで現在ログオンしているドメインは、 \( \) Active Directory 管理センターナビゲーションウィンドウの左側のウィンドウに表示され \( \) ます。 そして、現在のログオン資格情報セットの権利に応じて、このローカル ドメインで Active Directory オブジェクトを表示または管理できます。

 同じフォレスト内の他のドメインにある Active Directory オブジェクト、またはローカルドメインとの信頼関係が確立されている別のフォレスト内のドメインで、同じログオン資格情報のセットと同じインスタンス Active Directory 管理センターを使用して表示または管理することもできます。 一 \- 方向の信頼と双 \- 方向の信頼の両方がサポートされています。

> [!NOTE]
>  ドメイン a とドメイン B の間に一方向の信頼がある場合、ドメイン a のユーザーはドメイン \- b のリソースにアクセスできますが、ドメイン b のユーザーはドメイン a のリソースにアクセスできません。ドメイン a がローカルドメインであるコンピューターで Active Directory 管理センターを実行している場合は、現在のログオン資格情報のセットと同じ Active Directory 管理センターのインスタンスでドメイン b に ただし、ドメイン B がローカル ドメインのコンピューターで Active Directory 管理センターを実行している場合は、Active Directory 管理センターの同一インスタンスで、同じ資格情報セットを使用して、ドメイン A に接続することはできません。

 この手順を完了するために最低限必要なグループ メンバーシップはありません。

### <a name="windows-server-2012-to-manage-a-foreign-domain-in-the-selected-instance-of-active-directory-administrative-center-using-the-current-set-of-logon-credentials"></a>Windows Server 2012: 現在のログオン資格情報のセットを使用して Active Directory 管理センターの選択したインスタンスで外部ドメインを管理するには

1.  Active Directory 管理センターを開くには、**サーバーマネージャー**で [**ツール**] をクリックし、[ **Active Directory 管理センター**] をクリックします。

    > [!NOTE]
    >  Active Directory 管理センターを開く別の方法として、[**スタート**] をクリックし、「 **dsac.exe**」と入力します。

2.  [**ナビゲーションノードの追加**] を開くには、次の図に示すように、[**管理**] をクリックし、[**ナビゲーションノードの追加**] をクリックします。

     ![* * [ナビゲーションノードの追加 * * UI を示すスクリーンショット](media/ADDS_ADACAddNavNode.gif)

3.  [**ナビゲーションノードの追加**] で、次の図に示すように、[**他のドメインに接続する**] をクリックします。

     ![* * [ナビゲーションノードの追加 * * UI を示すスクリーンショット](media/ADDS_ADACConnectToDomain.gif)

4.  [**接続先**] に、管理する外部ドメインの名前 ( \( たとえば、 **contoso.com**) を入力し、 \) [ **OK]** をクリックします。

5.  外部ドメインに正常に接続したら、**[ナビゲーション ノードの追加]** ウィンドウの列を参照し、Active Directory 管理センターのナビゲーション ウィンドウに追加する 1 つまたは複数のコンテナーを選択して、**[OK]** をクリックします。

### <a name="windows-server-2008-r2-to-manage-a-foreign-domain-in-the-selected-instance-of-active-directory-administrative-center-using-the-current-set-of-logon-credentials"></a>Windows Server 2008 R2: 現在のログオン資格情報のセットを使用して Active Directory 管理センターの選択したインスタンスで外部ドメインを管理するには

1. Active Directory 管理センターを開くには、**[スタート]** ボタン、**[管理ツール]**、**[Active Directory 管理センター]** の順にクリックします。

   > [!NOTE]
   >  Active Directory 管理センターを開くもう 1 つの方法として、[**スタート**] ボタン、[**ファイル名を指定して実行**] の順にクリックし、「**dsac.exe**」と入力する方法もあります。

2. [**ナビゲーションノードの追加**] を開くには、次の図に示すように、Active Directory 管理センターウィンドウの上部にある [**ナビゲーションノードの追加**] をクリックします。

    ![* * [ナビゲーションノードの追加 * * UI を示すスクリーンショット](media/click_add_nav_nodes.gif)

   > [!NOTE]
   >  **ナビゲーションノードの追加**を開く別の方法 \- として、Active Directory 管理センターナビゲーションウィンドウの空の領域内の任意の場所を右クリックし、[**ナビゲーションノードの追加**] をクリックすることもできます。

3. [**ナビゲーションノードの追加**] で、次の図に示すように、[**他のドメインに接続する**] をクリックします。

    ![[ナビゲーションノードの追加 * * * * * * 他のドメインへの接続 * * UI を示すスクリーンショット](media/add_nav_nodes.gif)

4. [**接続先**] に、管理する外部ドメインの名前 ( \( たとえば、 **contoso.com**) を入力し、 \) [ **OK]** をクリックします。

5. 外部ドメインに正常に接続したら、**[ナビゲーション ノードの追加]** ウィンドウの列を参照し、Active Directory 管理センターのナビゲーション ウィンドウに追加する 1 つまたは複数のコンテナーを選択して、**[OK]** をクリックします。

   Active Directory 管理センターナビゲーションウィンドウのカスタマイズの詳細については、「 [Active Directory 管理センターのナビゲーションウィンドウをカスタマイズ](customize-the-active-directory-administrative-center-navigation-pane.md)する」を参照してください。

   現在のログオン資格情報のセットとは異なるログオン資格情報のセットを使用して、Active Directory 管理センターを開くこともできます。 次の手順のコマンドは、通常のユーザー資格情報で Active Directory 管理センターを実行しているコンピューターにログオンし、このコンピューターの Active Directory 管理センターを使用してローカル ドメインを管理者として管理するときに役立つ場合があります。 \(このコマンドは、現在のログオン資格情報のセットとは異なる資格情報のセットを使用して、ローカルドメインとは異なる外部ドメインをリモートで管理するために Active Directory 管理センターを使用する場合にも便利です。 ただし、外部ドメインには、ローカルドメインとの信頼関係が確立されている必要があります。\)

   この手順を完了するために最低限必要なグループ メンバーシップはありません。

### <a name="to-manage-a-domain-using-logon-credentials-that-are-different-from-the-current-set-of-logon-credentials"></a>現在のログオン資格情報のセットとは異なるログオン資格情報を使用してドメインを管理するには

1.  Active Directory 管理センターを開くには、コマンド プロンプトで次のコマンドを入力し、Enter キーを押します。

     `runas /user:<domain\user> dsac`

     は、を `<domain\user>` 使用して Active Directory 管理センター開く資格情報のセットであり、 `dsac` Active Directory 管理センター実行可能ファイル名 \(Dsac.exe\) です。

     たとえば、次のコマンドを入力し、ENTER キーを押します。

     `runas /user:contoso\administrator dsac`

2.  Active Directory 管理センターが開いているときに、ナビゲーション ウィンドウを参照して、Active Directory ドメインを表示または管理します。



