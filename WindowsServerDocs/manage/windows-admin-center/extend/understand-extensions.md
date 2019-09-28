---
title: Windows Admin Center 拡張機能について
description: Windows Admin Center SDK 拡張機能 (Project Honolulu) について
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 4bfabe4959fe16f5e240cbf1a972a902e37ffb52
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385248"
---
# <a name="understanding-windows-admin-center-extensions"></a>Windows Admin Center 拡張機能について

>適用先:Windows Admin Center、Windows Admin Center Preview

Windows 管理センターのしくみにまだ慣れていない場合は、概要アーキテクチャから始めましょう。 Windows Admin Center は、次の 2 つの主要コンポーネントで構成されます。

- Web ブラウザーの要求に対して Windows Admin Center UI の Web ページを提供するライトウェイト **Web サービス**です。
- Web ページからの REST API 要求をリッスンし、対象のサーバーまたはクラスターで WMI の呼び出しまたは PowerShell スクリプトが実行されるようにリレーする**ゲートウェイ コンポーネント**です。

![Windows Admin Center のアーキテクチャ](../media/understand-extensions/wac-architecture-500px.png)

Web サービスによって提供される Windows Admin Center UI Web ページには、拡張機能として実装される拡張性の観点からの 2 つの主要な UI コンポーネントであるソリューションとツール、およびゲートウェイ プラグインと呼ばれる 3 つ目の拡張機能の種類があります。

## <a name="solution-extensions"></a>ソリューションの拡張機能

既定では Windows Admin Center のホーム画面で、Windows Server 接続、Windows PC 接続、フェールオーバー クラスター接続、ハイパーコンバージド クラスター接続の 4 種類のうちのいずれかの接続を追加できます。 接続が追加されると、接続の名前と種類がホーム画面に表示されます。 接続名をクリックすると、対象のサーバーまたはクラスターへの接続が試行され、接続のために UI が読み込まれます。

![Windows Admin Center のアーキテクチャ](../media/understand-extensions/solutions-ui.png)

これらの各接続の種類はソリューションにマップされ、ソリューションは “ソリューション“ 拡張機能と呼ばれる種類の拡張機能を使用して定義されます。 ソリューションは通常、サーバー、PC またはフェールオーバー クラスターなどの Windows Admin Center を通じて管理する一意の種類のオブジェクトを定義します。 ネットワーク スイッチや Linux サーバーなどのその他のデバイス、またはリモート デスクトップ サービスなどのサーバーにも接続して管理するための新しいソリューションを定義することもできます。

## <a name="tool-extensions"></a>ツール拡張機能

Windows Admin Center のホーム画面で接続をクリックして接続すると、選択した接続の種類のソリューション拡張機能が読み込まれ、左側のナビゲーション ウィンドウにツールの一覧を含むソリューション UI が表示されます。 ツールをクリックすると、ツール UI が読み込まれ、右側のウィンドウに表示されます。

![Windows Admin Center UI のアーキテクチャ](../media/understand-extensions/ui-architecture.png)

これらの各ツールは、“ツール“ 拡張機能と呼ばれる 2 つ目の種類の拡張機能を使用して定義されます。 ツールが読み込まれると、対象のサーバーまたはクラスターで WMI の呼び出しまたは PowerShell スクリプトを実行し、UI に情報を表示するか、またはユーザー入力に基づいてコマンドを実行することができます。 ツール拡張機能では、表示する必要のあるソリューションを定義するため、各ソリューションについて異なるツール セットが生じます。 新しいソリューション拡張機能を作成する場合は、ソリューションの機能を提供する 1 つ以上のツールの拡張機能をさらに記述する必要があります。

![各ソリューションのツールの一覧](../media/understand-extensions/tools-for-solutions.png)

## <a name="gateway-plugins"></a>ゲートウェイ プラグイン

ゲートウェイ サービスでは、呼び出す UI の REST API を公開し、ターゲットで実行するコマンドとスクリプトをリレーします。 ゲートウェイ サービスは、異なるプロトコルをサポートするゲートウェイ プラグインによって拡張できます。 Windows Admin Center には、PowerShell スクリプトの実行用と WMI コマンド用の 2 つのゲートウェイ プラグインが事前にパッケージ化されています。 REST など、PowerShell または WMI 以外のプロトコルによってターゲットと通信する必要がある場合は、そのためのゲートウェイ プラグインを構築できます。

## <a name="next-steps"></a>次の手順

Windows Admin Center で構築する機能に応じて、既存のサーバーまたはクラスター ソリューション向けの[ツール拡張機能を構築する](develop-tool.md)だけで十分であり、これが拡張機能を構築するための最も簡単な最初の手順です。 ただし、機能がサーバーやクラスターではなく、デバイス、サービス、または完全に新しいものを管理するためのものである場合は、1 つ以上のツールを使用して[ソリューション拡張機能を構築する](develop-solution.md)ことを考慮する必要があります。 最後に、WMI または PowerShell 以外のプロトコルを使用してターゲットと通信する必要がある場合は、[ゲートウェイプラグインを作成](develop-gateway-plugin.md)する必要があります。 [さらに読み進めて](developing-extensions.md)開発環境を設定する方法および最初の拡張機能の記述を開始する方法を確認してください。
