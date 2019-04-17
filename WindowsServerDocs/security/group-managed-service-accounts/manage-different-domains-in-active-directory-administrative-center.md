---
title: "Active Directory 管理センターでさまざまなドメインを管理します。"
ms.prod: windows-server-threshold
description: "Windows Server のセキュリティ"
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.assetid: 166351c3-4076-48be-aa8f-797adf1e9d68
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 5f253bd4952d8a347e97eafdb38d86fa98024b8d
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="manage-different-domains-in-active-directory-administrative-center"></a>Active Directory 管理センターでさまざまなドメインを管理します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

  When you open Active Directory Administrative, the domain that you are currently logged on to on this computer \(the local domain\) appears in the Active Directory Administrative Center navigation pane \(the left pane\). Depending on the rights of your current set of logon credentials, you can view or manage the Active Directory objects in this local domain.

 You can also use the same set of logon credentials and the same instance of Active Directory Administrative Center to view or manage Active Directory objects in any other domain in the same forest, or a domain in another forest that has an established trust with the local domain. 特定の方向の信頼関係と two\ 方向の信頼関係の両方がサポートされます。

> [!NOTE]
>  If there is a one\-way trust between Domain A and Domain B through which users in Domain A can access resources in Domain B but users in Domain B cannot access resources in Domain A, if you are running Active Directory Administrative Center on the computer where Domain A is your local domain, you can connect to Domain B with the current set of logon credentials and in the same instance of Active Directory Administrative Center. But if you are running Active Directory Administrative Center on the computer where Domain B is your local domain, you cannot connect to Domain A with the same set of credentials in the same instance of the Active Directory Administrative Center.

 この手順を実行するために必要以上のグループ メンバーシップはありません。

### <a name="windows-server-2012-to-manage-a-foreign-domain-in-the-selected-instance-of-active-directory-administrative-center-using-the-current-set-of-logon-credentials"></a>Windows Server 2012: To manage a foreign domain in the selected instance of Active Directory Administrative Center using the current set of logon credentials

1.  To open Active Directory Administrative Center, in **Server Manager**, click **Tools**, and then click **Active Directory Administrative Center**.

    > [!NOTE]
    >  Another way to open Active Directory Administrative Center is to click **Start**, and then type **dsac.exe**.

2.  開くには**ナビゲーション ノードの追加**、] をクリックして**管理**、] をクリックし、**ナビゲーション ノードの追加**、次の図に示すようにします。

     ![ショット * * ナビゲーション ノード * * UI の追加](media/ADDS_ADACAddNavNode.gif)

3.  **ナビゲーション ノードの追加**、] をクリックして**他のドメインに接続する**、次の図に示すようにします。

     ![ショット * * ナビゲーション ノード * * UI の追加](media/ADDS_ADACConnectToDomain.gif)

4.  **への接続**、管理する外部ドメインの名前を入力 \ (たとえば、**contoso.com**\)、] をクリックし、**[OK]**します。

5.  When you are successfully connected to the foreign domain, browse through the columns in the **Add Navigation Nodes** window, select the container or containers to add to your Active Directory Administrative Center navigation pane, and then click **OK**.

### <a name="windows-server-2008-r2-to-manage-a-foreign-domain-in-the-selected-instance-of-active-directory-administrative-center-using-the-current-set-of-logon-credentials"></a>Windows Server 2008 R2: To manage a foreign domain in the selected instance of Active Directory Administrative Center using the current set of logon credentials

1.  To open Active Directory Administrative Center, click **Start**, click **Administrative Tools**, and then click **Active Directory Administrative Center**.

    > [!NOTE]
    >  Another way to open Active Directory Administrative Center is to click **Start**, click **Run**, and then type **dsac.exe**.

2.  To open **Add Navigation Nodes**, near the top of the Active Directory Administrative Center window, click **Add Navigation Nodes** as shown in the following illustration.

     ![ショット * * ナビゲーション ノード * * UI の追加](media/click_add_nav_nodes.gif)

    > [!NOTE]
    >  Another way to open **Add Navigation Nodes** is to right\-click anywhere in the empty space in the Active Directory Administrative Center navigation pane, and then click **Add Navigation Nodes**.

3.  **ナビゲーション ノードの追加**、] をクリックして**他のドメインに接続する**、次の図に示すようにします。

     ![ショット * * 追加ナビゲーション ノード * * * * 他のドメイン * * UI への接続](media/add_nav_nodes.gif)

4.  **への接続**、管理する外部ドメインの名前を入力 \ (たとえば、**contoso.com**\)、] をクリックし、**[OK]**します。

5.  When you are successfully connected to the foreign domain, browse through the columns in the **Add Navigation Nodes** window, select the container or containers to add to your Active Directory Administrative Center navigation pane, and then click **OK**.

 For more information about customizing the Active Directory Administrative Center navigation pane, see [Customize the Active Directory Administrative Center Navigation Pane](customize-the-active-directory-administrative-center-navigation-pane.md).

 You can also open Active Directory Administrative Center by using a set of logon credentials that is different from your current set of logon credentials. The command in the following procedure can be useful if you are logged on to the computer that is running Active Directory Administrative Center with normal user credentials, but you want to use Active Directory Administrative Center on this computer to manage your local domain as an administrator. \(This command can also be useful if you want to use Active Directory Administrative Center to remotely manage a foreign domain that is different from your local domain with a set of credentials that is different from your current set of logon credentials. ただし、外部ドメインのローカル ドメインと信頼が確立されている必要があります \)。

 この手順を実行するために必要以上のグループ メンバーシップはありません。

### <a name="to-manage-a-domain-using-logon-credentials-that-are-different-from-the-current-set-of-logon-credentials"></a>現在のログオン資格情報のセットとは異なるログオン資格情報を使用してドメインを管理するには

1.  To open Active Directory Administrative Center, at a command prompt, type the following command, and then press ENTER:

     `runas /user:<domain\user> dsac`

     Where `<domain\user>` is the set of credentials that you want to open Active Directory Administrative Center with and `dsac` is the Active Directory Administrative Center executable file name \(Dsac.exe\).

     たとえば、次のコマンドを入力し、Enter キーを押します。

     `runas /user:contoso\administrator dsac`

2.  When Active Directory Administrative Center is open, browse through the navigation pane to view or manage your Active Directory domain.

  

