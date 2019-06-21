---
title: OTP 認証を使用するリモート アクセスを計画する
description: このトピックでは、ガイド Windows Server 2016 での OTP 認証を使用したリモート アクセスの展開の一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 762bc463-eead-46ac-8b90-32355743c27c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 328e092dff23495203ee21fccbace1f7f36918d2
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280817"
---
# <a name="plan-remote-access-with-otp-authentication"></a>OTP 認証を使用するリモート アクセスを計画する

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

 Windows Server 2016 および Windows Server 2012 は、DirectAccess およびルーティングとリモート アクセス サービス (RRAS) VPN を 1 つのリモート アクセス役割に結合します。 この概要では、単一 Windows Server 2016 または Windows Server 2012 のリモート アクセスのマルチサイト展開を展開するために必要な構成手順を紹介します。  
  
  
-  手順 1:[高度な設定で単一の DirectAccess サーバーをデプロイ](https://technet.microsoft.com/windows-server-docs/networking/remote-access/directaccess/single-server-advanced/deploy-a-single-directaccess-server-with-advanced-settings)します。 この手順には、単一サーバーの展開に必要なインフラストラクチャの計画が含まれます。 これは、ネットワークとサーバーの設定、証明書の要件、DNS 設定、ネットワーク ロケーション サーバーの展開、DirectAccess 管理サーバー、Active Directory 設定、およびグループ ポリシー オブジェクト (Gpo) の計画が含まれます。  
  
-   [手順 2:RADIUS サーバーの展開を計画します。](Step-2-Plan-the-RADIUS-Server-Deployment.md)  
  
-   [手順 3:OTP 証明書の展開を計画します。](Step-3-Plan-OTP-Certificate-Deployment.md)  
  
-   [手順 4:リモート アクセス サーバーで OTP を計画します。](Step-4-Plan-for-OTP-on-the-Remote-Access-Server.md)  
  
これらの計画手順を完了したら後、は、次を参照してください。 [OTP 認証を使用したリモート アクセスの構成](https://technet.microsoft.com/windows-server-docs/networking/remote-access/ras/otp/configure/configure-ra-with-otp-authentication)します。 ラボ環境で概念実証としてマルチサイト展開を構成する方法の詳細については、次を参照してください。[テスト ラボ ガイド。OTP 認証と RSA SecurID と DirectAccess のデモンストレーション](https://technet.microsoft.com/windows-server-docs/networking/remote-access/directaccess/tlg-otp-securid/test-lab-guide-demonstrate-directaccess-with-otp-authentication-and-rsa-securid)します。  
  


