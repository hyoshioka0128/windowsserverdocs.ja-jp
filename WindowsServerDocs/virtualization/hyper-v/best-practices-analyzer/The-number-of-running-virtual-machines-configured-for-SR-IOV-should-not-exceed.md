---
title: SR-IOV 用に構成された仮想マシンの実行の数は仮想マシンで使用できる仮想関数の数を超えることはできません。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 8bd4af5e-9e7d-4710-8950-39435a8bb373
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 0887035c84ebc4b7d93163533387f2f8ab20fb87
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71364611"
---
# <a name="the-number-of-running-virtual-machines-configured-for-sr-iov-should-not-exceed-the-number-of-virtual-functions-available-to-the-virtual-machines"></a>SR-IOV 用に構成された仮想マシンの実行の数は仮想マシンで使用できる仮想関数の数を超えることはできません。

>適用先:Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|警告|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*シングルルート i/o 仮想化 (SR-IOV) 用に構成されている実行中の仮想マシンの数に使用できる仮想機能が不足しています。*  
  
## <a name="impact"></a>影響  
*次の仮想マシンでは、ネットワークのパフォーマンスが最適ではない可能性があります。*  
   
@no__t-仮想マシンの > の一覧  
  
## <a name="resolution"></a>解決方法  
*Sr-iov 仮想機能を必要としない1つ以上の仮想マシンで sr-iov を無効にすることを検討してください。*  
  


