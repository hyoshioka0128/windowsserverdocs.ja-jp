---
title: 手順 2 EDGE1 を構成します。
description: このトピックは一部のテスト ラボ ガイド - Windows Server 2016 で Windows NLB を使用するクラスターでの DirectAccess のデモンストレーション
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 84457351-1ca7-4e7c-8e2c-53d55b1fcdc0
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6c31e65fc7210849564bd0541085322a7a6c284e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838583"
---
# <a name="step-2-configure-edge1"></a>手順 2 EDGE1 を構成します。

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

次の手順は、DirectAccess サーバーで実行されます。

## <a name="to-configure-directaccess-on-edge1"></a>EDGE1 で DirectAccess を構成するには
  
1.  **開始**画面で「**RAMgmtUI.exe**、し、ENTER キーを押します。 **[ユーザー アカウント制御]** ダイアログ ボックスが表示されたら、表示された操作が正しいことを確認し、**[はい]** をクリックします。  
  
2.  左側のウィンドウで、リモート アクセス管理コンソールで次のようにクリックします。**構成**します。  
  
3.  コンソールの中央のペインでの**手順 2 リモート アクセス サーバー**領域で、をクリックして**編集**。  
  
4.  **リモート アクセス サーバーのセットアップ**ウィザード、をクリックして**プレフィックスの構成**します。 **プレフィックスの構成** ページの  **DirectAccess クライアント コンピューターに割り当てられている IPv6 プレフィックス**、入力**2001:db8:1:1000::/59**、 をクリックし、 **次へ**.  
  
5.  **[Finish]**(完了) をクリックします。  
  
6.  コンソールの中央のペインで次のようにクリックします。**完了**します。  
  
7.  **リモート アクセスのレビュー**ダイアログ ボックスで、構成設定を確認し、順にクリックします**適用**します。 **[リモートアクセス セットアップ ウィザードの設定を適用しています]** ダイアログ ボックスで、 **[閉じる]** をクリックします。
