---
title: 十分な量の動的 MAC アドレスを使用してサーバーを構成する
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: a2804519-9790-4006-80b6-e990a8f505fe
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 1fe7b34abc8be9777a491a08016627e7b2a66a2a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80862045"
---
# <a name="configure-the-server-with-a-sufficient-amount-of-dynamic-mac-addresses"></a>十分な量の動的 MAC アドレスを使用してサーバーを構成する

>適用対象: Windows Server 2016

*このトピックは、ベストプラクティスアナライザースキャンによって識別される特定の問題に対処することを目的としています。このトピックの情報は、Hyper-v ベストプラクティスアナライザーが実行されていて、このトピックで対処している問題が発生しているコンピューターにのみ適用する必要があります。ベストプラクティスとスキャンの詳細については、「ベストプラクティスアナライザー」を参照してください* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786)。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|［警告］|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
  
*使用可能な動的 MAC アドレスの数が不足しています。*  
  
## <a name="impact"></a>影響  
  
*動的 MAC アドレスが使用できない場合、動的 MAC アドレスを使用するように構成されたバーチャルマシンを起動することはできません。*  
  
## <a name="resolution"></a>解決方法  
  
*仮想スイッチマネージャーを使用して、動的アドレスの範囲を表示および拡張します。*  
  


