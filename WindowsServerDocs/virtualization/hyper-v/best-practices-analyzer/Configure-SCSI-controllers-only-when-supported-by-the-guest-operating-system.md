---
title: ゲストオペレーティングシステムでサポートされている場合にのみ SCSI コントローラーを構成する
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 861f194f-467e-4b07-a1c5-55b35f6327c4
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: cf206d9568ef7634d724f3fce450985c34ebfac5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80862165"
---
# <a name="configure-scsi-controllers-only-when-supported-by-the-guest-operating-system"></a>ゲストオペレーティングシステムでサポートされている場合にのみ SCSI コントローラーを構成する

>適用対象: Windows Server 2016


  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|［警告］|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
  
*ゲストオペレーティングシステムが SCSI コントローラーをサポートしていないため、バーチャルマシンには使用できない SCSI コントローラーが構成されています。*  
  
## <a name="impact"></a>影響  
  
*バーチャルマシンは、SCSI コントローラーに接続された記憶域を使用できません。これは、次の仮想マシンに影響します。*  
  
仮想マシンの一覧を \<>  
  
## <a name="resolution"></a>解決方法  
  
*バーチャルマシンをシャットダウンし、Hyper-v マネージャーを使用してバーチャルマシンから SCSI コントローラーを削除します。次に、仮想マシンを再起動します。*  
  


