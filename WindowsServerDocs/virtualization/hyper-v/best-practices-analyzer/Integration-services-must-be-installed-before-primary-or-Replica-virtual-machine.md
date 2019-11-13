---
title: 統合サービスは、プライマリの前にインストールする必要がありますか、レプリカ仮想マシンは、フェールオーバー後に代替の IP アドレスを使用することができます。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。詳細情報へのリンクがあります。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: a7fdd185-d6c8-4f58-9b58-2df5827bb056
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 58e744c182fb2013e55e91f58140c6ba14181f9f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393593"
---
# <a name="integration-services-must-be-installed-before-primary-or-replica-virtual-machines-can-use-an-alternate-ip-address-after-a-failover"></a>統合サービスは、プライマリの前にインストールする必要がありますか、レプリカ仮想マシンは、フェールオーバー後に代替の IP アドレスを使用することができます。

>適用対象: Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|エラー|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*レプリケーションに参加している仮想マシンは、フェールオーバーが発生した場合に特定の IP アドレスを使用するように構成できますが、仮想マシンのゲストオペレーティングシステムに統合サービスがインストールされている場合に限られます。*  
  
## <a name="impact"></a>影響  
*フェールオーバー (計画済み、計画外、またはテスト) が発生した場合、レプリカ仮想マシンは、プライマリ仮想マシンと同じ IP アドレスを使用してオンラインになります。この構成により、接続の問題が発生する可能性があります。これは、次の仮想マシンに影響します。*  
  
仮想マシンの一覧を \<>  
  
## <a name="resolution"></a>解決方法  
*仮想マシンに統合サービスをインストールするには、仮想マシン接続を使用します。*  
  
Windows Server 2016 の時点では、Windows 仮想マシン用の統合サービスは、Windows Update を通じて配信されます。 Integration services の最新バージョンを取得する Windows 更新プログラムを受信するこれらの仮想マシンが構成されていることを確認します。 Linux カーネルは、ここで Linux integration services (LIS) が含まれていて、新しいリリースでは更新されましたが、古いカーネルに基づく Linux ディストリビューションは、最新の機能強化または修正プログラムがない可能性が。 詳細については、「 [Windows 上の hyper-v でサポートされている Linux および FreeBSD 仮想マシン](../Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)」を参照してください。


