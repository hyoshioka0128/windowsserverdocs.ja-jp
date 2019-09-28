---
title: 仮想ファイバーチャネルアダプターで構成された仮想マシンが、コピー先のファイバーチャネル論理ユニット (Lun) へのパスがソースよりも小さい場合にライブマイグレーションを実行できるようにしない
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: c55a8c76391ae1b01f43492dc5c72e3760371b80
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365277"
---
# <a name="avoid-enabling-virtual-machines-configured-with-virtual-fibre-channel-adapters-to-allow-live-migrations-when-there-are-fewer-paths-to-fibre-channel-logical-units-luns-on-the-destination-than-on-the-source"></a>仮想ファイバーチャネルアダプターで構成された仮想マシンが、コピー先のファイバーチャネル論理ユニット (Lun) へのパスがソースよりも小さい場合にライブマイグレーションを実行できるようにしない

>適用先:Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|警告|  
|**カテゴリ**|構成|

次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。
  
## <a name="issue"></a>**問題**  
*1つ以上の仮想マシンで、仮想化 WMI プロバイダーに AllowReducedFcRedunancy プロパティが設定されています。*  
  
## <a name="impact"></a>**よる**  
*次の仮想マシンのライブマイグレーションにより、データが失われたり、記憶域への i/o が中断されることがあります。*  
  
@no__t-仮想マシンの > の一覧  
  
## <a name="resolution"></a>**解決方法**  
*影響を受ける仮想マシンで AllowReducedFcRedundancy WMI プロパティをクリアすることを検討してください。このプロパティをオフにすると、仮想ファイバーチャネルアダプターが構成されている仮想マシンでライブマイグレーションを実行できるのは、移行先でファイバーチャネルするパスの数が、ソースのパスの数と同じか、それよりも多い場合のみです。これらのチェックは、データの損失や記憶域への i/o の中断を防ぐのに役立ちます。* 