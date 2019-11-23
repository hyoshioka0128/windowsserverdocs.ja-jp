---
title: レプリケーションには証明書ベースの認証を使用することをお勧めします。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: d931cc57-414f-4bdf-9ebd-08fd5e22b19d
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 0eac99fddd8bbc6dc585931cd25f2a440be16c76
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365180"
---
# <a name="certificate-based-authentication-is-recommended-for-replication"></a>レプリケーションには証明書ベースの認証を使用することをお勧めします。

>適用対象: Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|Warning|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>**問題**  
*レプリケーション用に選択された1つ以上の仮想マシンが、Kerberos 認証用に構成されています。*  
  
## <a name="impact"></a>**よる**  
*プライマリサーバーからレプリケーションサーバーへのレプリケーションネットワークトラフィックは暗号化されていません。これは、次の仮想マシンに影響します。*  
  
仮想マシンの一覧を \<>  
  
## <a name="resolution"></a>**解決方法**  
*暗号化を実行するために別の方法が使用されている場合は、無視してかまいません。それ以外の場合は、仮想マシンの設定を変更して、証明書ベースの認証を選択します。*  
  


