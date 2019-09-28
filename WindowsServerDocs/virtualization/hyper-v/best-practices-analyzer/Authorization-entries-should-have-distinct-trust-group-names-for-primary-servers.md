---
title: 承認エントリには、同じ信頼グループに属していない仮想マシンを持つプライマリサーバーに対して、異なる信頼グループ名を付ける必要があります。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 8827a3a7-9f3c-4f51-826a-8e2ec43e01df
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: ab71e0e6562b73d81b871914fd0e9e76570c518e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366538"
---
# <a name="authorization-entries-should-have-distinct-trust-group-names-for-primary-servers-with-virtual-machines-that-are-not-part-of-the-same-trust-group"></a>承認エントリには、同じ信頼グループに属していない仮想マシンを持つプライマリサーバーに対して、異なる信頼グループ名を付ける必要があります。

>適用先:Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|警告|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>**問題**  
*サーバーは、仮想マシンと同じレプリケーションタグに関連付けられている承認リスト内の任意のサーバーから、レプリカ仮想マシンへのレプリケーション要求を受け入れます。*  
  
## <a name="impact"></a>**よる**  
@no__t、異なる承認エントリに属するプライマリサーバーからのレプリケーションを受け入れる仮想マシンでは、プライバシーとセキュリティの問題が発生する可能性があります。これは、次の承認エントリに影響します: @no__t-> 承認エントリの一覧 *  
  
## <a name="resolution"></a>**解決方法**  
@no__t は、同じセキュリティグループに属していない仮想マシンを使用して、プライマリサーバーの承認エントリで異なるタグを使用します。Hyper-v の設定を変更して、レプリケーションタグを構成してください。 *  
  


