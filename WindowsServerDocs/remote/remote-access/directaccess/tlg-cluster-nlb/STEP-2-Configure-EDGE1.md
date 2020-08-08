---
title: 手順 2 EDGE1 を構成する
description: このトピックは、「windows Server 2016 用 Windows NLB を使用するクラスターでの DirectAccess のデモンストレーション」のテストラボガイドに含まれています。
manager: brianlic
ms.topic: article
ms.assetid: 84457351-1ca7-4e7c-8e2c-53d55b1fcdc0
ms.author: lizross
author: eross-msft
ms.openlocfilehash: cdd0d58f9f664211da44b125a466132ea0301bd2
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87970289"
---
# <a name="step-2-configure-edge1"></a>手順 2 EDGE1 を構成する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

DirectAccess サーバーでは、次の手順が実行されます。

## <a name="to-configure-directaccess-on-edge1"></a>EDGE1 で DirectAccess を構成するには

1.  **スタート**画面で、「**RAMgmtUI.exe**」と入力し、enter キーを押します。 [**ユーザー アカウント制御**] ダイアログ ボックスが表示されたら、表示された操作が正しいことを確認し、[**はい**] をクリックします。

2.  リモートアクセス管理コンソールの左側のウィンドウで、[**構成**] をクリックします。

3.  コンソールの中央のウィンドウの [**手順2リモートアクセスサーバー** ] 領域で、[**編集**] をクリックします。

4.  **リモートアクセスサーバーのセットアップ**ウィザードで、[**プレフィックスの構成**] をクリックします。 [**プレフィックスの構成**] ページの [ **DirectAccess クライアントコンピューターに割り当てられた IPv6 プレフィックス**] に、「 **2001: db8: 1: 1000::/59**」と入力し、[**次へ**] をクリックします。

5.  **[完了]** をクリックします。

6.  コンソールの中央のウィンドウで、[**完了**] をクリックします。

7.  [**リモートアクセスの確認**] ダイアログボックスで、構成設定を確認し、[**適用**] をクリックします。 **[リモートアクセス セットアップ ウィザードの設定を適用しています]** ダイアログ ボックスで、**[閉じる]** をクリックします。
