---
title: オフピーク時間にレプリケーションの再同期をスケジュールする必要があります。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 093a7bb7-8e0a-486b-b42b-04edd8809710
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: ae630f93ef50ebc977de2bffcefa3b27b03622ee
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861795"
---
# <a name="resynchronization-of-replication-should-be-scheduled-for-off-peak-hours"></a>オフピーク時間にレプリケーションの再同期をスケジュールする必要があります。

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
*プライマリ仮想マシンのレプリケーションの再同期は、ピーク時以外にはスケジュールされません。*  
  
## <a name="impact"></a>影響  
*仮想マシンの再同期が必要な状態が長くなるほど、レプリケーションログファイルが大きくなり、プライマリ仮想マシンでレプリケートされていない変更が増えることになります。これは、次の仮想マシンに影響します。*  
  
仮想マシンの一覧を \<>  
  
## <a name="resolution"></a>解決方法  
*Hyper-v マネージャーを使用して、仮想マシンのレプリケーション設定を変更し、オフピーク時間中に自動的に再同期を実行します。*  
  


