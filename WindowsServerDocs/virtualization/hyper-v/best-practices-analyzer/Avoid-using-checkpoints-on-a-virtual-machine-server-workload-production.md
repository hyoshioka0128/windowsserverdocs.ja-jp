---
title: 運用環境で、サーバー ワークロードを実行する仮想マシンをチェックポイントを使用しないでください。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 1be75890-d316-495a-b9b7-be75fc1aac10
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 166ef839a40452cc4156144e10e9c666e7ce3472
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856153"
---
# <a name="avoid-using-checkpoints-on-a-virtual-machine-that-runs-a-server-workload-in-a-production-environment"></a>運用環境で、サーバー ワークロードを実行する仮想マシンをチェックポイントを使用しないでください。

>適用先:Windows Server 2016


  
*ベスト プラクティスとスキャンの詳細については、次を参照してください。* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786)します。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|警告|  
|**カテゴリ**|操作|  

次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。

> [!NOTE]  
> Windows Server 2012 r2、仮想マシンのスナップショットは、System Center Virtual Machine Management で使用される用語と一致する場合、HYPER-V マネージャーで仮想マシンのチェックポイントに名前が変更されました。 詳細については、次を参照してください。 [Checkpoints and Snapshots Overview](https://technet.microsoft.com/library/dn818483.aspx)します。  
  
## <a name="issue"></a>問題  
  
*1 つまたは複数のチェックポイントを使用して仮想マシンが検出されました。*  
  
## <a name="impact"></a>影響  
  
*チェックポイント ファイルを格納する物理ディスクの使用可能な領域が不足します。このような場合、物理記憶域に対して追加のディスク操作を実行できるはされません。物理記憶域に依存している任意の仮想マシンを受ける可能性があります。*  
  
物理ディスク領域がなくなる場合チェックポイントまたは仮想ハード_ディスクのディスクに格納されている実行中の仮想マシンが自動的に一時停止して可能性があります。 HYPER-V マネージャーでは、「一時停止しているクリティカル」としてこれらの仮想マシンの状態が表示されます。  
  
## <a name="resolution"></a>解決方法  
  
*仮想マシンは、運用環境で、サーバー ワークロードを実行する場合、仮想マシンをオフラインにして適用したり、チェックポイントを削除し、HYPER-V マネージャーを使用します。チェックポイントを削除するには、プロセスを完了する仮想マシンをシャット ダウンする必要があります。*  
  
> [!NOTE]  
> 実稼働のチェックポイントは、標準のチェックポイントの代替として使用できるようになりました。 詳細については、次を参照してください。[標準または実稼働のチェックポイント間選択](../manage/Choose-between-standard-or-production-checkpoints-in-Hyper-V.md)します。  
  


