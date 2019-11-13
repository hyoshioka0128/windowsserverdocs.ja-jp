---
title: スマートページングファイルをシステムディスクに保存しない
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 9b57c9b8-76c5-43c7-bfa6-2c95b3cb6510
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: e3ddb662d14545693e26eb680527d93eb65d5d13
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365241"
---
# <a name="avoid-storing-smart-paging-files-on-a-system-disk"></a>スマートページングファイルをシステムディスクに保存しない

>適用対象: Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|Warning|  
|**カテゴリ**|運用|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示されるテキストを示します。  
  
## <a name="issue"></a>問題  
*仮想マシンが再起動され、スマートページングファイル用に指定された場所が Hyper-v を実行するサーバーのシステムディスクである場合、1つまたは複数の仮想マシンのメモリ構成でスマートページングを使用することが必要になる場合があります。*  
  
## <a name="impact"></a>影響  
*システムディスクをスマートページングに使用すると、Hyper-v を実行しているサーバーで問題が発生する可能性があります。これは、次の仮想マシンに影響します。*  
  
仮想マシンの一覧を \<>  
  
## <a name="resolution"></a>解決方法  
*非システムディスクにスマートページングファイルを格納するように仮想マシンを再構成します。*  
  


