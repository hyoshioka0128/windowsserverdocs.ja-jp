---
title: Windows Server 2019 および Microsoft サーバー アプリケーションの互換性
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
ms.openlocfilehash: 7b62f0951ab8d7ed54448eb86f457f9a689da9cb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858513"
---
# <a name="windows-server-2019-and-microsoft-server-application-compatibility"></a>Windows Server 2019 および Microsoft サーバー アプリケーションの互換性

>適用先:Windows Server 2019

このテーブルには、ウィンドウのサーバー 2019 のインストールと機能をサポートする Microsoft サーバー アプリケーションが一覧表示します。 これはクイック リファレンスとして活用するための情報であり、個々の製品仕様、要件、アナウンス、または各サーバー アプリケーションの全般的な情報の代わりに使用することはできません。 各製品の互換性やオプションについて詳細を把握するには、公式のドキュメントを参照してください。

Windows Server と Microsoft 以外のアプリケーションの互換性の詳細情報を探して、ソフトウェア ベンダー パートナーがいる場合は、[商用アプリ認定ポータル](https://commercialappcertification.microsoft.com/)します。
| **Product**                                                  | **Server Core でサポートされています**             |   | **デスクトップ エクスペリエンス搭載サーバーでサポートされています** | **リリースか。** |   | **製品の Web リンク**                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|--------------------------------------------------------------|------------------------------------------|---|-------------------------------------------------|---------------|---|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Exchange Server 2019                                         | 〇                                      |   | 〇                                             | 〇            |   | [Exchange Server のシステム要件](https://docs.microsoft.com/Exchange/plan-and-deploy/system-requirements?view=exchserver-2019)                                                                        |
| Host Integration Server 2016 CU3                            | 〇                                      |   | 〇                                             | X            |   | [ホスト サーバーの統合システムの要件](https://docs.microsoft.com/host-integration-server/install-and-config-guides/system-requirements)                                                            |
| Visual Studio Team Foundation Server 2017                    | うん\*                                    |   | 〇                                             | 〇           |   | [Team Foundation Server 2017](https://docs.microsoft.com/tfs/server/requirements?view=vsts)                                                                                                                |
| Visual Studio Team Foundation Server 2018                    | うん\*                                    |   | 〇                                             | 〇           |   | [Team Foundation Server 2018](https://docs.microsoft.com/tfs/server/requirements?view=vsts)                                                                                                                  |
| Microsoft SQL Server 2014                                    | うん\*                                    |   | 〇                                             | 〇           |   | [SQL Server 2014 のインストールに必要なハードウェアおよびソフトウェア](https://docs.microsoft.com/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-2014)   |
| Microsoft SQL Server 2016                                    | うん\*                                    |   | 〇                                             | 〇           |   | [Hardware and Software Requirements for Installing SQL Server 2016](https://docs.microsoft.com/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-2016)   |
| Microsoft SQL Server 2017                                    | うん\*                                    |   | 〇                                             | 〇           |   | [Hardware and Software Requirements for Installing SQL Server 2017](https://docs.microsoft.com/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-2017) |
| Microsoft System Center Configuration Manager (バージョン 1806) | サイト サーバーとではなく、管理されたクライアントとして ○ します。 |   | サイト サーバーとではなく、管理されたクライアントとして ○ します。        | 〇           |   | [バージョン 1806 System Center Configuration Manager の新機能については](https://docs.microsoft.com/sccm/core/plan-design/changes/whats-new-in-version-1806)                                                    |
| Microsoft System Center Operations Manager 2019              | うん\*                                    |   | 〇                                             | いいえ            |   | [System Center Operations Manager のシステム要件](https://docs.microsoft.com/system-center/scom/plan-system-requirements)                                                                                                      |
| Microsoft System Center Virtual Machine Manager 2019         | うん\*                                    |   | 〇                                             | いいえ            |   | [System Center Virtual Machine Manager 用のシステム要件](https://docs.microsoft.com/system-center/vmm/system-requirements)                                                                                                      |
| Microsoft System Center Data Protection Manager 2019         | X                                       |   | 〇                                             | いいえ            |   | [System Center のリリースのオプションの概要](https://docs.microsoft.com/system-center/ltsc-and-sac-overview)                                                                                                      |
| SharePoint Server 2016                                       | いいえ                                       |   | 〇                                             | 〇           |   | [SharePoint Server 2016 のハードウェアおよびソフトウェアの要件](https://docs.microsoft.com/SharePoint/install/hardware-and-software-requirements)                                                                |
| SharePoint Server 2019                                       | いいえ                                       |   | 〇                                             | 〇            |   | [SharePoint Server 2019 ハードウェアとソフトウェアの要件](https://docs.microsoft.com/sharepoint/install/hardware-and-software-requirements-2019)                                                       |
| Project Server 2016                                          | X                                       |   | 〇                                             | 〇           |   | [Project Server 2016 のソフトウェア要件](https://docs.microsoft.com/project/software-requirements-for-project-server-2016)                                                                                |
| Project Server 2019                                          | X                                       |   | 〇                                             | 〇           |   | [Project Server 2019 のソフトウェア要件](https://docs.microsoft.com/project/software-requirements-for-project-server-2019)                                                                          |
| Skype for Business 2019                                      | いいえ                                       |   | 〇                                             | 〇           |   | [Business Server 用の Skype の前提条件をインストールします。](https://docs.microsoft.com/skypeforbusiness/deploy/install/install-prerequisites)                                                                          |

\*制限事項があります。 または、必要があります、 [Server Core アプリの互換性機能の需要 (FOD)。 ](install-fod-19.md)
特定の製品または FOD ドキュメントを参照してください。
