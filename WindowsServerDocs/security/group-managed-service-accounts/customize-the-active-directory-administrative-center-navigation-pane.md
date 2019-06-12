---
title: Active Directory 管理センターのナビゲーション ウィンドウをカスタマイズします。
ms.prod: windows-server-threshold
description: Windows Server のセキュリティ
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.assetid: c9933d16-e153-435a-b5b7-3e594db42d5c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: a4cab0246226cf22a1b7212b832a902783952407
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446503"
---
# <a name="customize-the-active-directory-administrative-center-navigation-pane"></a>Active Directory 管理センターのナビゲーション ウィンドウをカスタマイズします。

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

  Active Directory ユーザーとコンピューターのコンソール ツリーに類似した、ツリー ビューを使用して、またはリスト ビューを使用して Active Directory 管理センターのナビゲーション ウィンドウを参照できます。

 ローカル ドメインまたは外部ドメインからのさまざまなコンテナーを追加することで、Active Directory 管理センターのナビゲーション ウィンドウをいつでもカスタマイズできますツリー ビューまたはリスト ビューを使用するかどうか\(ローカル ドメイン以外のドメインは、ローカル ドメインと信頼が確立されている\)ノードとして個別のナビゲーション ウィンドウにします。 Active Directory 管理センターのナビゲーション ウィンドウをカスタマイズすると、Active Directory オブジェクトにすばやくアクセスを提供できます。 詳細については、次を参照してください。 [Active Directory 管理センターでのさまざまなドメインの管理](manage-different-domains-in-active-directory-administrative-center.md)します。

 また、手動で追加したこれらのナビゲーション ウィンドウ ノードは、名前を変更したり、削除したり、複製を作成したり、ナビゲーション ウィンドウで上下に移動したりすることで、さらにカスタマイズすることができます。

> [!NOTE]
>  既定のローカル ドメイン ノードはカスタマイズできません。

### <a name="to-customize-the-active-directory-administrative-center-navigation-pane"></a>Active Directory 管理センターのナビゲーション ペインをカスタマイズするには

1. Active Directory 管理センターのナビゲーション ウィンドウで右\-を変更するノードをクリックします。 ノードの位置や名前を変更したり、ノードの複製を作成したりできます。

2. 次のコマンドのいずれかをクリックします。

   -   **Rename**

   -   **重複するノードを作成します。**

   -   **[削除]**

   -   **上へ移動します。**

   -   **下へ移動します。**

   リスト ビューを使用して、最近使用した利用を行う\(MRU\)一覧。 MRU 一覧は、このナビゲーション ノード内の少なくとも 1 つのコンテナーにアクセスすると、ナビゲーション ノードの下で自動的に表示されます。 Active Directory 管理センター ウィンドウの上部にある階層リンク バーを展開して、現在の MRU 一覧を表示することもできます。 MRU 一覧には、常に特定のナビゲーション ノードにアクセスした最後の 3 つのコンテナーが含まれています。 特定のコンテナーを選択するたびに、そのコンテナーが MRU 一覧の最上部に追加され、最下部のコンテナーがこの一覧から削除されます。

  

