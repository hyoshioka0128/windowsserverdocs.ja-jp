---
title: テスト フェールオーバーの実行には、少なくとも毎月フェールオーバーが成功し、フェールオーバー後に予期した仮想マシンのワークロードとして動作することを確認するには
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 57a8aa50-e59e-4a4b-8571-1099d5a8eee4
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 879c860caede942393f0929faab9e4d567f225a6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856143"
---
# <a name="test-failovers-should-be-carried-out-at-least-monthly-to-verify-that-failover-will-succeed-and-that-virtual-machine-workloads-will-operate-as-expected-after-failover"></a>テスト フェールオーバーの実行には、少なくとも毎月フェールオーバーが成功し、フェールオーバー後に予期した仮想マシンのワークロードとして動作することを確認するには

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、次を参照してください。 [Run Best Practices Analyzer Scans and Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177)します。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016| 
|**製品/機能**|Hyper-V|  
|**重要度**|警告|  
|**カテゴリ**|操作|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*なかったテスト フェールオーバーには少なくとも 1 か月間で。*  
  
## <a name="impact"></a>影響  
*計画または計画外のフェールオーバーが成功またはワークロードの操作は、フェールオーバー後に正しく続行を確認することはありません。これには、次の仮想マシンに影響します。*  
  
\<仮想マシンの一覧 >  
  
## <a name="resolution"></a>解決方法  
*HYPER-V マネージャーを使用して、テスト フェールオーバーを実行します。*  
  


