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
ms.openlocfilehash: e8bb8cda003ca151216e3b86d5884dfd05e73e6d
ms.sourcegitcommit: 5d55c3ebd1ceee7229ea9a9989c69cf93757ed88
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2019
ms.locfileid: "9256945"
---
# Windows Server 2019 と Microsoft サーバー アプリケーションの互換性

>適用対象: Windows Server 2019

次の表では、Window Server 2019 のインストールと機能をサポートする Microsoft サーバー アプリケーションを示します。 これはクイック リファレンスとして活用するための情報であり、個々の製品仕様、要件、アナウンス、または各サーバー アプリケーションの全般的な情報の代わりに使用することはできません。 各製品の互換性やオプションについて詳細を把握するには、公式のドキュメントを参照してください。

探している Microsoft 以外のアプリケーションと Windows Server の互換性について詳しくは、ソフトウェア ベンダー パートナーは、[市販のアプリの認定ポータル](https://commercialappcertification.microsoft.com/)にアクセスしてください。
| **製品**                                                  | **Server Core でサポートされています。**             |   | **デスクトップ エクスペリエンス搭載サーバーでサポートされています。** | **リリース済み?** |   | **製品の Web リンク**                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|--------------------------------------------------------------|------------------------------------------|---|-------------------------------------------------|---------------|---|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Exchange Server 2019                                         | 要                                      |   | 要                                             | 要           |   | [Exchange サーバーのシステム要件](https://docs.microsoft.com/Exchange/plan-and-deploy/system-requirements?view=exchserver-2019)                                                                        |
| Host Integration Server 2016 CU3                            | 要                                      |   | 可                                             | いいえ            |   | [ホスト Integration Server システム要件](https://docs.microsoft.com/host-integration-server/install-and-config-guides/system-requirements)                                                            |
| Visual Studio Team Foundation Server 2017                    | Yes\ *                                    |   | 要                                             | はい           |   | [Team Foundation Server 2017](https://docs.microsoft.com/tfs/server/requirements?view=vsts)                                                                                                                |
| Visual Studio Team Foundation Server 2018                    | Yes\ *                                    |   | 要                                             | 要           |   | [Team Foundation Server 2018](https://docs.microsoft.com/tfs/server/requirements?view=vsts)                                                                                                                  |
| Microsoft SQL Server 2014                                    | Yes\ *                                    |   | 要                                             | 要           |   | [SQL Server 2014 のインストールに必要なハードウェアおよびソフトウェア](https://docs.microsoft.com/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-2014)   |
| Microsoft SQL Server 2016                                    | Yes\ *                                    |   | 要                                             | 要           |   | [ハードウェアおよび SQL Server 2016 をインストールするためのソフトウェア要件](https://docs.microsoft.com/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-2016)   |
| Microsoft SQL Server 2017                                    | Yes\ *                                    |   | 要                                             | 要           |   | [ハードウェアおよび SQL Server 2017 をインストールするためのソフトウェア要件](https://docs.microsoft.com/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-2017) |
| Microsoft System Center Configuration Manager (バージョン 1806) | サイト サーバーとしていいえ、管理されたクライアントとして [はい] します。 |   | サイト サーバーとしていいえ、管理されたクライアントとして [はい] します。        | はい           |   | [System Center Configuration Manager のバージョン 1806 の新機能](https://docs.microsoft.com/sccm/core/plan-design/changes/whats-new-in-version-1806)                                                    |
| Microsoft System Center Operations Manager 2019              | Yes\ *                                    |   | 要                                             | 要           |   | [System Center Operations Manager のシステム要件](https://docs.microsoft.com/system-center/scom/plan-system-requirements)                                                                                                      |
| Microsoft System Center Virtual Machine Manager 2019         | Yes\ *                                    |   | 要                                             | 要           |   | [System Center の仮想マシン マネージャーのシステム要件](https://docs.microsoft.com/system-center/vmm/system-requirements)                                                                                                      |
| Microsoft System Center Data Protection Manager 2019         | いいえ                                       |   | ○                                             | 要           |   | [System Center Data Protection Manager の環境を準備します。](https://docs.microsoft.com/system-center/dpm/prepare-environment-for-dpm?view=sc-dpm-2019)                                                                                                      |
| SharePoint Server 2016                                       | いいえ                                       |   | ○                                             | 要           |   | [SharePoint Server 2016 のハードウェア要件とソフトウェア要件](https://docs.microsoft.com/SharePoint/install/hardware-and-software-requirements)                                                                |
| SharePoint Server 2019                                       | いいえ                                       |   | ○                                             | 要           |   | [SharePoint Server 2019 のハードウェアおよびソフトウェア要件](https://docs.microsoft.com/sharepoint/install/hardware-and-software-requirements-2019)                                                       |
| Project Server 2016                                          | いいえ                                       |   | ○                                             | 要           |   | [Project Server 2016 のソフトウェア要件](https://docs.microsoft.com/project/software-requirements-for-project-server-2016)                                                                                |
| Project Server 2019                                          | いいえ                                       |   | ○                                             | 要           |   | [プロジェクト Server 2019 のソフトウェア要件](https://docs.microsoft.com/project/software-requirements-for-project-server-2019)                                                                          |
| Skype for Business 2019                                      | いいえ                                       |   | ○                                             | 要           |   | [For Business Server Skype の前提条件をインストールします。](https://docs.microsoft.com/skypeforbusiness/deploy/install/install-prerequisites)                                                                          |

\*May の制限事項があるまたは必要があります、[サーバー コア アプリ互換性機能オンデマンド (FOD) で ](install-fod-19.md)。
特定の製品または FOD ドキュメントを参照してください。
