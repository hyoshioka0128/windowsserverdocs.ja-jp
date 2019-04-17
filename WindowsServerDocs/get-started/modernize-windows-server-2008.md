---
title: Windows Server 2008 と Windows Server 2008 R2 のアップグレード
description: Windows Server 2008 と Windows Server 2008 R2 は、サービス終了が近づいています。 オンプレミスのアップグレードまたは Azure への再ホストの方法について説明します。
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: mikeblodge
ms.author: mikeblodge
ms.date: 07/12/2018
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.localizationpriority: high
ms.openlocfilehash: 4127eab613abb429a200f513a11b944e05da0f76
ms.sourcegitcommit: 9ed4c9fe04ebf3ef488170503c9a354c992b6fde
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/03/2018
ms.locfileid: "4339370"
---
# Windows Server 2008 と Windows Server 2008 R2 のアップグレード

Windows Server 2008 と Windows Server 2008 R2 の延長サポートは、2020 年 1 月 14 日に終了します。 オンプレミスのアップグレード、または Azure での再ホストによる移行の 2 つの現代化パスが利用可能です。 **Azure で再ホストする場合は、無料で既存のサーバー イメージを移行できます。**

![Windows Server 2008 からのアップグレード パスを説明するフローチャート](media/WS08_upgrade_paths.png)


## オンプレミスのアップグレード
オンプレミスにサーバーを保持する必要があり、Windows Server 2008 または Windows Server 2008 R2 を実行している場合は、[Windows Server 2012/2012 R2 にアップグレード](installation-and-upgrade.md#upgrading-to-windows-server-2012-r2)してから [Windows Server 2016 にアップグレードする](installation-and-upgrade.md#upgrading-to-windows-server-2016)必要があります。 アップグレード時に、再ホストにより Azure に移行するオプションもあります。

オンプレミスのアップグレード オプションについて詳しくは、「[Upgrading from Windows Server 2008 R2 or Windows Server 2008 (Windows Server 2008 R2 または Windows Server 2008 からのアップグレード)](installation-and-upgrade.md#upgrading-from-windows-server-2008-r2-or-windows-server-2008)」をご覧ください。

Windows Server 2003 を実行している場合は、[Windows Server 2008 にアップグレードする](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff972408(v%3dws.10))必要があります。 オンプレミスのアップグレード オプションについて詳しくは、「[upgrade paths for Windows Server 2008 (Windows Server 2008 のアップグレード パス)](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd979563(v=ws.10))」をご覧ください。


## Azure への移行
オンプレミスの Windows Server 2008 および Windows Server 2008 R2 サーバーを Azure に移行し、そこで仮想マシンでサーバーを実行し続けることができます。 Azure で準拠した状態が維持され、セキュリティが強化され、業務にクラウド イノベーションが追加されます。 Azure への移行の利点は次のとおりです。

- Azure でのセキュリティ更新プログラム。
- さらに 3 年分の Windows Server 2008 R2 または 2008 の重要なセキュリティ更新プログラムが追加料金なしで利用できます。 
- Azure での無償アップグレード。
- 準備ができた時点で、その他のクラウド サービスを導入します。
- SQL Server を Azure 管理インスタンスまたは VM に移行することで、さらに 3 年分の Windows Server 2008 R2 または 2008 の重要なセキュリティ更新プログラムが追加料金なしで利用できます。 
- Azure に固有のクラウド削減のために既存の SQL Server および Windows Server のライセンスを利用できます。

<a href="uploading-specialized-WS08-image-to-azure.md"><img src="media/WS08-image-banner-small.png"></a>

移行を開始するには、「[Windows Server 2008/2008 R2 に特化されたイメージの Azure へのアップロード](uploading-specialized-WS08-image-to-azure.md)」をご覧ください。

既存の IT リソースの分析方法について理解し、所有しているものを評価して、特定のサーバーやアプリケーションをクラウドに移行する利点、またはワークロードをオンプレミスに保持して最新バージョンの Windows Server にアップグレードする利点を特定するには、「[Migration Guide for Windows Server (Windows Server の移行ガイド)](https://go.microsoft.com/fwlink/?linkid=872689)」をご覧ください。


## Windows サーバーと並行した SQL Server 2008/2008 R2 のアップグレード

![SQL Server のロゴ](media/sqlr2.jpg)

SQL Server 2008/2008 R2 を実行している場合は、SQL Server [2016](https://docs.microsoft.com/sql/sql-server/sql-server-technical-documentation?view=sql-server-2016) または [2017](https://docs.microsoft.com/sql/sql-server/sql-server-technical-documentation?view=sql-server-2017) にアップグレードすることができます。


## その他のリソース
[Microsoft Azure](https://docs.microsoft.com/azure/#pivot=products)