---
title: 手順 3 DC1 を構成する
description: このトピックは、「テストラボガイド-OTP 認証を使用した DirectAccess のデモンストレーション」と「RSA SecurID for Windows Server 2016」に含まれています。
manager: brianlic
ms.topic: article
ms.assetid: 836a2a08-3d22-48d2-873e-80d7e57ebbd6
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 254789f18ca1adeebed227081c8177dc3c706e3d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971689"
---
# <a name="step-3-configure-dc1"></a>手順 3 DC1 を構成する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

DC1 は、corp.contoso.com ドメインのドメインコントローラー、DNS サーバー、および DHCP サーバーとして機能します。 DC1 を次のように構成します。

## <a name="verify-user1-has-a-user-principal-name-defined-on-dc1"></a>User1 のユーザープリンシパル名が DC1 に定義されていることを確認します。

1.  DC1 でサーバーマネージャーを開き、左側のウィンドウで [ **AD DS** ] をクリックします。 **DC1**を右クリックし、[ **Active Directory ユーザーとコンピューター**] を選択します。 左側のウィンドウで、[ **corp**] を展開し、[User1] をダブルクリックします。

2.  [**アカウント**] タブで、[**ユーザーログオン名**] が User1 に設定されていることを確認します。 それ以外の場合は、[**ユーザーログオン名**] フィールドに「 **User1** 」と入力します。

3.  **[OK]** をクリックします。 **[Active Directory ユーザーとコンピューター]** コンソールを閉じます。



