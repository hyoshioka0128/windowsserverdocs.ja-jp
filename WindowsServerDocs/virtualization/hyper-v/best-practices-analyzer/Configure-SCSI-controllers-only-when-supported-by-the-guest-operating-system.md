---
title: ゲストオペレーティングシステムでサポートされている場合にのみ SCSI コントローラーを構成する
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 861f194f-467e-4b07-a1c5-55b35f6327c4
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: da8d929a8f06f58610913d28d2f1e90299efb235
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366419"
---
# <a name="configure-scsi-controllers-only-when-supported-by-the-guest-operating-system"></a>ゲストオペレーティングシステムでサポートされている場合にのみ SCSI コントローラーを構成する

>適用先:Windows Server 2016


  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|警告|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
  
*ゲストオペレーティングシステムが SCSI コントローラーをサポートしていないため、バーチャルマシンには使用できない SCSI コントローラーが構成されています。*  
  
## <a name="impact"></a>影響  
  
@no__t 0Virtual machines では、SCSI コントローラーに接続された記憶域を使用できません。これは、次の仮想マシンに影響します: *  
  
@no__t-仮想マシンの > の一覧  
  
## <a name="resolution"></a>解決方法  
  
*Shut machine をシャットダウンし、Hyper-v マネージャーを使用してバーチャルマシンから SCSI コントローラーを削除します。次に、仮想マシンを再起動します。*  
  


