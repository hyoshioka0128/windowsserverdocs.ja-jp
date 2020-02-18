---
title: Windows Server のアップグレードに関する概要 | Microsoft Docs
description: Windows Server の一般的なアップグレード情報と、実際のアップグレードの実行前に考慮すべきことについて説明します。
ms.prod: windows server
ms.technology: server-general
ms.topic: upgrade
author: RobHindman
ms.author: robhind
ms.date: 09/10/2019
ms.openlocfilehash: 6f57e52657ca3c80c92d56c54ea87e43aabd1e99
ms.sourcegitcommit: 27f0caf74e88781054250455c3c1adf06deb6234
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/19/2019
ms.locfileid: "71124792"
---
# <a name="overview-about-windows-server-upgrades"></a>Windows Server のアップグレードに関する概要

新しいバージョンの Windows Server にアップグレードするプロセスは、開始するオペレーティング システムの種類や選択するパスに応じて大きく異なる場合があります。 新しい Windows Server の展開にかかわる可能性のあるさまざまな操作は次の用語を使用して区別します。

- **アップグレード。** "インプレース アップグレード" とも呼ばれます。 同じ物理ハードウェアの使用を継続しながら、古いバージョンのオペレーティング システムから新しいバージョンに移行します。 **これは、このセクションで説明する方法です。**

    >[!Important]
    >インプレース アップグレードはパブリック クラウドまたはプライベート クラウドの企業でサポートされている場合もありますが、詳細については、クラウド プロバイダーに確認する必要があります。 また、**VHD から起動するように**構成されている Windows Server では、インプレース アップグレードを実行できません。

- **インストール**。 "クリーン インストール" とも呼ばれます。 古いバージョンのオペレーティング システムから新しいバージョンに移行し、古いオペレーティング システムは削除されます。

- **移行。** 別のハードウェアまたは仮想マシンのセットに転送することで、古いバージョンのオペレーティング システムから新しいバージョンのオペレーティング システムに移行します。

- **クラスター OS のローリング アップグレード。** Hyper-V またはスケールアウト ファイル サーバーのワークロードを停止することなく、クラスター ノードのオペレーティング システムをアップグレードします。 この機能により、サービス レベル アグリーメントに影響する可能性のあるダウンタイムが回避できます。 詳細については、「[クラスター オペレーティング システムのローリング アップグレード](../failover-clustering/cluster-operating-system-rolling-upgrade.md)」を参照してください。

- **ライセンス変換。** 簡単なコマンドと適切なライセンス キーを使用して、1 回の手順でリリースの特定のエディションを同じリリースの別のエディションに変換します。 これは、"ライセンス変換" と呼ばれています。 たとえば、サーバーで Windows Server 2016 Standard を実行している場合、Windows Server 2016 Datacenter に変換できます。

## <a name="which-version-of-windows-server-should-i-upgrade-to"></a>どのバージョンの Windows Server にアップグレードする必要があるか?

次の最新バージョンの Windows Server にアップグレードすることをお勧めします:Windows Server 2019。 最新バージョンの Windows Server を実行すると、最新のセキュリティ機能を含む最新機能を使用して、最適なパフォーマンスを実現できます。

ただし、これは常に可能であるとは限りません。 次の図を使用すると、現在使用しているバージョンに基づいて、どの Windows Server バージョンにアップグレードできるかを把握できます。

![利用可能なインプレース アップグレードのパス](media/upgrade-paths.png)

Windows Server は、通常、少なくとも 1 つ (場合によっては 2 つ) のバージョンを経てアップグレードできます。 たとえば、Windows Server 2012 R2 と Windows Server 2016 はいずれも Windows Server 2019 にインプレース アップグレードできます。

オペレーティング システムの評価版から製品版、古い製品版から新しい製品版、または場合によってはオペレーティング システムのボリューム ライセンス版から通常の製品版にアップグレードすることもできます。 インプレース アップグレード以外のアップグレード オプションの詳細については、[Windows Server のアップグレード オプションと変換オプション](../get-started/supported-upgrade-paths.md)に関する記事を参照してください。
