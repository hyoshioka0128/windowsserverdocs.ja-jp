---
title: SR-IOV 用に構成された仮想マシンの実行の数は仮想マシンで使用できる仮想関数の数を超えることはできません。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 8bd4af5e-9e7d-4710-8950-39435a8bb373
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 3c58e980471284c950f41551b02b92bf74aca7cc
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854615"
---
# <a name="the-number-of-running-virtual-machines-configured-for-sr-iov-should-not-exceed-the-number-of-virtual-functions-available-to-the-virtual-machines"></a>SR-IOV 用に構成された仮想マシンの実行の数は仮想マシンで使用できる仮想関数の数を超えることはできません。

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
*シングルルート i/o 仮想化 (SR-IOV) 用に構成されている実行中の仮想マシンの数に使用できる仮想機能が不足しています。*  
  
## <a name="impact"></a>影響  
*次の仮想マシンでは、ネットワークのパフォーマンスが最適ではない可能性があります。*  
   
仮想マシンの一覧を \<>  
  
## <a name="resolution"></a>解決方法  
*Sr-iov 仮想機能を必要としない1つ以上の仮想マシンで sr-iov を無効にすることを検討してください。*  
  


