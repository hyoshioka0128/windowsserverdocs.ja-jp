---
title: SR-IOV 用に構成された仮想マシンの実行の数は仮想マシンで使用できる仮想関数の数を超えることはできません。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 8bd4af5e-9e7d-4710-8950-39435a8bb373
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: e63df9283927437f9cfc62c052d83b07fe599b34
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829753"
---
# <a name="the-number-of-running-virtual-machines-configured-for-sr-iov-should-not-exceed-the-number-of-virtual-functions-available-to-the-virtual-machines"></a>SR-IOV 用に構成された仮想マシンの実行の数は仮想マシンで使用できる仮想関数の数を超えることはできません。

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
*いないのに十分な仮想関数が使用できるシングル ルート I/O 仮想化 (SR-IOV) 用に構成された仮想マシンの実行の数。*  
  
## <a name="impact"></a>影響  
*ネットワークのパフォーマンスは、次の仮想マシンに最適でない可能性があります。*  
   
\<仮想マシンの一覧 >  
  
## <a name="resolution"></a>解決方法  
*SR-IOV 仮想機能を必要としない 1 つまたは複数の仮想マシンで SR-IOV を無効にすることを検討してください。*  
  


