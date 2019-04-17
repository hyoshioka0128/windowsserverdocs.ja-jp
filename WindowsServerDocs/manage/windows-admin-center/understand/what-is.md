---
title: Windows Admin Center とは
description: Windows Admin Center (Project Honolulu) とは
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: d374704768d06aaeb7ee6bc9c984cc78d49cb4b0
ms.sourcegitcommit: be0144eb59daf3269bebea93cb1c467d67e2d2f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2018
ms.locfileid: "4080909"
---
# Windows Admin Center とは

>適用対象: Windows Admin Center、Windows Admin Center Preview

Windows Admin Center は、Azure またはクラウドに依存せずに、Windows サーバーの管理を実現する、ローカルに展開されたブラウザー ベースの新しい管理ツール セットです。 Windows Admin Center では、サーバー インフラストラクチャのあらゆる側面を完全に管理できます。特に、インターネットに接続されていないプライベート ネットワークでのサーバーの管理に便利です。

Windows Admin Center は、サーバー マネージャーや MMC などの "インボックス" 管理ツールの進化形です。 System Center を補完 - 代替機能ではありません。

![](../media/wac-complements.png)

## Windows Admin Center のしくみ

Windows Admin Center は Web ブラウザーで実行され、Windows Server 2016 または Windows 10 にインストールされた **Windows Admin Center ゲートウェイ**を介して Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows 10 などを管理します。 ゲートウェイは、リモート PowerShell と WMI over WinRM を介してサーバーを管理します。 ゲートウェイは、[ダウンロード](https://aka.ms/windowsadmincenter)可能な単一の軽量な .msi パッケージとして Windows Admin Center に含まれています。

Windows Admin Center ゲートウェイは、DNS に発行され、対応する企業ファイアウォールによってアクセス権が与えられると、Microsoft Edge または Google Chrome によってユーザーがどこからでもサーバーに安全に接続し、管理できるようにします。

![](../media/architecture.png)

## Windows Admin Center で管理環境が改善するしくみの詳細

### **使い慣れた機能**

Windows Admin Center は、Microsoft 管理コンソール (MMC) など、現在システムが構築および管理される方法に合わせて一から構築された、従来から用いられてきたよく知られている管理プラットフォームの進化形です。 Windows Admin Center には、Windows サーバーおよびクライアントを管理するために現在使用している使い慣れた多くのツールが含まれています。

### **簡単なインストールと使用**

Windows 10 コンピューターに[インストール](../deploy/install.md)して数分で管理を開始するか、またはゲートウェイとして機能する Windows 2016 サーバーにインストールして、組織全体で Web ブラウザーからコンピューターを管理できるようにします。

### **既存のソリューションを補完** 

Windows Admin Center 連携するように System Center および Azure の管理およびセキュリティ ソリューション詳細を実行するには、その機能を追加する単一コンピューターの管理タスク。

### **どこからでもを管理**

Windows Admin Center ゲートウェイ サーバーをパブリック インターネットに公開すると、安全な方法でどこからでもサーバーに接続して管理することができます。

### **管理プラットフォームのセキュリティを強化**

Windows Admin Center には、管理プラットフォームを[より安全](../plan/user-access-options.md)にする多くの機能強化が含まれています。 役割ベースのアクセス制御によって、どの管理者がどの管理機能にアクセスできるかを微調整できます。 ゲートウェイの認証方オプションには、ローカル グループ、ローカル ドメイン ベースの Active Directory、およびクラウド ベースの Azure Active Directory が含まれます。  また、環境で実行された管理操作を[把握](../use/logging.md)できます。

### **Azure の統合**

Windows Admin Center では、 [Azure サービスとの統合](../plan/azure-integration-options.md)、Azure Active Directory、Azure Backup、Azure Site Recovery などの多くの点があります。

### **ハイパーコンバージド クラスターの管理**

Windows Admin Center は、仮想化されたコンピューター、ストレージ、ネットワーク コンポーネントなど、[ハイパーコンバージド クラスターの管理](../use/manage-hyper-converged.md)のための最適なエクスペリエンスを提供します。

### **拡張性**

Windows Admin Center は拡張機能を念頭に置いて一から構築され、Microsoft およびサード パーティーの開発者が現在提供されている製品に含まれないツールやソリューションを構築できる機能が用意されています。 Microsoft は、開発者が Windows Admin Center 向けの独自のツールを構築できるようにする [SDK](../extend/extensibility-overview.md) を提供します。

> [!Tip]
> Windows Admin Center をインストールする準備はできましたか。 [今すぐダウンロード](https://aka.ms/windowsadmincenter)
