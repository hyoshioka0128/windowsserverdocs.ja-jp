---
title: バーチャルマシンのファイルを保存するファイル共有には、SMB プロトコルバージョン3.0 以降を使用してください。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 4bb832b8-f1aa-4c1f-a0f2-324dd53553ea
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 64c78c4725c84cbd02276cb2c0eadffae42d7060
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854195"
---
# <a name="use-at-least-smb-protocol-version-30-for-file-shares-that-store-files-for-virtual-machines"></a>バーチャルマシンのファイルを保存するファイル共有には、SMB プロトコルバージョン3.0 以降を使用してください。

>適用対象: Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|エラー|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>**問題**  
*仮想マシンファイルまたは仮想ハードディスクファイルは、SMB プロトコルバージョン3.0 以降をサポートしていないファイル共有に格納されます。*  
  
## <a name="impact"></a>**よる**  
*Microsoft では、この構成をサポートしていません。これは、次の仮想マシンに影響します。*  
  
仮想マシンの一覧を \<>  
  
## <a name="resolution"></a>**解決方法**  
*SMB プロトコルバージョン3.0 以降を使用しているファイル共有にファイルを移動します。*  
  


