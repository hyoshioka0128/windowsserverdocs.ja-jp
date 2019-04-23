---
title: 仮想マシン用に構成されたすべての仮想ネットワーク アダプターを有効にします。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: fcd350b7-4240-4359-aadd-93e7ac4d314e
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: fbb1ef5283f6ccf8dfa355a09a86040be80f53e9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844233"
---
# <a name="enable-all-virtual-network-adapters-configured-for-a-virtual-machine"></a>仮想マシン用に構成されたすべての仮想ネットワーク アダプターを有効にします。

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
  
*仮想マシンでは、1 つまたは複数のネットワーク アダプターを無効にすることがあります。*  
  
## <a name="impact"></a>影響  
  
*次の仮想マシンは、ネットワーク接続をいない可能性があります。*  
  
\<仮想マシン名の一覧 >  
  
## <a name="resolution"></a>解決方法  
  
*ゲスト オペレーティング システムでデバイス マネージャーを使用して、すべての仮想ネットワーク アダプターを有効にします。アダプターが必要ない場合は、HYPER-V マネージャーを使用して、仮想マシンから削除します。*  
  


