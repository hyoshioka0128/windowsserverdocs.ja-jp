---
title: Active Directory 管理センターでさまざまなドメインを管理します。
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 5f253bd4952d8a347e97eafdb38d86fa98024b8d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839943"
---
# <a name="manage-different-domains-in-active-directory-administrative-center"></a>Active Directory 管理センターでさまざまなドメインを管理します。

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

  Active Directory 管理者をこのコンピューターに現在ログオンしているドメインを開く\(ローカル ドメイン\)Active Directory 管理センターのナビゲーション ウィンドウに表示されます\(の左側のウィンドウ\). 現在のログオン資格情報のセットの権利、に応じて表示またはこのローカル ドメインで Active Directory オブジェクトを管理できます。

 表示または同じフォレスト内の他のドメインまたはローカルでの確立された信頼のある別のフォレスト内のドメインで Active Directory オブジェクトを管理するログオン資格情報と Active Directory 管理センターの同じインスタンスの同じセットを使用することもできます。ドメイン。 両方のいずれか\-方向の信頼関係と 2 つ\-方向の信頼関係がサポートされています。

> [!NOTE]
>  1 つがある場合\-方向の信頼間ドメイン A とドメイン B によりドメイン A のユーザーがドメイン B のリソースにアクセスできますが、ドメイン B のユーザーは、コンピューター上の Active Directory 管理センターを実行している場合に、ドメイン A のリソースにアクセスできませんドメイン A が、ローカルのドメインにあると、現在の Active Directory 管理センターの同じインスタンスで、ログオン資格情報のセットとドメイン B に接続できます。 ただし、Active Directory 管理センターは、ドメイン B が、ローカル ドメイン、コンピューターで実行されて場合、は、同じ Active Directory 管理センターの同じインスタンス内の資格情報のセットを持つドメイン A に接続することはできません。

 この手順を完了するために最低限必要なグループ メンバーシップはありません。

### <a name="windows-server-2012-to-manage-a-foreign-domain-in-the-selected-instance-of-active-directory-administrative-center-using-the-current-set-of-logon-credentials"></a>Windows Server 2012:現在のログオン資格情報のセットを使用して Active Directory 管理センターの選択したインスタンスの外部ドメインを管理するには

1.  Active Directory 管理センターを開く**サーバー マネージャー**、 をクリックして**ツール**、 をクリックし、 **Active Directory 管理センター**します。

    > [!NOTE]
    >  Active Directory 管理センターを開く別の方法は をクリックする**開始**、し、入力**dsac.exe**します。

2.  開くには**ナビゲーション ノードの追加**、 をクリックして**管理**、 をクリックし、**ナビゲーション ノードの追加**次の図に示すようにします。

     ![スクリーン ショット * * ナビゲーション ノード * * UI の追加](media/ADDS_ADACAddNavNode.gif)

3.  **ナビゲーション ノードの追加**、 をクリックして**他のドメインへの接続**次の図に示すようにします。

     ![スクリーン ショット * * ナビゲーション ノード * * UI の追加](media/ADDS_ADACConnectToDomain.gif)

4.  **への接続**、管理する外部ドメインの名前を入力\(など**contoso.com**\)、順にクリックします**OK**します。

5.  外部ドメインに正常に接続されて、列参照、**ナビゲーション ノードの追加**ウィンドウで、または、Active Directory 管理センターのナビゲーション ウィンドウに追加する複数のコンテナーを選択し、クリックして**OK**します。

### <a name="windows-server-2008-r2-to-manage-a-foreign-domain-in-the-selected-instance-of-active-directory-administrative-center-using-the-current-set-of-logon-credentials"></a>Windows Server 2008 R2:現在のログオン資格情報のセットを使用して Active Directory 管理センターの選択したインスタンスの外部ドメインを管理するには

1.  Active Directory 管理センターを開くには、次のようにクリックします。**開始**、 をクリック**管理ツール**、 をクリックし、 **Active Directory 管理センター**します。

    > [!NOTE]
    >  Active Directory 管理センターを開く別の方法は をクリックする**開始**、 をクリックして**実行**、し、入力**dsac.exe**します。

2.  開くには**ナビゲーション ノードの追加**、Active Directory 管理センター ウィンドウの上部には、次のようにクリックします。**ナビゲーション ノードの追加**次の図に示すようにします。

     ![スクリーン ショット * * ナビゲーション ノード * * UI の追加](media/click_add_nav_nodes.gif)

    > [!NOTE]
    >  別の方法で開く**ナビゲーション ノードの追加**右側には、\-Active Directory 管理センターのナビゲーション ウィンドウで空の領域内をクリックし、クリックして**ナビゲーションノードの追加**.

3.  **ナビゲーション ノードの追加**、 をクリックして**他のドメインへの接続**次の図に示すようにします。

     ![スクリーン ショット * * 追加のナビゲーション ノード * * * * その他のドメイン * * UI への接続](media/add_nav_nodes.gif)

4.  **への接続**、管理する外部ドメインの名前を入力\(など**contoso.com**\)、順にクリックします**OK**します。

5.  外部ドメインに正常に接続されて、列参照、**ナビゲーション ノードの追加**ウィンドウで、または、Active Directory 管理センターのナビゲーション ウィンドウに追加する複数のコンテナーを選択し、クリックして**OK**します。

 Active Directory 管理センターのナビゲーション ウィンドウをカスタマイズする方法の詳細については、次を参照してください。 [Active Directory 管理センターのナビゲーション ウィンドウのカスタマイズ](customize-the-active-directory-administrative-center-navigation-pane.md)します。

 現在のログオン資格情報のセットとは異なるログオン資格情報のセットを使用して、Active Directory 管理センターを開くこともできます。 次の手順で、コマンドは通常のユーザーの資格情報で Active Directory 管理センターを実行しているコンピューターにログオンしている場合に便利ですがこのコンピューターを管理する Active Directory 管理センターを使用する、管理者としてローカル ドメインです。 \(このコマンドは、現在のログオン資格情報のセットとは異なる一連の資格情報でローカル ドメインとは異なる外部ドメインをリモートで管理する Active Directory 管理センターを使用する場合に便利だことができます。 ただし、外部ドメインには、ローカル ドメインでの確立された信頼が必要です。\)

 この手順を完了するために最低限必要なグループ メンバーシップはありません。

### <a name="to-manage-a-domain-using-logon-credentials-that-are-different-from-the-current-set-of-logon-credentials"></a>現在のログオン資格情報のセットとは異なるログオン資格情報を使用してドメインを管理するには

1.  Active Directory 管理センターでは、コマンド プロンプトを開く、次のコマンドを入力し、ENTER キーを押します。

     `runas /user:<domain\user> dsac`

     場所`<domain\user>`で Active Directory 管理センターを開きたいする資格情報のセットと`dsac`Active Directory 管理センターの実行可能ファイル名は、 \(Dsac.exe\)。

     たとえば、次のコマンドを入力して、Enter キーを押します。

     `runas /user:contoso\administrator dsac`

2.  Active Directory 管理センターが開いている場合に、表示または Active Directory ドメインを管理するには、ナビゲーション ウィンドウを参照します。

  

