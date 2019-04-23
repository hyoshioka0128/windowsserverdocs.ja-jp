---
title: Windows Admin Center とは
description: Windows Admin Center (Project Honolulu) とは
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 76427cc6d86a3d61dcf2d66cdf47ded9ba9be848
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829043"
---
# <a name="what-is-windows-admin-center"></a>Windows Admin Center とは

>適用先:Windows Admin Center、Windows Admin Center プレビュー

Windows Admin Center は、Azure またはクラウドに依存せずに、Windows サーバーの管理を実現する、ローカルに展開されたブラウザー ベースの新しい管理ツール セットです。 Windows Admin Center では、サーバー インフラストラクチャのあらゆる側面を完全に管理できます。特に、インターネットに接続されていないプライベート ネットワークでのサーバーの管理に便利です。

Windows Admin Center は、サーバー マネージャーや MMC などの "インボックス" 管理ツールの進化形です。 System Center を補完する - 置換ではありません。

![](../media/wac-complements.png)

## <a name="how-does-windows-admin-center-work"></a>Windows Admin Center のしくみ

Windows Admin Center は、web ブラウザーで実行し、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows 10、およびによってを管理、 **Windows Admin Center ゲートウェイ**Windows Server または Windows 10 にインストールされます。 ゲートウェイは、リモート PowerShell と WMI over WinRM を介してサーバーを管理します。 ゲートウェイは、[ダウンロード](https://aka.ms/windowsadmincenter)可能な単一の軽量な .msi パッケージとして Windows Admin Center に含まれています。

Windows Admin Center ゲートウェイは、DNS に発行され、対応する企業ファイアウォールによってアクセス権が与えられると、Microsoft Edge または Google Chrome によってユーザーがどこからでもサーバーに安全に接続し、管理できるようにします。

![](../media/architecture.png)

## <a name="learn-how-windows-admin-center-improves-your-management-environment"></a>Windows Admin Center で管理環境が改善するしくみの詳細

### <a name="familiar-functionality"></a>**使い慣れた機能**

Windows Admin Center は、Microsoft 管理コンソール (MMC) など、現在システムが構築および管理される方法に合わせて一から構築された、従来から用いられてきたよく知られている管理プラットフォームの進化形です。 Windows Admin Center には、Windows サーバーおよびクライアントを管理するために現在使用している使い慣れた多くのツールが含まれています。

### <a name="easy-to-install-and-use"></a>**簡単にインストールして使用するには**

Windows 10 コンピューターに[インストール](../deploy/install.md)して数分で管理を開始するか、またはゲートウェイとして機能する Windows 2016 サーバーにインストールして、組織全体で Web ブラウザーからコンピューターを管理できるようにします。

### <a name="complements-existing-solutions"></a>**既存のソリューションを補完**

Windows Admin Center ソリューションと連携して System Center と Azure の管理およびセキュリティのように、詳細なを実行するには、その機能を追加する 1 台のコンピューターの管理タスク。

### <a name="manage-from-anywhere"></a>**どこからでも管理します。**

Windows Admin Center ゲートウェイ サーバーをパブリック インターネットに公開すると、安全な方法でどこからでもサーバーに接続して管理することができます。

### <a name="enhanced-security-for-your-management-platform"></a>**管理プラットフォームのセキュリティを強化**

Windows Admin Center には、管理プラットフォームを[より安全](../plan/user-access-options.md)にする多くの機能強化が含まれています。 役割ベースのアクセス制御によって、どの管理者がどの管理機能にアクセスできるかを微調整できます。 ゲートウェイの認証方オプションには、ローカル グループ、ローカル ドメイン ベースの Active Directory、およびクラウド ベースの Azure Active Directory が含まれます。  また、環境で実行された管理操作を[把握](../use/logging.md)できます。

### <a name="azure-integration"></a>**Azure との統合**

Windows Admin Center は、の多くの点を持つ[Azure サービスとの統合](../plan/azure-integration-options.md)、Azure Active Directory、Azure Backup を Azure Site Recovery など。

### <a name="manage-hyper-converged-clusters"></a>**ハイパー コンバージド クラスターを管理します。**

Windows Admin Center は、仮想化されたコンピューター、ストレージ、ネットワーク コンポーネントなど、[ハイパーコンバージド クラスターの管理](../use/manage-hyper-converged.md)のための最適なエクスペリエンスを提供します。

### <a name="extensibility"></a>**機能拡張**

Windows Admin Center は拡張機能を念頭に置いて一から構築され、Microsoft およびサード パーティーの開発者が現在提供されている製品に含まれないツールやソリューションを構築できる機能が用意されています。 Microsoft は、開発者が Windows Admin Center 向けの独自のツールを構築できるようにする [SDK](../extend/extensibility-overview.md) を提供します。

> [!Tip]
> Windows Admin Center をインストールする準備はできましたか。 [今すぐダウンロード](https://aka.ms/windowsadmincenter)
