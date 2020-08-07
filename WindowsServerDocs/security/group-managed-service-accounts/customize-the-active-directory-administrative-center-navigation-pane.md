---
title: Active Directory 管理センターナビゲーションウィンドウのカスタマイズ
description: Windows Server のセキュリティ
ms.assetid: c9933d16-e153-435a-b5b7-3e594db42d5c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 4ecadc09eaa0433458a0224582c3c2ba67dd938f
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971479"
---
# <a name="customize-the-active-directory-administrative-center-navigation-pane"></a>Active Directory 管理センターナビゲーションウィンドウのカスタマイズ

>適用先:Windows Server (半期チャネル)、Windows Server 2016

  Active Directory 管理センターナビゲーションウィンドウを参照するには、ツリービューを使用します。これは、[Active Directory ユーザーとコンピューター] コンソールツリーに似ています。また、リストビューを使用して参照することもできます。

 ツリービューとリストビューのどちらを使用する場合でも、ローカルドメインまたは外部ドメインからさまざまなコンテナーを追加することで、いつでも Active Directory 管理センターナビゲーションウィンドウをカスタマイズでき \( ます。これは、ローカルドメインの信頼関係が確立されているローカルドメイン以外のドメインは、 \) 別のノードとしてナビゲーションウィンドウに表示されます。 Active Directory 管理センターナビゲーションウィンドウをカスタマイズすると、Active Directory オブジェクトにすばやくアクセスできるようになります。 詳細については、「 [Active Directory 管理センターでのさまざまなドメインの管理](manage-different-domains-in-active-directory-administrative-center.md)」を参照してください。

 また、手動で追加したこれらのナビゲーション ウィンドウ ノードは、名前を変更したり、削除したり、複製を作成したり、ナビゲーション ウィンドウで上下に移動したりすることで、さらにカスタマイズすることができます。

> [!NOTE]
>  既定のローカル ドメイン ノードはカスタマイズできません。

### <a name="to-customize-the-active-directory-administrative-center-navigation-pane"></a>Active Directory 管理センターのナビゲーション ウィンドウをカスタマイズするには

1. Active Directory 管理センターナビゲーションウィンドウで、 \- 変更するノードを右クリックします。 ノードの位置や名前を変更したり、ノードの複製を作成したりできます。

2. 次のコマンドのいずれかをクリックします。

   -   **Rename**

   -   **複製ノードの作成**

   -   **Remove**

   -   **上へ移動**

   -   **下へ移動**

   リストビューを使用すると、最近使用した MRU 一覧を利用 \( でき \) ます。 このナビゲーションノードで少なくとも1つのコンテナーにアクセスすると、[MRU] の一覧がナビゲーションノードの下に自動的に表示されます。 Active Directory 管理センターウィンドウの上部にある階層リンクバーを展開して、現在の MRU 一覧を表示することもできます。 MRU の一覧には、常に、特定のナビゲーションノードでアクセスした最後の3つのコンテナーが含まれています。 特定のコンテナーを選択するたびに、そのコンテナーが MRU 一覧の最上部に追加され、最下部のコンテナーがこの一覧から削除されます。



