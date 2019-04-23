---
title: 手順 3 DC1 を構成します。
description: このトピックでは、OTP 認証と Windows Server 2016 で RSA SecurID を使用した DirectAccess のデモンストレーションのテスト ラボ ガイドの一部
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 836a2a08-3d22-48d2-873e-80d7e57ebbd6
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b1762fe6e5a98529956208c4c807dfeb39c439cd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59875743"
---
# <a name="step-3-configure-dc1"></a>手順 3 DC1 を構成します。

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

DC1 は、ドメイン コント ローラー、DNS サーバー、および DHCP サーバーを corp.contoso.com ドメインとして機能します。 DC1 を次のように構成します。  
  
## <a name="verify-user1-has-a-user-principal-name-defined-on-dc1"></a>User1 には、DC1 で定義されたユーザー プリンシパル名を確認します。  
  
1.  DC1 で、サーバー マネージャーを開き、をクリックして**AD DS**左側のウィンドウでします。 右クリック**DC1**選択**Active Directory ユーザーとコンピューター**します。 左側のウィンドウで展開**corp.contoso.com\Users**User1 をダブルクリックします。  
  
2.  **アカウント**ことを確認します タブ**ユーザー ログオン名**User1 に設定されます。 そうでない場合は、入力**User1**で、**ユーザー ログオン名**フィールド。  
  
3.  **[OK]** をクリックします。 **[Active Directory ユーザーとコンピューター]** コンソールを閉じます。  
  


