---
title: "Active Directory 管理センターのナビゲーション ウィンドウをカスタマイズします。"
ms.prod: windows-server-threshold
description: "Windows Server のセキュリティ"
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.assetid: c9933d16-e153-435a-b5b7-3e594db42d5c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: e7b1128d93912f724225905bedd38131f8aab0b2
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="customize-the-active-directory-administrative-center-navigation-pane"></a>Active Directory 管理センターのナビゲーション ウィンドウをカスタマイズします。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

  You can browse through the Active Directory Administrative Center navigation pane by using the tree view, which is similar to the Active Directory Users and Computers console tree, or by using the list view.

 Whether you use the tree view or the list view, you can customize your Active Directory Administrative Center navigation pane anytime by adding various containers from the local domain or any foreign domain \(that is, a domain other than the local domain that has an established trust with the local domain\) to the navigation pane as separate nodes. Customizing the Active Directory Administrative Center navigation pane can provide quicker access to Active Directory objects. 詳細については、次を参照してください。 [Active Directory 管理センターでさまざまなドメインを管理](manage-different-domains-in-active-directory-administrative-center.md)します。

 また、ナビゲーション ウィンドウをさらにカスタマイズするには、名前を変更またはこれらの手動で追加のナビゲーション ウィンドウ ノードを削除する、これらのノードの複製を作成したり、ナビゲーション ウィンドウで上下に移動できます。

> [!NOTE]
>  既定のローカル ドメイン ノードをカスタマイズすることはできません。

### <a name="to-customize-the-active-directory-administrative-center-navigation-pane"></a>To customize the Active Directory Administrative Center navigation pane

1.  In the Active Directory Administrative Center navigation pane, right\-click the node that you want to modify. 位置や、ノードの名前を変更するかの複製を作成することができます。

2.  次のコマンドのいずれかをクリックします。

    -   **名前の変更**

    -   **重複するノードを作成します。**

    -   **削除します。**

    -   **上に移動します。**

    -   **下へ移動します。**

 リスト ビューを使用すると、最近使用した \(MRU\) リストの利点を実行できます。 MRU 一覧は、このナビゲーション ノードの少なくとも 1 つのコンテナーにアクセスするときに、ナビゲーション ノードの下に自動的に表示されます。 You can also view the current MRU list by expanding the breadcrumb bar at the top of the Active Directory Administrative Center window. MRU 一覧には、常に特定のナビゲーション ノードにアクセスした最後の 3 つのコンテナーが含まれています。 たびに特定のコンテナーを選択することでは、このコンテナーが MRU 一覧の先頭に追加され、MRU 一覧の最後のコンテナーがから削除されます。

  

