---
title: SR-IOV 対応のゲスト オペレーティング システムでサポートされている場合にのみを使用する仮想マシンの構成します。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 33cf5b68-e43e-47ef-adbc-6b266c1d4dce
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: e5c2acb21fe8b11e8f020c6d2ab1742116c23b28
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833363"
---
# <a name="configure-virtual-machines-to-use-sr-iov-only-when-supported-by-the-guest-operating-system"></a>SR-IOV 対応のゲスト オペレーティング システムでサポートされている場合にのみを使用する仮想マシンの構成します。

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、次を参照してください。 [Run Best Practices Analyzer Scans and Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177)します。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|警告|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*シングル ルート I/O 仮想化 (SR-IOV) を使用する 1 つまたは複数の仮想マシンが構成されているが、ゲスト オペレーティング システムは、SR-IOV をサポートしていません*  
  
## <a name="impact"></a>影響  
*SR-IOV 仮想機能を次の仮想マシンに割り当てられていません。*  
  
\<仮想マシンの一覧 >  
  
## <a name="resolution"></a>解決方法  
*SR-IOV をサポートしていないゲスト オペレーティング システムを実行するすべての仮想マシンで SR-IOV を無効にします。*  
  
SR-IOV は、いくつかの 64 ビット Windows ゲストでのみサポートされます。 詳細については、次を参照してください。[生成とゲストでの Hyper-v 機能の互換性](../Hyper-V-feature-compatibility-by-generation-and-guest.md)します。  
  


