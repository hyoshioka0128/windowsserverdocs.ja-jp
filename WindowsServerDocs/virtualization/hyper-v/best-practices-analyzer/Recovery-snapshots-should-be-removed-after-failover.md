---
title: フェールオーバー後に回復スナップショットを削除する必要があります。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 922115fa-e8dd-4055-aaf1-4a4437c5cf28
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 4663320df91019fc7dc1d8ca7ffdb2fcc3e0de42
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837683"
---
# <a name="recovery-snapshots-should-be-removed-after-failover"></a>フェールオーバー後に回復スナップショットを削除する必要があります。

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、次を参照してください。 [Run Best Practices Analyzer Scans and Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177)します。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016| 
|**製品/機能**|Hyper-V|  
|**重要度**|警告|  
|**カテゴリ**|操作|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>**問題**  
*仮想マシンのフェールオーバーを持つ 1 つまたは複数の復旧スナップショットです。*  
  
## <a name="impact"></a>**影響**  
*スナップショット ファイルを格納する物理ディスクの使用可能な領域が不足します。このような場合、物理記憶域に対して追加のディスク操作を実行できるはされません。物理ストレージに依存する任意の仮想マシンを受ける可能性があります。これには、次の仮想マシンに影響します。*  
  
\<仮想マシンの一覧 >  
  
## <a name="resolution"></a>**解決方法**  
*フェールオーバーされた仮想マシンごとには、回復スナップショットを削除し、フェールオーバーの完了を示すために Windows PowerShell で Complete-vmfailover コマンドレットを使用します。*  
  


