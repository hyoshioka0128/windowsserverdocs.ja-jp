---
title: Windows 管理センターを使用して、Azure Update Management でオペレーティングシステムの更新を管理する
description: Windows 管理センター (Project ホノルル) を使用して、OS の更新を管理するように Azure Update Management を設定します。
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 07/17/2018
ms.localizationpriority: low
ms.prod: windows-server
ms.openlocfilehash: 7b38dae62232c61afafd65eabaf239ad7e747d69
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407068"
---
# <a name="use-windows-admin-center-to-manage-operating-system-updates-with-azure-update-management"></a>Windows 管理センターを使用して、Azure Update Management でオペレーティングシステムの更新を管理する

[Azure と Windows 管理センターとの統合の詳細については、こちらを参照してください。](../plan/azure-integration-options.md)

Azure Update Management は Azure Automation のソリューションであり、サーバー単位ではなく、複数のコンピューターの更新プログラムと修正プログラムを1か所から管理できます。 Azure Update Management では、利用可能な更新プログラムの状態を迅速に評価したり、必要な更新プログラムのインストールをスケジュールしたり、展開結果を確認して更新プログラムの正常適用を検証したりできます。 これは、マシンが Azure Vm であるか、他のクラウドプロバイダーによって、またはオンプレミスでホストされているかにかかわらず発生します。 [Azure Update Management の詳細については、こちらをご覧ください。](https://docs.microsoft.com/azure/automation/automation-update-management)

Windows 管理センターでは、Azure Update Management を簡単にセットアップして使用し、管理対象サーバーを最新の状態に保つことができます。 Azure サブスクリプションに Log Analytics ワークスペースがまだない場合、Windows 管理センターはサーバーを自動的に構成し、指定したサブスクリプションと場所に必要な Azure リソースを作成します。 既存の Log Analytics ワークスペースがある場合、Windows 管理センターでは、Azure Update Management からの更新プログラムを使用するようにサーバーを自動的に構成できます。  

開始するには、サーバー接続の更新プログラムツールに移動し、[今すぐセットアップ] を選択して、関連する Azure リソースの設定を指定します。 

Azure Update Management によって管理されるようにサーバーを構成したら、更新ツールで提供されているハイパーリンクを使用して Azure Update Management にアクセスできます。 

[Azure Update Management の使用を停止してサーバーを更新する方法について説明します。](azure-monitor.md#disabling-monitoring)

Azure Update Management を設定する前に[、Windows 管理センターゲートウェイを azure に登録](../configure/azure-integration.md)する必要があることに注意してください。

