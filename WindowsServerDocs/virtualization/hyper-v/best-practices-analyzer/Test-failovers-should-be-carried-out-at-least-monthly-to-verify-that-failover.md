---
title: テスト フェールオーバーの実行には、少なくとも毎月フェールオーバーが成功し、フェールオーバー後に予期した仮想マシンのワークロードとして動作することを確認するには
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 57a8aa50-e59e-4a4b-8571-1099d5a8eee4
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: f99ccfe065015d1731978ba5e7f31c766c343efc
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858935"
---
# <a name="test-failovers-should-be-carried-out-at-least-monthly-to-verify-that-failover-will-succeed-and-that-virtual-machine-workloads-will-operate-as-expected-after-failover"></a>テスト フェールオーバーの実行には、少なくとも毎月フェールオーバーが成功し、フェールオーバー後に予期した仮想マシンのワークロードとして動作することを確認するには

>適用対象: Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016| 
|**製品/機能**|Hyper-V|  
|**順**|［警告］|  
|**カテゴリ**|運用|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*少なくとも1か月にテストフェールオーバーが発生していません。*  
  
## <a name="impact"></a>影響  
*計画済みまたは計画外のフェールオーバーが成功するか、フェールオーバー後にワークロード操作が正常に続行されるかを確認するメッセージは表示されません。これは、次の仮想マシンに影響します。*  
  
仮想マシンの一覧を \<>  
  
## <a name="resolution"></a>解決方法  
*Hyper-v マネージャーを使用して、テストフェールオーバーを実行します。*  
  


