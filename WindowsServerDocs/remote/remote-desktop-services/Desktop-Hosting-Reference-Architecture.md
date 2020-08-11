---
title: デスクトップ ホスティングの参照アーキテクチャ
description: RDS および Azure でデスクトップ ホスティング ソリューションを作成するためのアーキテクチャに関するガイダンス。
ms.author: elizapo
ms.date: 11/02/2016
ms.topic: article
ms.assetid: 1bac5dd3-8430-46ee-8bef-10cc4b7cc437
author: lizap
manager: dongill
ms.openlocfilehash: 7cd57a6df788ab1730332522b3682feeb398fb60
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87989734"
---
# <a name="desktop-hosting-reference-architecture"></a>デスクトップ ホスティングの参照アーキテクチャ

>適用先:Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016

この記事では、リモート デスクトップ サービス (RDS) と Microsoft Azure 仮想マシンを使用してマルチテナント型かつホステッド型の Windows デスクトップおよびアプリケーションのサービス ("デスクトップ ホスティング" と呼ぶ) を作成するための一連のアーキテクチャ ブロックを定義します。 このアーキテクチャの参照を使用して、ユーザー数が 5 人から 5000 人の小規模から中規模の組織を対象とする、高い安全性、拡張性、信頼性を持つデスクトップ ホスティング ソリューションを作成できます。

この参照アーキテクチャの第一の対象者は、Microsoft Azure インフラストラクチャ サービスを活用し、[マイクロソフトのサービス プロバイダー ライセンス アグリーメント (SPLA)](https://www.microsoft.com/hosting/en/us/licensing/splabenefits.aspx) プログラムによって複数のテナントにデスクトップ ホスティング サービスやサブスクライバー アクセス ライセンス (SAL) を提供することを予定しているホスティング プロバイダーです。 この参照アーキテクチャの第二の対象者は、[ソフトウェア アシュアランス (SA) による RDS ユーザー CAL の拡張された権利](https://download.microsoft.com/download/6/B/A/6BA3215A-C8B5-4AD1-AA8E-6C93606A4CFB/Windows_Server_2012_R2_Remote_Desktop_Services_Licensing_Datasheet.pdf)を使用して、自社の従業員を対象に Microsoft Azure インフラストラクチャ サービスでデスクトップ ホスティング ソリューションを作成および管理することを予定しているエンド カスタマーです。

デスクトップ ホスティング ソリューションを提供する場合、ホスティング パートナーと SA のお客様は Windows Server を活用して、ビジネス ユーザーやコンシューマーになじみの深いアプリケーション エクスペリエンスを Windows ユーザーに提供します。 Windows 10 を基盤として構築された Windows Server 2016 は、使い慣れたアプリケーション サポートとユーザー エクスペリエンスを提供します。

このドキュメントの範囲は以下に限定されます。

* デスクトップ ホスティング サービスのアーキテクチャ設計のガイダンス。 展開手順、パフォーマンス、キャパシティ プランニングなどの詳細情報は、別のドキュメントで説明されています。 Azure インフラストラクチャ サービスの一般情報については、[Microsoft Azure の仮想マシン](https://azure.microsoft.com/documentation/services/virtual-machines/)に関するページをご覧ください。

* Windows Server 2016 リモート デスクトップ セッション ホスト (RD セッション ホスト) を使用するセッション ベースのデスクトップ、RemoteApp アプリケーション、およびサーバー ベースの個人用デスクトップ。 Windows クライアント オペレーティング システム用のサービス プロバイダー ライセンス アグリーメント (SPLA) がないため、Windows クライアント ベースの仮想デスクトップ インフラストラクチャは対象ではありません。 Windows Server ベースの仮想デスクトップ インフラストラクチャは、SPLA の下で許可され、Windows クライアント ベースの仮想デスクトップ インフラストラクチャは、特定のシナリオにおいてエンド カスタマー ライセンスを使用する専用ハードウェアで許可されます。 ただし、クライアント ベースのデスクトップ インフラストラクチャは、このドキュメントの範囲外になります。

* Microsoft の製品と機能、主に Windows Server 2016 と Microsoft Azure インフラストラクチャ サービス。

* ユーザー数が 5 人から 5000 人の規模のテナント向けデスクトップ ホスティング サービス。   規模の大きいテナントの場合は、適切なパフォーマンスを提供するためにこのアーキテクチャを変更する必要がある可能性があります。 サーバー マネージャーの RDS グラフィカル ユーザー インターフェイス (GUI) は、ユーザー数が 500 人を超える展開には推奨されません。 500 人から 5000 人のユーザーの RDS 展開を管理するには、PowerShell をお勧めします。

* デスクトップ ホスティング サービスに必要なコンポーネントとサービスの最小セット。 デスクトップ ホスティング サービスを強化するために追加できる多くのオプションのコンポーネントやサービスがありますが、それらはこのドキュメントの範囲外です。

このドキュメントを読むことで、閲覧者は次のことを理解できます。
- Microsoft Azure サービスに基づく、安全で、信頼できるマルチテナント型のデスクトップ ホスティング ソリューションを提供するために必要な構成要素。
- 各構成要素の目的とそれらがどのように組み合わされるか。

このアーキテクチャに基づいてデスクトップ ホスティング ソリューションを構築するには、複数の方法があります。 このアーキテクチャは、Windows Server 2016 での Azure の統合と機能強化の概要を示します。 他の展開オプションは、Windows Server 2012 R2 用の「[デスクトップ ホスティング参照ガイド](https://go.microsoft.com/fwlink/p/?LinkId=517389)」を参照してください。

次のトピックについて説明します。
- [デスクトップ ホスティングの論理アーキテクチャ](Desktop-hosting-logical-architecture.md)
- [RDS のロールの理解](./desktop-hosting-service.md)
- [デスクトップ ホスティング環境の理解](Understanding-the-desktop-hosting-environment.md)
- [デスクトップ ホスティングの Azure サービスと考慮事項](Azure-services-and-considerations-for-desktop-hosting.md)