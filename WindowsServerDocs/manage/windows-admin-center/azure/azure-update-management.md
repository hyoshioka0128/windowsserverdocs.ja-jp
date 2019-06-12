---
title: Azure の Update Management の使用のオペレーティング システムの更新プログラムを管理する Windows Admin Center を使用
description: OS を管理する Azure の更新の管理の設定を使用して Windows Admin Center (プロジェクト ホノルル) を更新します。
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 07/17/2018
ms.localizationpriority: low
ms.prod: windows-server-threshold
ms.openlocfilehash: 79b18e9963fba0993a7f34b1409edba6abfd48f0
ms.sourcegitcommit: 48bb3e5c179dc520fa879b16c9afe09e07c87629
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66452544"
---
# <a name="use-windows-admin-center-to-manage-operating-system-updates-with-azure-update-management"></a>Azure の Update Management の使用のオペレーティング システムの更新プログラムを管理する Windows Admin Center を使用

[Azure Windows Admin Center との統合について説明します。](../plan/azure-integration-options.md)

Azure の更新プログラム管理は、サーバー単位ではなく、1 つの場所から更新プログラムとパッチを複数のマシンを管理するための Azure Automation でのソリューションです。 Azure の Update Management、すぐに利用可能な更新の状態を評価する、必要な更新プログラムのインストールをスケジュールして正常に適用される更新プログラムを確認する展開の結果を確認できます。 これは、かどうか、マシンは、Azure Vm に他のクラウド プロバイダーまたはオンプレミスでホストされていることです。 [Azure の更新プログラムの管理について説明します。](https://docs.microsoft.com/azure/automation/automation-update-management)

Windows Admin Center では、簡単を設定して、Azure の更新プログラム管理を使用して、管理対象サーバーを最新に保つためにことができます。 Azure サブスクリプションで Log Analytics ワークスペースがない場合 Windows Admin Center は自動的にサーバーを構成し、サブスクリプションおよび場所を指定するために必要な Azure リソースを作成します。 既存の Log Analytics ワークスペースがあれば、Windows Admin Center は Azure の更新プログラムの管理から更新プログラムを使用するようにサーバーを自動的に構成できます。  

開始するには、サーバー接続の更新プログラム ツールに移動し、「"今すぐセットアップ"、を選択し、、関連する Azure リソース設定を提供します。 

Azure の更新プログラム管理で管理するようにサーバーを構成したら、更新プログラム ツールで提供されるハイパーリンクを使用して Azure の Update Management をアクセスできます。 

[サーバーを更新する Azure の Update Management の使用を停止する方法について説明します。](azure-monitor.md#disabling-monitoring)

注意する必要のある[Windows Admin Center ゲートウェイを Azure に登録](../configure/azure-integration.md)Azure 更新プログラム管理をセットアップする前にします。

