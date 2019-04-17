---
title: Windows Admin Center を使用する Azure Update Management によるオペレーティング システムの更新プログラムの管理
description: OS を管理する Azure アップデート管理の設定を使用して Windows Admin Center (Project Honolulu) を更新します。
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 07/17/2018
ms.localizationpriority: low
ms.prod: windows-server-threshold
ms.openlocfilehash: 5ba81968f8baa81176ad646fb2a97961ddc49fda
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296989"
---
# Windows Admin Center を使用する Azure Update Management によるオペレーティング システムの更新プログラムの管理

[Windows Admin Center での Azure 統合の詳細](../plan/azure-integration-options.md)

Azure の更新プログラムの管理は、ソリューション Azure オートメーションでは、サーバーごとではなく、1 つの場所から更新プログラムと複数のコンピューターの更新プログラムを管理することができます。 Azure 更新プログラムの管理を迅速に利用可能な更新プログラムの状態を評価、必須の更新プログラムのインストールのスケジュールして正常に適用できる更新プログラムを確認する展開の結果を確認できます。 これは、マシンは、Azure Vm、オンプレミスまたはその他のクラウド プロバイダーによってホストされているかどうか。 [Azure の更新プログラムの管理について説明します。](https://docs.microsoft.com/azure/automation/automation-update-management)

Windows Admin center では、簡単を設定し、Azure の更新プログラムの管理を使って、管理対象サーバーを常に最新の状態に保つことができます。 Log Analytics ワークスペースで Azure サブスクリプションがあるない、Windows Admin Center のサーバーを構成は自動的に作成し、サブスクリプションと指定した場所で必要な Azure リソースを作成します。 既存の Log Analytics ワークスペースを使っている場合、Windows Admin Center は Azure Update Management から更新プログラムを利用するようにサーバーを自動的に構成できます。  

最初に、サーバー間の接続で更新ツールに移動して「ようになりましたセットアップ」を選び関連の Azure リソースの基本設定を提供します。 

Azure Update Management で管理するため、サーバーを構成した後は、更新プログラムのツールで提供されるハイパーリンクを使用して Azure Update Management を表示できます。 

[Azure Update Management を使用して、サーバーを更新するを停止する方法について説明します。](azure-monitor.md#disabling-monitoring)

必ず[、Windows Admin Center ゲートウェイを Azure に登録](..\configure\azure-integration.md)Azure Update Management をセットアップする前に注意してください。

