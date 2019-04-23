---
title: 構成ソースよりも先に論理ユニット (Lun) ファイバー チャネルの少ないパスがある場合は、ライブ マイグレーションを許可する仮想ファイバー チャネル アダプターの仮想マシンを有効にしないように
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 6ff69d5cb09133a806c2a2df3446713264a4e892
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849553"
---
# <a name="avoid-enabling-virtual-machines-configured-with-virtual-fibre-channel-adapters-to-allow-live-migrations-when-there-are-fewer-paths-to-fibre-channel-logical-units-luns-on-the-destination-than-on-the-source"></a>構成ソースよりも先に論理ユニット (Lun) ファイバー チャネルの少ないパスがある場合は、ライブ マイグレーションを許可する仮想ファイバー チャネル アダプターの仮想マシンを有効にしないように

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、次を参照してください。 [Run Best Practices Analyzer Scans and Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177)します。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|警告|  
|**カテゴリ**|構成|

次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。
  
## <a name="issue"></a>**問題**  
*1 つまたは複数の仮想マシンには、仮想化 WMI プロバイダーの設定 AllowReducedFcRedunancy プロパティが設定されています。*  
  
## <a name="impact"></a>**影響**  
*次の仮想マシンのライブ マイグレーションは、データが失われる可能性があります。 またはストレージへの I/O の割り込み。*  
  
\<仮想マシンの一覧 >  
  
## <a name="resolution"></a>**解決方法**  
*影響を受ける仮想マシンで AllowReducedFcRedundancy WMI プロパティをクリアすることを検討してください。このプロパティがオフの場合は、先にファイバー チャネルへのパスの数が同じ、またはソース上のパスの数を超える場合にのみ、仮想ファイバー チャネル アダプターで構成された仮想マシンのライブ マイグレーションを実行できます。これらのチェックでは、ストレージにデータの損失や I/O の中断を防ぐのに役立ちます。* 