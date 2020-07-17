---
title: 使用可能な場合は、ネットワークにすべての仮想機能を使用する
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: bf895484-6a0d-4aa4-9a42-9fac739e875d
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 0fab06ae21a4632df73b7a4d8b17b12665ffed98
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854215"
---
# <a name="use-all-virtual-functions-for-networking-when-they-are-available"></a>使用可能な場合は、ネットワークにすべての仮想機能を使用する

>適用対象: Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|［警告］|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*一部のハードウェアアクセラレータ機能が使用されていません*  
  
## <a name="impact"></a>影響  
*この構成によって、全体的な CPU 使用率が必要以上に高くなる可能性があります。次の仮想マシンでは、ネットワークのパフォーマンスが最適ではない可能性があります。*  
  
仮想マシンの一覧を \<>  
  
## <a name="resolution"></a>解決方法  
*物理ハードウェアが sr-iov をサポートし、この構成が仮想マシンに必要なネットワーク機能と競合しない場合は、sr-iov 用の仮想ネットワークアダプターを構成することを検討してください。*  
  


