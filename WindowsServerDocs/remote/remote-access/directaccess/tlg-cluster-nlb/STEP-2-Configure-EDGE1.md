---
title: 手順 2 EDGE1 を構成する
description: このトピックは、「windows Server 2016 用 Windows NLB を使用するクラスターでの DirectAccess のデモンストレーション」のテストラボガイドに含まれています。
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 84457351-1ca7-4e7c-8e2c-53d55b1fcdc0
ms.author: lizross
author: eross-msft
ms.openlocfilehash: eea83bd9788ffd704b6169c140adc68465f9325d
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80310841"
---
# <a name="step-2-configure-edge1"></a>手順 2 EDGE1 を構成する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

DirectAccess サーバーでは、次の手順が実行されます。

## <a name="to-configure-directaccess-on-edge1"></a>EDGE1 で DirectAccess を構成するには
  
1.  **スタート**画面で「**ramgmtui.exe**」と入力し、enter キーを押します。 **[ユーザー アカウント制御]** ダイアログ ボックスが表示された場合、表示された操作が目的の操作であることを確認して、 **[はい]** をクリックします。  
  
2.  リモートアクセス管理コンソールの左側のウィンドウで、 **[構成]** をクリックします。  
  
3.  コンソールの中央のウィンドウの **[手順2リモートアクセスサーバー]** 領域で、 **[編集]** をクリックします。  
  
4.  **リモートアクセスサーバーのセットアップ**ウィザードで、 **[プレフィックスの構成]** をクリックします。 **[プレフィックスの構成]** ページの **[DirectAccess クライアントコンピューターに割り当てられた IPv6 プレフィックス]** に、「 **2001: db8: 1: 1000::/59**」と入力し、 **[次へ]** をクリックします。  
  
5.  **[完了]** をクリックします。  
  
6.  コンソールの中央のウィンドウで、 **[完了]** をクリックします。  
  
7.  **[リモートアクセスの確認]** ダイアログボックスで、構成設定を確認し、 **[適用]** をクリックします。 **[リモートアクセス セットアップ ウィザードの設定を適用しています]** ダイアログ ボックスで、 **[閉じる]** をクリックします。
