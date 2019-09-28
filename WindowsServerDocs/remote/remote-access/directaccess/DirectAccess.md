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
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4cc5ed275a6dc3cd235aa0ff1bfb0f0f46350a2b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71394511"
---
# <a name="directaccess"></a>DirectAccess

>適用先:Windows Server (半期チャネル)、Windows Server 2016

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
>Microsoft Azure では、仮想マシン \(VM @ no__t-1 にリモートアクセスを展開しないでください。 Microsoft Azure でのリモートアクセスの使用はサポートされていません。 Windows Server 2016 以前のバージョンの Windows Server では、Azure VM でリモートアクセスを使用して VPN、DirectAccess、またはその他のリモートアクセス機能を展開することはできません。 詳細については、「 [Microsoft Azure の仮想マシンに対する Microsoft サーバーソフトウェアのサポート](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines)」を参照してください。
  
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
