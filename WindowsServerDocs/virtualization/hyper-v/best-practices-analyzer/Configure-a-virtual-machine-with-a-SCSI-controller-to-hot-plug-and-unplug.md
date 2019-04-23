---
title: プラグをホット ストレージ層とホット ストレージを取り外しできる SCSI コント ローラーと仮想マシンの構成します。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 511e1172-aeef-463d-b5dd-2bffae411ff1
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 755e7485e54ee58e0acd7ebd75a7ee591aa655f9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843283"
---
# <a name="configure-a-virtual-machine-with-a-scsi-controller-to-be-able-to-hot-plug-and-hot-unplug-storage"></a>プラグをホット ストレージ層とホット ストレージを取り外しできる SCSI コント ローラーと仮想マシンの構成します。

>適用先:Windows Server 2016


  
*ベスト プラクティスとスキャンの詳細については、次を参照してください。* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786)します。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|警告|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
  
*SCSI コント ローラーでない構成される仮想マシンが検出されました。*  
  
## <a name="impact"></a>影響  
  
*プラグをホット、またはホット次の仮想マシンの記憶域を取り外すことはできません。*  
  
\<仮想マシン名の一覧 >  
  
プラグをホット、またはホット ストレージを取り外すことにより、ダウンタイムを必要とせず、仮想マシンの記憶域のニーズを管理しやすくします。 追加したり記憶域を削除する前に、SCSI コント ローラーなしの仮想マシンをシャット ダウンする必要があります。  
  
## <a name="resolution"></a>解決方法  
  
*ホット プラグまたはホットこの仮想マシンの記憶域を取り外す必要がない場合のアクションは必要ありません。それ以外の場合、仮想マシンをシャット ダウンし、構成に SCSI コント ローラーを追加します。*  
  
ホット プラグに SCSI コント ローラーを使用して、ホット ストレージを取り外しするには、ゲスト オペレーティング システムを現在のバージョンの integration services 実行する必要があります。  
  


