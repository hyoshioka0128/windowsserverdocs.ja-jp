---
title: Windows Server Update Services を展開する
description: Windows Server Update Service (WSUS) のトピックで、それを達成する 4 つの手順へのリンクを展開プロセスの概要
ms.prod: windows-server-threshold
ms.reviewer: na
ms.technology: manage-wsus
ms.topic: get-started-article
ms.assetid: 2708f6b2-4252-4b8f-9b7e-84c9b4222075
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 51972ad352f6530c8ee2aa84aec57b62784da728
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873183"
---
# <a name="deploy-windows-server-update-services"></a>Windows Server Update Services を展開する

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows Server Update Services (WSUS) を使用すると、IT 管理者は Microsoft 製品の最新の更新プログラムを展開できます。 WSUS は Windows Server のサーバーの役割の 1 つで、更新プログラムを管理および配布するためにインストールできます。 1 台の WSUS サーバーを、組織内にある他の WSUS サーバー用の更新プログラムの供給元として運用できます。 更新プログラムの供給元として機能する WSUS サーバーは、"アップストリーム サーバー" と呼ばれます。  

WSUS 実装では、利用可能な更新プログラムの情報を入手するために、ネットワーク内にある WSUS サーバーのうち少なくとも 1 台を Microsoft Update に接続する必要があります。 指定できますネットワークのセキュリティと構成に基づき、その他の何台のサーバーに直接接続 Microsoft Update。  

このガイドでは、計画と展開 Windows Server Update Service の概念について説明します。  

-   [WSUS 展開を計画します。](../plan/plan-your-wsus-deployment.md)  

-   [ステップ 1: WSUS サーバーの役割をインストールします。](1-install-the-wsus-server-role.md)  

-   [手順 2:WSUS を構成します。](2-configure-wsus.md)  

-   [手順 3:承認および展開する WSUS で更新プログラム](3-approve-and-deploy-updates-in-wsus.md)  

-   [手順 4:自動更新のグループ ポリシー設定を構成します。](4-configure-group-policy-settings-for-automatic-updates.md)  
