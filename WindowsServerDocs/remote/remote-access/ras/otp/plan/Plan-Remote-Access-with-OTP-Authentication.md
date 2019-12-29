---
title: OTP 認証を使用するリモート アクセスを計画する
description: このトピックは、「Windows Server 2016 で OTP 認証を使用してリモートアクセスを展開する」の一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 762bc463-eead-46ac-8b90-32355743c27c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 69127ef86e1e14620f8cbb29322e930c6d921702
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404361"
---
# <a name="plan-remote-access-with-otp-authentication"></a>OTP 認証を使用するリモート アクセスを計画する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

 Windows Server 2016 および Windows Server 2012 は、DirectAccess とルーティングとリモートアクセスサービス (RRAS) VPN を1つのリモートアクセスの役割に結合します。 この概要では、単一の Windows Server 2016 または Windows Server 2012 リモートアクセスマルチサイト展開を展開するために必要な構成手順の概要を説明します。  
  
  
-  手順 1:[詳細設定を使用して単一の DirectAccess サーバーを展開](https://technet.microsoft.com/windows-server-docs/networking/remote-access/directaccess/single-server-advanced/deploy-a-single-directaccess-server-with-advanced-settings)します。 この手順には、単一のサーバーを展開するために必要なインフラストラクチャの計画が含まれます。 これには、ネットワークとサーバーの設定、証明書の要件、DNS 設定、ネットワークロケーションサーバーの展開、DirectAccess 管理サーバー、Active Directory 設定、グループポリシーオブジェクト (Gpo) の計画が含まれます。  
  
-   [手順 2: RADIUS サーバーの展開を計画する](Step-2-Plan-the-RADIUS-Server-Deployment.md)  
  
-   [手順 3: OTP 証明書の展開を計画する](Step-3-Plan-OTP-Certificate-Deployment.md)  
  
-   [手順 4: リモートアクセスサーバーで OTP を計画する](Step-4-Plan-for-OTP-on-the-Remote-Access-Server.md)  
  
これらの計画手順を完了したら、「 [OTP 認証を使用したリモートアクセスの構成](https://technet.microsoft.com/windows-server-docs/networking/remote-access/ras/otp/configure/configure-ra-with-otp-authentication)」を参照してください。 ラボ環境での概念実証としてマルチサイト展開を構成する方法については、「[テストラボガイド: OTP 認証と RSA SecurID を使用した DirectAccess のデモンストレーション](https://technet.microsoft.com/windows-server-docs/networking/remote-access/directaccess/tlg-otp-securid/test-lab-guide-demonstrate-directaccess-with-otp-authentication-and-rsa-securid)」を参照してください。  
  


