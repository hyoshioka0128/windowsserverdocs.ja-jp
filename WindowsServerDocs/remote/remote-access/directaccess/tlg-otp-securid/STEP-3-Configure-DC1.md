---
title: 手順 3 DC1 を構成します。
description: このトピックでは、OTP 認証と Windows Server 2016 で RSA SecurID を使用した DirectAccess のデモンストレーションのテスト ラボ ガイドの一部
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 836a2a08-3d22-48d2-873e-80d7e57ebbd6
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 338e214ac10796d3f9864aef74190f2d27f173b7
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67281354"
---
# <a name="step-3-configure-dc1"></a>手順 3 DC1 を構成します。

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

DC1 は、ドメイン コント ローラー、DNS サーバー、および DHCP サーバーを corp.contoso.com ドメインとして機能します。 DC1 を次のように構成します。  
  
## <a name="verify-user1-has-a-user-principal-name-defined-on-dc1"></a>User1 には、DC1 で定義されたユーザー プリンシパル名を確認します。  
  
1.  DC1 で、サーバー マネージャーを開き、をクリックして**AD DS**左側のウィンドウでします。 右クリック**DC1**選択**Active Directory ユーザーとコンピューター**します。 左側のウィンドウで展開**corp.contoso.com\Users**User1 をダブルクリックします。  
  
2.  **アカウント**ことを確認します タブ**ユーザー ログオン名**User1 に設定されます。 そうでない場合は、入力**User1**で、**ユーザー ログオン名**フィールド。  
  
3.  **[OK]** をクリックします。 **[Active Directory ユーザーとコンピューター]** コンソールを閉じます。  
  


