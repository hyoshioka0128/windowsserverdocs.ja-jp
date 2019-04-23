---
title: 1 つまたは複数のネットワーク アダプターは、ポート ミラーリングのソースとして構成する必要があります。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 147fd00f-1440-44d1-94e3-3a8af63aa7ed
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 0843c1f302b96d334e8d6649ac5503bbe2b12d02
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831793"
---
# <a name="one-or-more-network-adapters-should-be-configured-as-the-source-for-port-mirroring"></a>1 つまたは複数のネットワーク アダプターは、ポート ミラーリングのソースとして構成する必要があります。

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
*1 つまたは複数の仮想マシンは、ポート ミラーリングを変換先として構成されているネットワーク アダプターが仮想スイッチに対応するソースはありません。*  
  
## <a name="impact"></a>**影響**  
*ポート ミラーリングは、次の仮想スイッチと仮想マシンは正しく機能しません。*  
  
\<仮想マシンの一覧 >  
  
## <a name="resolution"></a>**解決方法**  
*完了またはポート ミラーリングの構成を修正するには、Windows PowerShell または HYPER-V マネージャーを使用します。*  
  


