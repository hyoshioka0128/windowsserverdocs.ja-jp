---
title: マルチサイト展開を構成する
description: このトピックは、「Windows Server 2016 のマルチサイト展開に複数のリモートアクセスサーバーを展開する」の一部です。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: cb84920e-7cf5-4266-b071-d09e3d5e1f10
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 2c2d044c02673d74d7aa8ec076aeac7e2f1aebdb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858385"
---
# <a name="configure-a-multisite-deployment"></a>マルチサイト展開を構成する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

 Windows Server 2016 では、DirectAccess とリモートアクセスサービス (RAS) VPN が1つのリモートアクセスの役割に統合されています。 この概要では、単一の Windows Server 2016 または Windows Server 2012 リモートアクセスマルチサイト展開を展開するために必要な構成手順の概要を説明します。  
  
-   手順 1:[詳細設定を使用して単一の DirectAccess サーバーを展開](https://technet.microsoft.com/windows-server-docs/networking/remote-access/directaccess/single-server-advanced/deploy-a-single-directaccess-server-with-advanced-settings)します。 単一のリモートアクセスサーバーをインストールして構成します。 マルチサイト展開では、マルチサイト展開を構成する前に、単一のサーバーをインストールする必要があります。  
  
-   [手順 2: マルチサイトインフラストラクチャを構成](Step-2-Configure-the-Multisite-Infrastructure.md)します。 マルチサイト展開の場合は、追加の Active Directory サイトおよびドメインコントローラーを構成する必要があります。 自動的に構成された Gpo を使用していない場合は、追加のセキュリティグループとグループポリシーオブジェクト (Gpo) も必要です。  
  
-   [手順 3: マルチサイト展開を構成する](Step-3-Configure-the-Multisite-Deployment.md)-追加のリモートアクセスサーバーにリモートアクセスの役割をインストールし、マルチサイト展開を有効にして、追加のサーバーを展開のエントリポイントとして構成します。  
  
-   [手順 4: マルチサイト展開を確認する](Step-4-Verify-the-Multisite-Deployment.md) 
  


