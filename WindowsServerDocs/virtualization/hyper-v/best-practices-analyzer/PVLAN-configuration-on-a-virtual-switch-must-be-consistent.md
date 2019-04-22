---
title: 仮想スイッチ上 PVLAN 構成は、一貫性のあるである必要があります。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 4db63bcc-7a54-4f19-98a6-c274c3956d51
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: b7d6d068027aa9497b00138bd1d889ea86aa3308
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813253"
---
# <a name="pvlan-configuration-on-a-virtual-switch-must-be-consistent"></a>仮想スイッチ上 PVLAN 構成は、一貫性のあるである必要があります。

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、次を参照してください。 [Run Best Practices Analyzer Scans and Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177)します。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016| 
|**製品/機能**|Hyper-V|  
|**重要度**|エラー|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。
  
## <a name="issue"></a>**問題**  
*プライベート仮想ローカル エリア ネットワーク (PVLAN) は、1 つまたは複数の仮想ネットワーク アダプターで正しく構成されていません。*  
  
## <a name="impact"></a>**影響**  
*PVLAN では、仮想マシン間のネットワーク トラフィックを正しく特定可能性があります。*  
  
## <a name="resolution"></a>**解決方法**  
*PVLAN を正しく構成するのに、Windows PowerShell コマンドレット、Set-vmnetworkadaptervlan を使用します。*  
  


