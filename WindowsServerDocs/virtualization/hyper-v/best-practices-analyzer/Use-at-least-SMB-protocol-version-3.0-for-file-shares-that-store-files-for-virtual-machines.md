---
title: バーチャルマシンのファイルを保存するファイル共有には、SMB プロトコルバージョン3.0 以降を使用してください。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 4bb832b8-f1aa-4c1f-a0f2-324dd53553ea
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: af23c3c860a47d0dd9096bc3f5ff466aca7836b6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393323"
---
# <a name="use-at-least-smb-protocol-version-30-for-file-shares-that-store-files-for-virtual-machines"></a>バーチャルマシンのファイルを保存するファイル共有には、SMB プロトコルバージョン3.0 以降を使用してください。

>適用先:Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|Error|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>**問題**  
*仮想マシンファイルまたは仮想ハードディスクファイルは、SMB プロトコルバージョン3.0 以降をサポートしていないファイル共有に格納されます。*  
  
## <a name="impact"></a>**よる**  
*Microsoft では、この構成をサポートしていません。これは、次の仮想マシンに影響します:*  
  
@no__t-仮想マシンの > の一覧  
  
## <a name="resolution"></a>**解決方法**  
*SMB プロトコルバージョン3.0 以降を使用しているファイル共有にファイルを移動します。*  
  


