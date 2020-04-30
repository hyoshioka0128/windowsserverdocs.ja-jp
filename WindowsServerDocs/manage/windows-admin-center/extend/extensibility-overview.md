---
title: Windows Admin Center の拡張機能
description: Windows Admin Center SDK の拡張機能 (Project Honolulu)
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 09/17/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 010ab340dc71d199119f1bd51fbc22e3ad449040
ms.sourcegitcommit: 074b59341640a8ae0586d6b37df7ba256e03a0c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81650081"
---
# <a name="extensions-for-windows-admin-center"></a>Windows Admin Center の拡張機能

>適用先:Windows Admin Center、Windows Admin Center Preview

Windows Admin Center は拡張可能なプラットフォームとして構築され、パートナーと開発者が Windows Admin Center 内で既存の機能を利用できるようにすることで、他の IT 管理製品およびソリューションとシームレスに統合し、お客様に付加価値を提供しています。 Windows Admin Center の各ソリューションおよびツールは、パートナーと開発者が利用できるのと同じ拡張機能を使用して拡張機能として構築されています。そのため、現在 Windows Admin Center で利用可能なものと同様の強力なツールを作成することができます。

Windows Admin Center 拡張機能は、HTML5、CSS、Angular、TypeScript、jQuery など最新の Web テクノロジを使用して構築されており、PowerShell や WMI を介して対象サーバーを管理することができます。 また、Windows Admin Center のゲートウェイ プラグインを構築することで、REST などの異なるプロトコルで対象のサーバー、サービス、またはデバイスを管理することもできます。

## <a name="why-you-should-consider-developing-an-extension-for-windows-admin-center"></a>Windows Admin Center の拡張機能の開発を考慮する必要がある理由

次に、Windows 管理センターの拡張機能を開発することによって、製品と顧客にもたらす価値を示します。

- **Windows Admin Center ツールとの統合:** Windows Admin Center でサーバーおよびクラスター管理ツールを使用して製品とサービスを統合し、監視、管理、トラブルシューティングの統一されたシームレスなエンド ツー エンドのエクスペリエンスをお客様に提供できます。
- **プラットフォームのセキュリティ、id、および管理機能を活用します。** Windows 管理センターのプラットフォーム機能を活用して、現在の IT 組織の複雑な要件を満たすことで、Azure Active Directory (AAD) のサポート、Multi-Factor Authentication、ロールベースの Access Control (RBAC)、ログ記録、製品とサービスの監査を有効にします。
- **最新の Web テクノロジを使用した開発:** HTML5、CSS、Angular、TypeScript および jQuery、また Windows Admin Center SDK に含まれる充実した強力な UI コントロールを含む最新の Web テクノロジを使用して、魅力的なユーザー エクスペリエンスを簡単に作成できます。
- **製品の支援を拡張する:** 拡張された顧客ベースを利用して、Windows 管理センターエコシステムの一部になることができます。

## <a name="start-developing-with-the-windows-admin-center-sdk"></a>Windows 管理センター SDK を使用した開発の開始

Windows 管理センターの開発を簡単に開始できるようになりました。  サンプルコードについては、SDK ドキュメントの「[ツール](develop-tool.md)、[ソリューション](develop-solution.md)、および[ゲートウェイのプラグイン](develop-gateway-plugin.md)拡張機能の種類」を参照してください。 ここでは、Windows 管理センター CLI を利用して新しい拡張機能プロジェクトをビルドした後、個々のガイドに従って、ニーズに合わせてプロジェクトをカスタマイズします。

