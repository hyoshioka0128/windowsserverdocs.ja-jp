---
title: Windows Server 2016 リモート デスクトップ サービスへようこそ
description: リモート デスクトップ サービスの概要を説明します
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: chrimo
ms.date: 02/22/2017
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 52b9e09f-39e0-41a9-9d3b-4d5f4eacf3e0
author: christianmontoya
manager: scottman
ms.localizationpriority: medium
ms.openlocfilehash: 3d148c99911be0cebfc29429d93241f24c2b9606
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2019
ms.locfileid: "66453008"
---
# <a name="welcome-to-remote-desktop-services"></a>リモート デスクトップ サービスへようこそ 

リモート デスクトップ サービス (RDS) は、たとえば個別に仮想化されたアプリケーションを提供する、セキュリティで保護されたモバイル/リモート デスクトップ アクセスを提供する、エンドユーザーがクラウドからアプリケーションやデスクトップを実行できるようにするなど、個々のエンド カスタマーのニーズに合わせた仮想化ソリューションを構築するのに最適なプラットフォームです。

![リモート デスクトップ サービスの概要](./media/rds-overview.png)

RDS では、Windows Server 2016 (オンプレミス展開の場)、Microsoft Azure (クラウド展開の場合)、信頼性の高い多数のパートナー ソリューションなど、さまざまな展開オプションを通して、展開の柔軟性、コスト効率性、および拡張性のすべてが提供されます。

お客様の環境や構成に応じて、RDS ソリューションをセッション ベースの仮想化または仮想デスクトップ インフラストラクチャ (VDI) として、または 2 つの組み合わせとして設定できます。

- **セッション ベースの仮想化**:Windows Server のコンピューティング能力を活用し、ユーザーの日常業務を効率化するコスト効率に優れたマルチ セッション環境を提供します。
- **VDI**:Windows クライアントを活用し、高パフォーマンス、アプリの互換性、ユーザーが Windows デスクトップ エクスペリエンスに期待する操作性を提供します。

これらの仮想化環境内では、ユーザーに発行するものをより柔軟に制御できます。

- **デスクトップ**:お客様がインストールおよび管理するさまざまなアプリケーションを使用して、ユーザーに完全なデスクトップ エクスペリエンスを提供します。 これらのコンピューターをプライマリ ワークステーションとして利用するユーザーや、シン クライアントのユーザーに最適です (MultiPoint Services の使用など)。
- **RemoteApps**:ユーザーのデスクトップ上で実行するローカル アプリケーションのように見える、仮想マシン上でホスト/実行する個々のアプリケーションを指定します。 アプリには独自のタスク バー エントリがあり、サイズの変更やモニター間での移動ができます。 主要なアプリケーションをセキュリティで保護されたリモート環境に展開し、ユーザーが自分のデスクトップから作業したり、カスタマイズしたりできるようにする場合に最適です。

費用対効果が非常に重要であり、セッション ベースの仮想化環境に完全なデスクトップを展開する利点を幅広く活用したい場合は、[MultiPoint Services](../multipoint-services/multipoint-services.md) を使用することによって最も高い価値を提供できます。 

これらのオプションと構成により、お客様はユーザーに必要なデスクトップとアプリケーションを、リモート、安全、かつ費用対効果の高い方法で柔軟に展開することができます。

## <a name="next-steps"></a>次のステップ

RDS の理解を深め、さらには自身の環境の展開を開始するのに役立つ手順を次に示します。
-   Windows と Windows Server のさまざまなバージョンで[サポートされる RDS の構成](rds-supported-config.md)について理解する。
-   高可用性や多要素認証などのさまざまな要件に対応する RDS 環境を[計画および設計](rds-plan-and-design.md)する。
-   目的の環境に最適な[リモート デスクトップ サービスのアーキテクチャ モデル](desktop-hosting-logical-architecture.md)を確認する。
-   [ARM と Azure Marketplace を使用して RDS 環境の展開](rds-in-azure.md)を開始する。
