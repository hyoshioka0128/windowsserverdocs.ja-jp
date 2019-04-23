---
title: シリアル ポートが第 2 世代仮想マシンで構成します。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 87061193-dd3f-4398-aa5d-4cee83cadfa3
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 58c3fc5f975b85ce17ac5f7cca4930ec9e851e07
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877383"
---
# <a name="serial-ports-should-not-be-configured-on-generation-2-virtual-machines"></a>シリアル ポートが第 2 世代仮想マシンで構成します。

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
*1 つまたは複数の世代 2 の仮想マシンがあるシリアル ポートを構成します。*  
  
## <a name="impact"></a>**影響**  
*次の仮想マシンのパフォーマンスに影響する可能性があります。*  
  
\<仮想マシンの一覧 >  
  
## <a name="resolution"></a>**解決方法**  
*これが意図的な場合は、これ以上の操作は必要ありません。それ以外の場合、HYPER-V マネージャーまたは Windows PowerShell を使用して、仮想マシンのシリアル ポートからの接続文字列を削除するを検討してください。*  
  


