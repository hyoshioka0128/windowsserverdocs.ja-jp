---
title: 記憶域コント ローラーは仮想マシンで接続された記憶域にアクセスできるように有効にする必要があります。
description: このベスト プラクティス アナライザー ルールによって報告された問題を解決する方法を説明します。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 532548a1-8ffe-4b5b-902e-ed2f0819012b
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 42803a0eef84bf006e9f9e7ed6297ea21b4eb7b1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849163"
---
# <a name="storage-controllers-should-be-enabled-in-virtual-machines-to-provide-access-to-attached-storage"></a>記憶域コント ローラーは仮想マシンで接続された記憶域にアクセスできるように有効にする必要があります。

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、「 [ベスト プラクティス アナライザー](https://go.microsoft.com/fwlink/?LinkId=122786)」をご覧ください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|警告|  
|**カテゴリ**|構成|  

次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。

## <a name="issue"></a>問題  
  
*1 つまたは複数の記憶域コント ローラーは、仮想マシンで無効にすることがあります。*  
  
## <a name="impact"></a>影響  
  
*仮想マシンには、無効化された記憶域コント ローラーに接続されている記憶域を使用できません。これには、次の仮想マシンに影響します。*  
  
\<仮想マシン名の一覧 >  
  
## <a name="resolution"></a>解決方法  
  
*ゲスト オペレーティング システムでデバイス マネージャーを使用して、すべての記憶域コント ローラーを有効にします。記憶域コント ローラーが必要ない場合は、HYPER-V マネージャーを使用して、仮想マシンから削除します。*  
  
デバイス マネージャーを使用する方法については、ゲスト オペレーティング システムのヘルプを参照してください。 記憶域コント ローラーを削除する方法については、次の手順を参照してください。  
  
#### <a name="to-remove-a-scsi-storage-controller-from-the-virtual-machine"></a>仮想マシンから SCSI 記憶域コント ローラーを削除するには  
  
1.  Hyper-V マネージャーを開きます。 **[スタート]** ボタンをクリックし、**[管理ツール]** をポイントして **[Hyper-V マネージャー]** をクリックします。  
  
2.  結果ウィンドウで  **仮想マシン**, 、構成する仮想マシンを選択します。  
  
3.  仮想マシンが実行されている場合は、仮想マシンをシャット ダウンします。 仮想マシンを右クリックし、をクリックして**シャット ダウン**します。  
  
4.  **アクション** ウィンドウの 仮想マシン名をクリックして **設定**します。  
  
5.  左側のウィンドウで、**設定**ダイアログ ボックスで、**ハードウェア**、 をクリックして**SCSI コント ローラー**します。  
  
6.  右側のウィンドウで次のようにクリックします。**削除**します。  
  


