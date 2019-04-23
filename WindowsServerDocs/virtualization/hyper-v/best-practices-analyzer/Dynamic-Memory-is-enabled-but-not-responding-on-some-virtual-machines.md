---
title: 動的メモリが有効になっているが、一部の仮想マシン上で応答しません。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 91b7f50f-a071-4ab6-beb1-1b29f92f52b6
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 95fd426929f3e2f6f01bc10b207a21a57f1d8370
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887783"
---
# <a name="dynamic-memory-is-enabled-but-not-responding-on-some-virtual-machines"></a>動的メモリが有効になっているが、一部の仮想マシン上で応答しません。

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、次を参照してください。 [Run Best Practices Analyzer Scans and Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177)します。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|警告|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*1 つまたは複数の仮想マシンには、動的メモリ、ゲスト オペレーティング システムで必要なドライバーを使用した問題が発生します。*  
  
## <a name="impact"></a>影響  
*次の仮想マシンでゲスト オペレーティング システムでは、実行されない可能性または、HYPER-V はメモリ需要の変化に応答するには、動的にメモリを調整することはできませんので含んで実行可能性があります。これには、次の仮想マシンに影響します。*  
  
\<仮想マシンの一覧 >  
  
## <a name="resolution"></a>解決方法  
*これは、仮想マシンが起動中の場合に想定される動作です。仮想マシンを起動していない場合は、統合サービスが最新バージョンにアップグレードされると、ゲスト オペレーティング システムが動的メモリをサポートしていることを確認します。*  
  
Windows Server 2016 integration services は、Windows Update を通じて配信されます。 Integration services の最新バージョンを取得する更新プログラムを受信する仮想マシンが構成されていることを確認します。  
  
動的メモリは、サポートされているゲストの特定のバージョンで動作します。 参照してください [HYPER-V 動的メモリの概要](https://technet.microsoft.com/library/hh831766.aspx) の Windows Server 2016 および Windows 10 より前のバージョン。  
  


