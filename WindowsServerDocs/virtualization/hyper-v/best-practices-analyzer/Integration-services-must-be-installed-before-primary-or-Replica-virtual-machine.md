---
title: 統合サービスは、プライマリの前にインストールする必要がありますか、レプリカ仮想マシンは、フェールオーバー後に代替の IP アドレスを使用することができます。
description: 詳細情報へのリンクで、このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: a7fdd185-d6c8-4f58-9b58-2df5827bb056
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 1ff8dbfd71655aee86ba7d0feac87ec2267a2171
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865513"
---
# <a name="integration-services-must-be-installed-before-primary-or-replica-virtual-machines-can-use-an-alternate-ip-address-after-a-failover"></a>統合サービスは、プライマリの前にインストールする必要がありますか、レプリカ仮想マシンは、フェールオーバー後に代替の IP アドレスを使用することができます。

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、次を参照してください。 [Run Best Practices Analyzer Scans and Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177)します。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|エラー|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*レプリケーションに参加している仮想マシンは、フェールオーバーが発生した場合、特定の IP アドレスを使用するように構成が仮想マシンのゲスト オペレーティング システムで統合サービスがインストールされている場合にのみできます。*  
  
## <a name="impact"></a>影響  
*フェールオーバー (計画された、計画されていない、またはテスト) の場合、レプリカ仮想マシンがオンライン プライマリ仮想マシンと同じ IP アドレスを使用します。この構成では、接続の問題を引き起こす可能性があります。これには、次の仮想マシンに影響します。*  
  
\<仮想マシンの一覧 >  
  
## <a name="resolution"></a>解決方法  
*仮想マシンで統合サービスをインストールするには、仮想マシンの接続を使用します。*  
  
Windows Server 2016 の時点では、Windows 仮想マシン用の統合サービスは、Windows Update を通じて配信されます。 Integration services の最新バージョンを取得する Windows 更新プログラムを受信するこれらの仮想マシンが構成されていることを確認します。 Linux カーネルは、ここで Linux integration services (LIS) が含まれていて、新しいリリースでは更新されましたが、古いカーネルに基づく Linux ディストリビューションは、最新の機能強化または修正プログラムがない可能性が。 詳細については、次を参照してください。 [Windows 上の Hyper-v ではサポートされている Linux および FreeBSD の仮想マシン](../Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)します。


