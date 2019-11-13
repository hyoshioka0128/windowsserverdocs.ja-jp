---
title: 動的メモリは有効になっていますが、一部の仮想マシンでは応答しません
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 91b7f50f-a071-4ab6-beb1-1b29f92f52b6
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 9aa482d91c94a7a619bb65046cf152d6a5f8827a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393680"
---
# <a name="dynamic-memory-is-enabled-but-not-responding-on-some-virtual-machines"></a>動的メモリは有効になっていますが、一部の仮想マシンでは応答しません

>適用対象: Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|Warning|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*1つ以上のバーチャルマシンで、ゲストオペレーティングシステムの動的メモリに必要なドライバーの問題が発生しています。*  
  
## <a name="impact"></a>影響  
*次の仮想マシンのゲストオペレーティングシステムが実行されていないか、または実行できない可能性があります。これは、Hyper-v がメモリを動的に調整して、メモリの需要の変化に対応することができないためです。これは、次の仮想マシンに影響します。*  
  
仮想マシンの一覧を \<>  
  
## <a name="resolution"></a>解決方法  
*これは、仮想マシンが起動している場合に想定される動作です。バーチャルマシンが起動していない場合は、統合サービスが最新バージョンにアップグレードされていること、およびゲストオペレーティングシステムが動的メモリをサポートしていることを確認してください。*  
  
Windows Server 2016 の場合、integration services は Windows Update を通じて配信されます。 最新バージョンの integration services を取得するための更新プログラムを受信するように仮想マシンが構成されていることを確認します。  
  
動的メモリは、サポートされているゲストの特定のバージョンで動作します。 参照してください [HYPER-V 動的メモリの概要](https://technet.microsoft.com/library/hh831766.aspx) の Windows Server 2016 および Windows 10 より前のバージョン。  
  


