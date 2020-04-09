---
title: 仮想スイッチにバインドされているチーム インターフェイスが既定のモードである必要があります。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 8c118e1e-865f-4cff-acdc-7c35e45d5da9
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: fe19de5dd380d08c01c917da9d4e2ef9465de042
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854605"
---
# <a name="the-team-interface-bound-to-a-virtual-switch-should-be-in-default-mode"></a>仮想スイッチにバインドされているチーム インターフェイスが既定のモードである必要があります。

>適用対象: Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|［警告］|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>**問題**  
*一部の仮想スイッチはチームインターフェイスにバインドされていますが、チームインターフェイスは、すべての Vlan 上のトラフィックを仮想スイッチに渡しません。*  
  
## <a name="impact"></a>**よる**  
*次の仮想スイッチは、すべての Vlan にアクセスすることはできません: \n{0}*  
  
## <a name="resolution"></a>**解決方法**  
*サーバーマネージャーまたは Windows PowerShell コマンドレット NetLbfoTeamNic を使用して、チームインターフェイスを既定のモードにリセットします。*  
  


