---
title: 動的 MAC アドレスのための十分な量で、サーバーを構成します。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: a2804519-9790-4006-80b6-e990a8f505fe
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: fc444225c38ef7e8605ec328cfe3f8184b2fd307
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870733"
---
# <a name="configure-the-server-with-a-sufficient-amount-of-dynamic-mac-addresses"></a>動的 MAC アドレスのための十分な量で、サーバーを構成します。

>適用先:Windows Server 2016

*このトピックではベスト プラクティス アナライザー スキャンで検知した特定の問題に対処するためのものです。このトピックの情報は、HYPER-V ベスト プラクティス アナライザーを実行する必要がありましたし、このトピックで取り上げて問題が発生しているコンピューターのみに適用してください。ベスト プラクティスとスキャンの詳細については、次を参照してください。* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786)します。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|警告|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
  
*使用可能な動的 MAC アドレスの数が少ないです。*  
  
## <a name="impact"></a>影響  
  
*動的 MAC アドレスが使用できない場合は、動的 MAC アドレスを使用するように構成する仮想マシンを開始できません。*  
  
## <a name="resolution"></a>解決方法  
  
*仮想スイッチ マネージャーを使用して、表示、および動的アドレスの範囲を拡張します。*  
  


