---
title: DirectAccess
description: このトピックでは、Windows Server 2016 の DirectAccess の簡単な概要について説明します。
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6b71d18e-1939-4fc0-bb42-29e0e5ffc8da
ms.author: lizross
author: eross-msft
ms.openlocfilehash: d07e4ab62c7362d8d58f68380d8d9abb8e7a7f2c
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80310825"
---
# <a name="directaccess"></a>DirectAccess

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、directaccess の簡単な概要について説明します。これには、directaccess をサポートするサーバーとクライアントのオペレーティングシステム、および Windows Server 2016 用の追加の DirectAccess ドキュメントへのリンクも含まれます。  
  
> [!NOTE]  
> このトピックに加えて、次の DirectAccess ドキュメントも参照できます。  
>   
> -   [Windows Server の DirectAccess 展開パス](DirectAccess-Deployment-Paths-in-Windows-Server.md)  
> -   [DirectAccess の展開の前提条件](Prerequisites-for-Deploying-DirectAccess.md)  
> -   [DirectAccess のサポートされない構成](DirectAccess-Unsupported-Configurations.md)  
> -   [DirectAccess のテスト ラボ ガイド](DirectAccess-Test-Lab-Guides.md)  
> -   [DirectAccess の既知の問題](DirectAccess-Known-Issues.md)  
> -   [DirectAccess のキャパシティ プランニング](DirectAccess-Capacity-Planning.md) 
> -   [DirectAccess オフラインドメイン参加](DirectAccess-Offline-Domain-Join.md)  
> -   [DirectAccess のトラブルシューティング](Troubleshooting-DirectAccess.md)  
> -   [はじめにウィザードを使用して単一の DirectAccess サーバーを展開する](single-server-wizard/Deploy-a-Single-DirectAccess-Server-Using-the-Getting-Started-Wizard.md)  
> -   [詳細設定を使用して単一の DirectAccess サーバーを展開する](single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)  
> -   [既存のリモート アクセス (VPN) 展開に DirectAccess を追加する](add-to-existing-vpn/Add-DirectAccess-to-an-Existing-Remote-Access-VPN-Deployment.md)  
  
DirectAccess を使用すると、従来の仮想プライベートネットワーク (VPN) 接続を必要とすることなく、組織のネットワークリソースへのリモートユーザーの接続が可能になります。 DirectAccess 接続では、リモートクライアントコンピューターは常に組織に接続されます。リモートユーザーが VPN 接続で必要とされる接続を開始および停止する必要はありません。 さらに、IT 管理者は、を実行していてインターネットに接続しているときに、DirectAccess クライアントコンピューターを管理できます。

>[!IMPORTANT]
>Microsoft Azure では、仮想マシン \(VM\) にリモートアクセスをデプロイしないでください。 Microsoft Azure でのリモートアクセスの使用はサポートされていません。 Windows Server 2016 以前のバージョンの Windows Server では、Azure VM でリモートアクセスを使用して VPN、DirectAccess、またはその他のリモートアクセス機能を展開することはできません。 詳細については、「 [Microsoft Azure の仮想マシンに対する Microsoft サーバーソフトウェアのサポート](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines)」を参照してください。
  
DirectAccess では、DirectAccess のオペレーティングシステムのサポートを含むドメインに参加しているクライアントのみがサポートされます。  
  
次のサーバーオペレーティングシステムでは、DirectAccess がサポートされています。  
  
-   すべてのバージョンの Windows Server 2016 を DirectAccess クライアントまたは DirectAccess サーバーとして展開できます。  
  
-   すべてのバージョンの Windows Server 2012 R2 を DirectAccess クライアントまたは DirectAccess サーバーとして展開できます。  
  
-   すべてのバージョンの Windows Server 2012 を DirectAccess クライアントまたは DirectAccess サーバーとして展開できます。  
  
-   すべてのバージョンの Windows Server 2008 R2 を DirectAccess クライアントまたは DirectAccess サーバーとして展開できます。  
  
次のクライアントオペレーティングシステムでは、DirectAccess がサポートされています。  
  
-   Windows 10 Enterprise  
  
-   Windows 10 Enterprise 2015 Long Term Servicing Branch (LTSB)  
  
-   Windows 8 および 8.1 Enterprise  
  
-   Windows 7 Ultimate  
  
-   Windows 7 Enterprise
