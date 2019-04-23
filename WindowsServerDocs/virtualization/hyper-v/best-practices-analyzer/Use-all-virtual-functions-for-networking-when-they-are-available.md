---
title: 利用可能なネットワークのすべての仮想関数を使用します。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: bf895484-6a0d-4aa4-9a42-9fac739e875d
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 3ad120ffa689f1f7dcae832432e216ebda57e62f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877793"
---
# <a name="use-all-virtual-functions-for-networking-when-they-are-available"></a>利用可能なネットワークのすべての仮想関数を使用します。

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
*いくつかのハードウェア アクセラレーション機能が使用されません。*  
  
## <a name="impact"></a>影響  
*この構成は必要以上に高くする全体的な CPU の使用率を引き起こす可能性があります。ネットワークのパフォーマンスは、次の仮想マシンに最適でない可能性があります。*  
  
\<仮想マシンの一覧 >  
  
## <a name="resolution"></a>解決方法  
*SR-IOV と仮想マシンで必要なネットワーク機能と、この構成が競合しないかどうかは、物理ハードウェアがサポートしている場合は、SR-IOV 対応の仮想ネットワーク アダプターを構成することを検討してください。*  
  


