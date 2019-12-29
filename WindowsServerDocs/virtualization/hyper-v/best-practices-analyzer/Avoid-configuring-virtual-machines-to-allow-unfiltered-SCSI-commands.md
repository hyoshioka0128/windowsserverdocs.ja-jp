---
title: フィルター処理される SCSI コマンドを許可するようにバーチャルマシンを構成しない
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: dd4a3d78-a77f-451e-a383-d5cf45ea17cf
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 5deb20862ed0e359febd4a9b58202d53c85058ca
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365270"
---
# <a name="avoid-configuring-virtual-machines-to-allow-unfiltered-scsi-commands"></a>フィルター処理される SCSI コマンドを許可するようにバーチャルマシンを構成しない

>適用対象: Windows Server 2016


  
*ベストプラクティスとスキャンの詳細については、「* [ベストプラクティスアナライザー](https://go.microsoft.com/fwlink/?LinkId=122786)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|Warning|  
|**カテゴリ**|運用|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
  
*フィルター処理されていない SCSI コマンドを許可するようにバーチャルマシンが構成されています。*  
  
## <a name="impact"></a>影響  
  
*SCSI コマンドフィルターをバイパスすると、セキュリティ上のリスクが生じます。この構成は、ゲストオペレーティングシステムで実行されているストレージアプリケーションとの互換性を確保するために必要な場合にのみ有効にしてください。次のバーチャルマシンは、フィルター処理されていない SCSI コマンドを許可するように構成されています:*  
  
仮想マシン名の \<一覧 >  
  
## <a name="resolution"></a>解決方法  
  
*この構成が必要かどうかを判断するには、記憶域のベンダーに問い合わせてください。また、管理オペレーティングシステムまたはその他のゲストオペレーティングシステムが侵害されたり、通常とは異なる動作が発生したりした場合は、コマンドをブロックするようにバーチャルマシンを再構成します。*  
  


