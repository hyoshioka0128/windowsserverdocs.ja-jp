---
title: OTP 認証を使用するリモート アクセスを計画する
description: このトピックは、「Windows Server 2016 で OTP 認証を使用してリモートアクセスを展開する」の一部です。
manager: brianlic
ms.topic: article
ms.assetid: 762bc463-eead-46ac-8b90-32355743c27c
ms.author: lizross
author: eross-msft
ms.openlocfilehash: f7fa8e9074601222d35baecc7352f245f1ef198c
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87969019"
---
# <a name="plan-remote-access-with-otp-authentication"></a>OTP 認証を使用するリモート アクセスを計画する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

 Windows Server 2016 および Windows Server 2012 は、DirectAccess とルーティングとリモートアクセスサービス (RRAS) VPN を1つのリモートアクセスの役割に結合します。 この概要では、単一の Windows Server 2016 または Windows Server 2012 リモートアクセスマルチサイト展開を展開するために必要な構成手順の概要を説明します。


-  手順 1:[詳細設定を使用して単一の DirectAccess サーバーを展開](../../../directaccess/single-server-advanced/deploy-a-single-directaccess-server-with-advanced-settings.md)します。 この手順には、単一のサーバーを展開するために必要なインフラストラクチャの計画が含まれます。 これには、ネットワークとサーバーの設定、証明書の要件、DNS 設定、ネットワークロケーションサーバーの展開、DirectAccess 管理サーバー、Active Directory 設定、グループポリシーオブジェクト (Gpo) の計画が含まれます。

-   [手順 2: RADIUS サーバーの展開を計画する](Step-2-Plan-the-RADIUS-Server-Deployment.md)

-   [手順 3: OTP 証明書の展開を計画する](Step-3-Plan-OTP-Certificate-Deployment.md)

-   [手順 4: リモートアクセスサーバーで OTP を計画する](Step-4-Plan-for-OTP-on-the-Remote-Access-Server.md)

これらの計画手順を完了したら、「 [OTP 認証を使用したリモートアクセスの構成](../configure/configure-ra-with-otp-authentication.md)」を参照してください。 ラボ環境での概念実証としてマルチサイト展開を構成する方法については、「[テストラボガイド: OTP 認証と RSA SecurID を使用した DirectAccess のデモンストレーション](../../../directaccess/tlg-otp-securid/test-lab-guide-demonstrate-directaccess-with-otp-authentication-and-rsa-securid.md)」を参照してください。

