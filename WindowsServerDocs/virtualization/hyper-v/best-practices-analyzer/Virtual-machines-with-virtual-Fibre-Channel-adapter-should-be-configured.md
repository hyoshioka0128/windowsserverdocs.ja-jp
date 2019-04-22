---
title: 仮想ファイバー チャネル アダプターで構成された仮想マシンをファイバー チャネル ベースの記憶域を高可用性を構成してください。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 73127bdd-8086-4268-a93c-2fdf1623e91b
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 203477a022f7c5f819ef7b99f1b8e37a0b8b0a9f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816943"
---
# <a name="virtual-machines-configured-with-a-virtual-fibre-channel-adapter-should-be-configured-for-high-availability-to-the-fibre-channel-based-storage"></a>仮想ファイバー チャネル アダプターで構成された仮想マシンをファイバー チャネル ベースの記憶域を高可用性を構成してください。

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、次を参照してください。 [Run Best Practices Analyzer Scans and Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177)します。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|情報|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。
  
## <a name="issue"></a>**問題**  
*1 つまたは複数の仮想マシンでは、これらの仮想マシンが 1 つだけのホスト バス アダプター (HBA) に接続されている仮想ファイバー チャネル アダプターで構成されているために、ファイバー チャネル ベース記憶域への接続を高可用性が不足しています。*  
  
## <a name="impact"></a>**影響**  
*ホスト バス アダプターの障害は、記憶域と仮想マシン間のファイバー チャネル接続をブロック可能性があります。これには、次の仮想マシンに影響します。*  
  
\<仮想マシンの一覧 >  
  
## <a name="resolution"></a>**解決方法**  
*仮想マシンからホスト バス アダプターに別の接続を追加し、冗長ファイバー チャネル接続を確立するためにゲスト オペレーティング システムでマルチパス I/O (MPIO) を構成します。*  
  


