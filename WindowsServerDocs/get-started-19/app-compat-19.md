---
title: Windows Server 2019 と Microsoft サーバー アプリケーションの互換性
description: Windows Server 2019 と Microsoft サーバー アプリケーションの互換性表
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2afe7c32-1fda-4441-989b-4115dabdcd34
author: coreyp
ms.author: coreyp-at-msft
manager: jasgroce
ms.localizationpriority: medium
ms.openlocfilehash: 8dcaff6ab8a296790158f59035bd4a5c1a093cbd
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2019
ms.locfileid: "66442371"
---
# <a name="windows-server-2019-and-microsoft-server-application-compatibility"></a>Windows Server 2019 と Microsoft サーバー アプリケーションの互換性

>適用先:Windows Server 2019

以下の表は、Window Server 2019 上でインストールと機能をサポートする Microsoft サーバー アプリケーションについてまとめたものです。 これはクイック リファレンスとして活用するための情報であり、個々の製品仕様、要件、アナウンス、または各サーバー アプリケーションの全般的な情報の代わりに使用することはできません。 各製品の互換性やオプションについて詳細を把握するには、公式のドキュメントを参照してください。

Windows Server と Microsoft 以外のアプリケーションとの互換性について詳細情報をお探しのソフトウェア ベンダー パートナー様である場合、[Commercial App Certification ポータル](https://commercialappcertification.microsoft.com/)にアクセスしてください。

| **製品**                                                  | **Server Core でサポートされる**             |   | **デスクトップ エクスペリエンス搭載サーバーでサポートされる** | **リリース済み?** |   | **製品の Web リンク**                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|--------------------------------------------------------------|------------------------------------------|---|-------------------------------------------------|---------------|---|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Exchange Server 2019                                         | 〇                                      |   | 〇                                             | 〇           |   | [Exchange Server のシステム要件](https://docs.microsoft.com/Exchange/plan-and-deploy/system-requirements?view=exchserver-2019)                                                                        |
| Host Integration Server 2016、CU3                            | 〇                                      |   | 〇                                             | 〇            |   | [Host Integration Server のシステム要件](https://docs.microsoft.com/host-integration-server/install-and-config-guides/system-requirements)                                                            |
| Visual Studio Team Foundation Server 2017                    | 〇\*                                    |   | 〇                                             | 〇           |   | [Team Foundation Server 2017](https://docs.microsoft.com/tfs/server/requirements?view=vsts)                                                                                                                |
| Visual Studio Team Foundation Server 2018                    | 〇\*                                    |   | 〇                                             | 〇           |   | [Team Foundation Server 2018](https://docs.microsoft.com/tfs/server/requirements?view=vsts)                                                                                                                  |
| Microsoft SQL Server 2014                                    | 〇\*                                    |   | 〇                                             | 〇           |   | [SQL Server 2014 のインストールに必要なハードウェアおよびソフトウェア](https://docs.microsoft.com/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-2014)   |
| Microsoft SQL Server 2016                                    | 〇\*                                    |   | 〇                                             | 〇           |   | [SQL Server 2016 のインストールに必要なハードウェアおよびソフトウェア](https://docs.microsoft.com/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-2016)   |
| Microsoft SQL Server 2017                                    | 〇\*                                    |   | 〇                                             | 〇           |   | [SQL Server 2017 のインストールに必要なハードウェアおよびソフトウェア](https://docs.microsoft.com/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-2017) |
| Microsoft System Center Configuration Manager (バージョン 1806) | 管理対象のクライアントとしては〇、サイト サーバーとしては X |   | 管理対象のクライアントとしては〇、サイト サーバーとしては X        | 〇           |   | [System Center Configuration Manager バージョン 1806 の新機能](https://docs.microsoft.com/sccm/core/plan-design/changes/whats-new-in-version-1806)                                                    |
| Microsoft System Center Operations Manager 2019              | 〇\*                                    |   | 〇                                             | 〇           |   | [System Center Operations Manager のシステム要件](https://docs.microsoft.com/system-center/scom/plan-system-requirements)                                                                                                      |
| Microsoft System Center Virtual Machine Manager 2019         | 〇\*                                    |   | 〇                                             | 〇           |   | [System Center Virtual Machine Manager のシステム要件](https://docs.microsoft.com/system-center/vmm/system-requirements)                                                                                                      |
| Microsoft System Center Data Protection Manager 2019         | X                                       |   | 〇                                             | 〇           |   | [System Center Data Protection Manager 向けの環境の準備](https://docs.microsoft.com/system-center/dpm/prepare-environment-for-dpm?view=sc-dpm-2019)                                                                                                      |
| SharePoint Server 2016                                       | X                                       |   | 〇                                             | 〇           |   | [SharePoint Server 2016 のハードウェア要件とソフトウェア要件](https://docs.microsoft.com/SharePoint/install/hardware-and-software-requirements)                                                                |
| SharePoint Server 2019                                       | X                                       |   | 〇                                             | 〇           |   | [SharePoint Server 2019 のハードウェア要件とソフトウェア要件](https://docs.microsoft.com/sharepoint/install/hardware-and-software-requirements-2019)                                                       |
| Project Server 2016                                          | X                                       |   | 〇                                             | 〇           |   | [Project Server 2016 のソフトウェア要件](https://docs.microsoft.com/project/software-requirements-for-project-server-2016)                                                                                |
| Project Server 2019                                          | X                                       |   | 〇                                             | 〇           |   | [Project Server 2019 のソフトウェア要件](https://docs.microsoft.com/project/software-requirements-for-project-server-2019)                                                                          |
| Skype for Business 2019                                      | X                                       |   | 〇                                             | 〇           |   | [Skype for Business Server の前提条件のインストール](https://docs.microsoft.com/skypeforbusiness/deploy/install/install-prerequisites)                                                                          |

\*制限があるか、[Server Core アプリ互換性オンデマンド機能 (FOD)](install-fod-19.md) が必要な場合があります。
特定の製品または FOD のドキュメントを参照してください。
