---
title: 手順 9 EDGE1 を構成します。
description: このトピックは一部のテスト ラボ ガイド-DirectAccess マルチサイト展開の Windows Server 2016 のデモンストレーション
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f6e8d85b-de65-43b3-bf3e-ec84471a1fcc
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f5d216934f0d09cdef97ce4405161862b112d632
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59864873"
---
# <a name="step-9-configure-edge1"></a>手順 9 EDGE1 を構成します。

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

EDGE1 サーバーで、次の手順が実行されます。  
  
1. EDGE1 上の DNS サーバーを構成します。 EDGE1 で corp2.corp.contoso.com ドメインの DNS サーバーを構成する必要があります。  
  
2. サブネット間のルーティングを構成します。 企業ネットワークと 2 Corpnet サブネット間の通信を有効にする EDGE1 上のルーティングを構成します。  
  
## <a name="IPv6"></a>EDGE1 上の DNS サーバーを構成します。  
  
1.  サーバー マネージャー コンソールで、次のようにクリックします。**ローカル サーバー**、し、**プロパティ**エリア、次へ を**Corpnet**、リンクをクリックします。  
  
2.  ネットワーク接続 ウィンドウで右クリック**Corpnet**、 をクリックし、**プロパティ**します。  
  
3.  **[インターネット プロトコル バージョン 4 (TCP/IPv4)]** をクリックし、**[プロパティ]** をクリックします。  
  
4.  **代替 DNS サーバー**、型**10.2.0.1**します。 **[OK]** をクリックします。  
  
5.  **[インターネット プロトコル バージョン 6 (TCP/IPv6)]** をクリックし、 **[プロパティ]** をクリックします。  
  
6.  **代替 DNS サーバー**、型**2001:db8:2::1**順にクリックします**OK**します。  
  
7.  **Corpnet プロパティ**ダイアログ ボックスで、をクリックして**閉じる**します。  
  
8.  **[ネットワーク接続]** ウィンドウを閉じます。  
  
## <a name="ConfigRouting"></a>サブネット間のルーティングを構成します。  
  
1.  **開始**画面で「**cmd.exe**、を右クリックして**cmd** をクリック**詳細**、順にクリックします**として実行管理者**します。 **[ユーザー アカウント制御]** ダイアログ ボックスが表示されたら、表示された操作が正しいことを確認し、**[はい]** をクリックします。  
  
2.  コマンド プロンプト ウィンドウで、次のコマンドを入力します。 各コマンドを入力した後 ENTER キーを押します。  
  
    ```  
    netsh interface IPv4 add route 10.2.0.0/24 Corpnet 10.0.0.254  
    netsh interface IPv6 add route 2001:db8:2::/64 Corpnet 2001:db8:1::fe  
    ```  
  
3.  コマンド プロンプト ウィンドウを閉じます。  
  


