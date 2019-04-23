---
title: 外部仮想スイッチにバインドされている VMQ 対応の物理ネットワーク アダプターで VMQ を有効にする必要があります。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 93d1b155-bf44-46b0-bb69-d34d5b30e574
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 9a552c15675e6ca7a7310c8c9eaec883653987be
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889473"
---
# <a name="vmq-should-be-enabled-on-vmq-capable-physical-network-adapters-bound-to-an-external-virtual-switch"></a>外部仮想スイッチにバインドされている VMQ 対応の物理ネットワーク アダプターで VMQ を有効にする必要があります。

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、次を参照してください。 [Run Best Practices Analyzer Scans and Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177)します。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|警告|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>**問題**  
*次のネットワーク アダプターが仮想マシン キュー (VMQ) が、機能が無効になっています。*  
  
## <a name="impact"></a>**影響**  
*Windows は活用するために使用できるハードウェア オフロードの次のネットワーク アダプターにできません。*  
  
\<ネットワーク アダプターの一覧 >  
  
## <a name="resolution"></a>**解決方法**  
*VMQ NetAdapterVmq Windows PowerShell コマンドレットを使用して、またはネットワーク アダプターのプロパティの高度なユーザー インターフェイスを使用して有効にします。*  
  


