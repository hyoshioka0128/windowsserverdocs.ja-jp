---
title: ゲスト オペレーティング システムでサポートされている場合にのみ、SCSI コント ローラーを構成します。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 861f194f-467e-4b07-a1c5-55b35f6327c4
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 3dc48602ab6c71c60fdb734ca98cf1359f58d87c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830393"
---
# <a name="configure-scsi-controllers-only-when-supported-by-the-guest-operating-system"></a>ゲスト オペレーティング システムでサポートされている場合にのみ、SCSI コント ローラーを構成します。

>適用先:Windows Server 2016


  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|警告|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
  
*仮想マシンは、ゲスト オペレーティング システムが SCSI コント ローラーをサポートしていないために使用することはできません、SCSI コント ローラーで構成されます。*  
  
## <a name="impact"></a>影響  
  
*仮想マシンは SCSI コント ローラーに接続されているストレージを使用できません。これには、次の仮想マシンに影響します。*  
  
\<仮想マシンの一覧 >  
  
## <a name="resolution"></a>解決方法  
  
*仮想マシンをシャット ダウンし、HYPER-V マネージャーを使用して、仮想マシンから SCSI コント ローラーを削除します。仮想マシンを再起動します。*  
  


