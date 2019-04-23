---
title: SR-IOV を使用する仮想マシンが構成されている場合、仮想関数のドライバーが正しく動作することを確認します。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: d21e4b93-29bf-423a-a635-71c6d48dc49e
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 8d3d0a5008b55d4823cef9a8dd2a7bce4a6a2a33
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852083"
---
# <a name="ensure-that-the-virtual-function-driver-operates-correctly-when-a-virtual-machine-is-configured-to-use-sr-iov"></a>SR-IOV を使用する仮想マシンが構成されている場合、仮想関数のドライバーが正しく動作することを確認します。

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
*仮想関数のドライバーが 1 つまたは複数の仮想マシンのゲスト オペレーティング システムで正しく動作しません。*  
  
## <a name="impact"></a>影響  
*ネットワークのパフォーマンスは、次の仮想マシンに最適ではありません。*  
  
\<仮想マシンの一覧 >  
  
## <a name="resolution"></a>解決方法  
*ゲスト オペレーティング システムで、次の操作を行います。適切なドライバーがインストールされていることとすべてのネットワーク デバイスを有効にし、エラーまたは警告のイベント ログを確認を確認します。*  
  


