---
title: リモート アクセス サーバーで OTP を手順 4. プラン
description: このトピックでは、ガイド Windows Server 2016 での OTP 認証を使用したリモート アクセスの展開の一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4b97b2fd-767a-45c1-a64e-5b3edd0c8a47
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 470eebc82177a21985afb8d0bf143427a33d65fb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825443"
---
# <a name="step-4-plan-for-otp-on-the-remote-access-server"></a>リモート アクセス サーバーで OTP を手順 4. プラン

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

ワンタイム パスワード (OTP) の RADIUS サーバーおよび証明書の設定の計画、後にリモート アクセスの OTP の展開を計画する最後の手順がリモート アクセス サーバーでクライアント OTP 設定の計画です。  
  
|タスク|説明|  
|----|--------|  
|[4.1 が OTP クライアントの除外対象を計画します。](#bkmk_4_1_Exemptions)|OTP を使用して認証を必要としないユーザーの除外を計画します。|  
|[4.2 は、Windows 7 クライアントを計画します。](#bkmk_4_2_Win7)|Windows 7 クライアント コンピューターに、DirectAccess Connectivity Assistant (DCA) 2.0 を展開する予定です。|  
|[4.3 スマート カードのプラン](#BKMK_smartcard)|追加の承認のスマート カードの使用を計画します。|  
  
## <a name="bkmk_4_1_Exemptions"></a>4.1 が OTP クライアントの除外対象を計画します。  
OTP 認証を有効にすると、既定ではすべてのユーザーはユーザー名とパスワードおよび OTP 資格情報の組み合わせを使用して認証を要求します。 ただし、OTP せず、ユーザー名とパスワードのみを使用して認証を選択したユーザーを許可することができます。 これを行うには、セキュリティ グループを作成しに OTP 認証から除外するユーザーを追加します。  
  
> [!NOTE]  
> という事実により、単一フォレストからのクライアント コンピュータのみを除外することがありますクライアントの除外対象にその 1 つだけのセキュリティ グループを選択できます。  
  
## <a name="bkmk_4_2_Win7"></a>4.2 は、Windows 7 クライアントを計画します。  
既定では、Windows 7 クライアント コンピューターは、OTP を使用して認証できません。  Windows 7 クライアント コンピューターでは、Windows Server 2012 のリモート アクセス展開で OTP を使用して認証に DCA 2.0 が必要です。 DCA 2.0 の詳細については、次を参照してください。 [DirectAccess Connectivity Assistant 2.0](https://go.microsoft.com/fwlink/?LinkId=253699) 、Microsoft ダウンロード センター。  
  
## <a name="BKMK_smartcard"></a>4.3 スマート カードのプラン  
OTP 認証が有効にすると、追加の承認のスマート カードの使用を有効にするオプションは、使用します。 ユーザーのスマート カードが機能していないことに、一時的なアクセスを許可するセキュリティ グループを作成します。  
  
## <a name="BKMK_Links"></a>参照してください。  
  
-   [OTP 認証を使用した DirectAccess を構成します。](https://technet.microsoft.com/windows-server-docs/networking/remote-access/ras/otp/deploy-ra-otp)  
  


