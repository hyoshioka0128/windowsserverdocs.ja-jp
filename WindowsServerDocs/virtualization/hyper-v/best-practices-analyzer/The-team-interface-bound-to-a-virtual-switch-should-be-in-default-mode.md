---
title: 仮想スイッチにバインドされているチーム インターフェイスが既定のモードである必要があります。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 8c118e1e-865f-4cff-acdc-7c35e45d5da9
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 22e5ad0eed6e6ea07a83150762b76163442f2c5c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872163"
---
# <a name="the-team-interface-bound-to-a-virtual-switch-should-be-in-default-mode"></a>仮想スイッチにバインドされているチーム インターフェイスが既定のモードである必要があります。

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
*一部の仮想スイッチがチーム インターフェイスにバインドされますが、チーム インターフェイスは、すべての Vlan でトラフィックを仮想スイッチに合格しなかった。*  
  
## <a name="impact"></a>**影響**  
*次の仮想スイッチは、すべての Vlan へのアクセスを持つことはできません \n。{0}*  
  
## <a name="resolution"></a>**解決方法**  
*サーバー マネージャーを使用してまたは Windows PowerShell のコマンドレット セット NetLbfoTeamNic チーム インターフェイスの既定のモードにリセットします。*  
  


