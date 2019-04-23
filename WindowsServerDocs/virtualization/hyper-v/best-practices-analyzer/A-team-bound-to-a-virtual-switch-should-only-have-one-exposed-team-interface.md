---
title: 仮想スイッチにバインドされているチームは、公開されているチーム インターフェイスの 1 つのみにあります。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 1074f086-1a2e-42e1-b58c-f55e657d5ce1
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 108bbec1439959bb7ab4475b59c7231653952ea8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838463"
---
# <a name="a-team-bound-to-a-virtual-switch-should-only-have-one-exposed-team-interface"></a>仮想スイッチにバインドされているチームは、公開されているチーム インターフェイスの 1 つのみにあります。

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
*1 つまたは複数の仮想スイッチは、複数のチームのインターフェイスがあるチームにバインドされます。*  
  
## <a name="impact"></a>**影響**  
*次の仮想スイッチは Vlan とその他のチームのインターフェイスで使用される帯域幅へのアクセスがありません。*  
  
\<仮想スイッチの一覧 >  
  
## <a name="resolution"></a>**解決方法**  
*既定のチーム インターフェイス以外のチームからチームのすべてのインターフェイスを削除するのにには、削除 NetLbfoTeamNic の Windows PowerShell コマンドレットを使用します。*  
  


