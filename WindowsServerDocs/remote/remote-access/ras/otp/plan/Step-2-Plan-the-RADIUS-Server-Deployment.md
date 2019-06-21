---
title: 手順 2、RADIUS サーバー展開を計画します。
description: このトピックでは、ガイド Windows Server 2016 での OTP 認証を使用したリモート アクセスの展開の一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2d6ad863-02a5-49b0-9aff-d189e78b2b80
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f74a83c3962c7accd76fbf07307216742ada863d
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280827"
---
# <a name="step-2-plan-the-radius-server-deployment"></a>手順 2、RADIUS サーバー展開を計画します。

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

単一のリモート アクセス サーバーをデプロイした後は、ワンタイム パスワード (OTP) 認証サーバーを計画します。  
  
|タスク|説明|  
|----|--------|  
|2.1、RADIUS サーバーを計画します。|OTP 認証サーバーの場合は、Windows Server 2016 および Windows Server 2012 でのリモート アクセスは、パスワード認証プロトコル (PAP) をサポートする任意の RADIUS が有効な OTP サーバーをサポートします。|  
  
## <a name="BKMK_1.1"></a>2.1、RADIUS サーバーを計画します。  
OTP 認証用の RADIUS サーバーを計画するときは、次に注意してください。  
  
-   ほとんどの種類の OTP 展開では、RADIUS エージェントとしてリモート アクセス サーバーを構成する必要があります。 詳細については、OTP ベンダーのマニュアルを参照してください。  
  
-   OTP 展開では、すべての RADIUS サーバーと Active Directory ユーザーを同期する必要があります。  
  
-   RADIUS サーバーは、ドメイン メンバーである必要はありません。  
  
-   RADIUS サーバーを展開するときは、共有シークレットと RADIUS トラフィックにポート番号を設定します。 これらの詳細をメモしてをおきますリモート アクセス サーバーを構成するときに必要な。  
  
RSA SecurID サーバーでの OTP 認証を設定する例のテスト ラボ ガイドを表示する[テスト ラボ ガイド。OTP 認証と RSA SecurID と DirectAccess のデモンストレーション](https://technet.microsoft.com/windows-server-docs/networking/remote-access/directaccess/tlg-otp-securid/test-lab-guide-demonstrate-directaccess-with-otp-authentication-and-rsa-securid)します。  
  
  
  


