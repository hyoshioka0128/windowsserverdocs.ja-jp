---
title: 仮想マシンのファイルを格納するファイル共有での継続的な可用性を実現するように構成された SMB プロトコルバージョン3.0 以降を使用する
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: a1fa5cf9-8a48-4f63-bb57-d81e63e77b30
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 3a6cbb6052e2e50b7fd78792c5e01885d7672932
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393339"
---
# <a name="use-at-least-smb-protocol-version-30-configured-for-continuous-availability-on-file-shares-that-store-files-for-virtual-machines"></a>仮想マシンのファイルを格納するファイル共有での継続的な可用性を実現するように構成された SMB プロトコルバージョン3.0 以降を使用する

>適用対象: Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|Warning|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>**問題**  
*バーチャルマシンファイルまたはバーチャルハードディスクファイルは、SMB プロトコルバージョン3.0 の継続的可用性機能が構成されていないネットワークファイル共有に保管されます。*  
  
## <a name="impact"></a>**よる**  
*この構成は、サーバーを使用した仮想マシンの可用性に影響を与える可能性があるため、Microsoft は推奨しません。これは、次の仮想マシンに影響します。*  
  
仮想マシンの一覧を \<>  
  
## <a name="resolution"></a>**解決方法**  
次のいずれかの操作を行います。  
  
-   継続的な可用性を確保するように構成されている SMB 3.0 ファイル共有にファイルを移動します。  
  
-   現在のファイル共有を再構成して、継続的な可用性を提供します。  
  