Windows 管理センターのスタイル、コントロール、およびページテンプレートを使用して、PowerPoint の拡張機能を迅速にモックアップするために使用できる Windows 管理センター [SDK design toolkit](https://github.com/Microsoft/windows-admin-center-sdk/blob/master/WindowsAdminCenterDesignToolkit.zip)を用意しました。 コーディングを開始する前に、Windows 管理センターで拡張機能がどのように表示されるかを確認してください。

GitHub でホストされているサンプルコードもあります。[開発者ツール](https://aka.ms/wacsdk)は、独自の拡張機能で参照して使用できる豊富なコントロールのコレクションを含むサンプルソリューション拡張機能です。 開発者ツールは、開発者モードで Windows Admin Center にサイド ローディングすることができる完全に機能する拡張機能です。

SDK の詳細を確認し、作業を開始するには、次のトピックを参照してください。

- [拡張機能のしくみについて](understand-extensions.md)
- [拡張機能の開発](developing-extensions.md)
- [ガイド](guides.md)
- [拡張機能の公開](publish-extensions.md)

## <a name="partner-spotlight"></a>パートナー スポットライト

パートナーが Windows Admin Center エコシステムにもたらし始めたすばらしい価値を確認し、今すぐそれらの拡張機能を試してください。 Windows Admin Center から[拡張機能をインストールする方法](../configure/using-extensions.md)の詳細については、こちらを参照してください。

### <a name="biitops"></a>BiitOps
BiitOps の拡張機能は、Windows Server の物理/バーチャルマシンのハードウェア、ソフトウェア、および構成設定の変更の追跡を提供します。 BiitOps の拡張機能によって、新しいもの、変更されたもの、および単一のウィンドウガラスで削除されたものが正確に表示され、コンプライアンス、信頼性、セキュリティに関する問題を追跡するのに役立ちます。 [BiitOps の拡張機能の詳細については、こちらを参照して](case-studies/biitops.md)ください。

![BiitOps 拡張機能](../media/extensibility-overview/biitops-1.png)

### <a name="dataon"></a>DataON

DataON 拡張機能では、Windows Server に基づいて、ハイパー集約型インフラストラクチャおよびストレージシステムのデータに対する監視、管理、エンドツーエンドの洞察を得ることができます。 拡張機能には、履歴データレポート、ディスクマッピング、システムアラート、SAN などの電話ホームサービスなどの一意の値が追加されます。これにより、Windows 管理センターサーバーとハイパー集約型インフラストラクチャの管理機能がシームレスな統合されたエクスペリエンスによって補完されます。 [DataON の MUST 拡張機能と開発エクスペリエンスの詳細については、こちらを参照してください](case-studies/dataon.md)。

![DataON MUST 拡張機能](../media/extensibility-overview/dataon-must-extension.png)

### <a name="fujitsu"></a>Fujitsu

Windows 管理センターの富士通の ServerView Health および RAID Health extensions は、富士通 PRIMERGY サーバーのプロセッサ、メモリ、パワー、記憶域サブシステムなどの重要なハードウェアコンポーネントの詳細な監視と管理を提供します。 Windows Admin Center UX の設計パターンと UI コントロールを利用することで、Fujitsu は Windows Admin Center プラットフォームを通じて、サーバー ロールとサービス、オペレーティング システム、ハードウェア管理に至るまで、エンド ツー エンドの洞察のビジョンに対して大きな前進をもたらしました。 [Fujitsu の拡張機能と開発エクスペリエンスの詳細については、こちらを参照してください](case-studies/fujitsu.md)。

![Fujitsu ServerView 拡張機能](../media/extensibility-overview/fujitsu-serverview-extension.png)

### <a name="lenovo"></a>Lenovo

Lenovo XClarity インテグレーターの拡張機能は、Windows 管理センター内のさまざまなエクスペリエンスにシームレスに統合することで、次のレベルにハードウェア管理を行います。 XClarity インテグレーターソリューションには、すべての Lenovo サーバーの概要が示されており、単一サーバー、フェールオーバークラスター、またはハイパー集約クラスターに接続されているかどうかに応じて、さまざまなツール拡張機能によってハードウェアの詳細が提供されます。 [Lenovo XClarity インテグレーター拡張機能の詳細については、こちらを参照して](case-studies/lenovo.md)ください。

![Lenovo 拡張機能](../media/extensibility-overview/lenovo-extension.png)

### <a name="pure-storage"></a>Pure Storage

純粋なストレージは、データ中心のアーキテクチャを提供し、競争力を高めるためにビジネスを促進する、エンタープライズ、すべてのフラッシュデータストレージソリューションを提供します。 Windows 管理センターの純粋なストレージ拡張機能は、純粋な FlashArray 製品に対する単一のウィンドウビューを提供し、ユーザーが単一の UI エクスペリエンスで監視タスクを実行したり、リアルタイムのパフォーマンスメトリックを表示したり、ストレージボリュームとイニシエーターを管理したりできるようにします。 [純粋な拡張機能とその開発エクスペリエンスの詳細については、こちらをご覧](case-studies/purestorage.md)ください。

![純粋なストレージ拡張機能](../media/extensibility-overview/purestorage-extension.png)

### <a name="qct"></a>QCT

QCT Management Suite 拡張機能は、QCT Azure Stack HCI 認定システムの物理サーバーの監視と管理を提供することで、Windows 管理センターを補完します。 QCT Management Suite 拡張機能には、サーバーのハードウェア情報が表示されます。また、物理ディスクを効率的に、ハードウェアイベントログツール、および S.M.A.R.T. に置き換えるための直感的なウィザード UI が用意されています。 ベースの予測ディスク管理。 [QCT Management Suite 拡張機能の詳細については、こちらを参照して](case-studies/qct.md)ください。

![QCT 拡張機能](../media/extensibility-overview/qct-extension.png)