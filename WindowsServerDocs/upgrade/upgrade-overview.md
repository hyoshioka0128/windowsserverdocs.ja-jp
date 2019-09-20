---
title: Windows Server のアップグレードに関する概要 |Microsoft Docs
description: Windows Server の一般的なアップグレード情報と、実際のアップグレードを行う前に考慮すべき情報について説明します。
ms.prod: windows server
ms.technology: server-general
ms.topic: upgrade
author: RobHindman
ms.author: robhind
ms.date: 09/10/2019
ms.openlocfilehash: 6f57e52657ca3c80c92d56c54ea87e43aabd1e99
ms.sourcegitcommit: 27f0caf74e88781054250455c3c1adf06deb6234
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/19/2019
ms.locfileid: "71124792"
---
# <a name="overview-about-windows-server-upgrades"></a>Windows Server のアップグレードに関する概要

新しいバージョンの Windows Server にアップグレードするプロセスは、開始するオペレーティングシステムと実行する経路によって大きく異なる場合があります。 次の用語を使用して、新しい Windows Server の展開に関係する可能性があるさまざまなアクションを区別します。

- **増設.** "インプレースアップグレード" とも呼ばれます。 以前のバージョンのオペレーティングシステムから新しいバージョンに移行し、同じ物理ハードウェアを維持します。 **このセクションでは、このメソッドについて説明します。**

    >[!Important]
    >また、一括アップグレードは、パブリックまたはプライベートクラウドの企業によってサポートされる場合もあります。ただし、詳細については、クラウドプロバイダーに確認する必要があります。 また、 **VHD から起動**するように構成されている Windows Server では、インプレースアップグレードを実行できません。

- **スト.** "クリーンインストール" とも呼ばれます。 以前のバージョンのオペレーティングシステムから新しいバージョンに移行すると、古いオペレーティングシステムが削除されます。

- **移動.** 以前のバージョンのオペレーティングシステムから新しいバージョンのオペレーティングシステムに移動するには、別のハードウェアまたは仮想マシンのセットに転送します。

- **クラスター OS のローリングアップグレード。** Hyper-v またはスケールアウトファイルサーバーワークロードを停止せずに、クラスターノードのオペレーティングシステムをアップグレードします。 この機能により、サービス レベル アグリーメントに影響する可能性のあるダウンタイムが回避できます。 詳細については、「[クラスターオペレーティングシステムのローリングアップグレード](../failover-clustering/cluster-operating-system-rolling-upgrade.md)」を参照してください。

- **ライセンスの変換。** 単純なコマンドと適切なライセンスキーを使用して、1回の手順でリリースの特定のエディションを同じリリースの別のエディションに変換します。 この "ライセンス変換" を呼び出します。 たとえば、サーバーで Windows Server 2016 Standard を実行している場合、Windows Server 2016 Datacenter に変換できます。

## <a name="which-version-of-windows-server-should-i-upgrade-to"></a>アップグレードする必要がある Windows Server のバージョンを教えてください。

最新バージョンの Windows Server にアップグレードすることをお勧めします。Windows Server 2019。 最新バージョンの Windows Server を実行すると、最新のセキュリティ機能を含む最新の機能を使用して、最高のパフォーマンスを実現できます。

ただし、これは常に可能であるとは限りません。 次の図を使用すると、現在使用しているバージョンに基づいて、アップグレードできる Windows Server のバージョンを確認できます。

![使用可能なインプレースアップグレードパス](media/upgrade-paths.png)

Windows Server は、通常、少なくとも1つのバージョン (場合によっては2つのバージョン) を使用してアップグレードできます。 たとえば、Windows Server 2012 R2 と Windows Server 2016 の両方を Windows Server 2019 にインプレースアップグレードできます。

また、オペレーティングシステムの評価版から製品版、古い製品版から新しいバージョン、場合によっては、オペレーティングシステムのボリュームライセンス版から通常の製品版にアップグレードすることもできます。 インプレースアップグレード以外のアップグレードオプションの詳細については、「 [Windows Server のアップグレードオプションと変換オプション](../get-started/supported-upgrade-paths.md)」を参照してください。
