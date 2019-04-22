---
title: すべての必須の仮想スイッチ拡張機能が使用できることを確認します。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 2f2f2698-f5ec-4cad-aa64-d6987e8142a1
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 53ceeb9aab6ca7196454fbcd7f0fdae8b34d05d2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825943"
---
# <a name="ensure-that-all-mandatory-virtual-switch-extensions-are-available"></a>すべての必須の仮想スイッチ拡張機能が使用できることを確認します。

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
*1 つまたは複数の仮想ネットワーク アダプターは、無効またはインストールされていない必須の拡張機能を仮想スイッチに接続されます。*  
  
## <a name="impact"></a>影響  
*次の仮想マシン上の 1 つまたは複数の仮想ネットワーク アダプターのネットワーク トラフィックがブロックされます。*  
  
\<仮想マシンの一覧 >  
  
## <a name="resolution"></a>解決方法  
*最初に、ホスト上に必須の拡張機能がインストールされているかどうかを確認し、必要な場合は、拡張機能をインストールします。次に、必須の拡張機能が無効になっている場合を使用して、仮想スイッチ マネージャーまたは Windows PowerShell コマンドレットは、有効にする VMSwitchExtension、拡張機能を有効にします。*  
  


