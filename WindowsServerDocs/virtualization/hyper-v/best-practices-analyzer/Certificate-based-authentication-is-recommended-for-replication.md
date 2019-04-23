---
title: 証明書ベースの認証はレプリケーションをお勧めします。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: d931cc57-414f-4bdf-9ebd-08fd5e22b19d
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 5bd131b48b009b43b6379f72f370b4179dea5a03
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873063"
---
# <a name="certificate-based-authentication-is-recommended-for-replication"></a>証明書ベースの認証はレプリケーションをお勧めします。

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
*レプリケーション用に選択された 1 つまたは複数の仮想マシンは、Kerberos 認証用に構成されます。*  
  
## <a name="impact"></a>**影響**  
*レプリケーション サーバーへのプライマリ サーバーからレプリケーションのネットワーク トラフィックは暗号化されません。これには、次の仮想マシンに影響します。*  
  
\<仮想マシンの一覧 >  
  
## <a name="resolution"></a>**解決方法**  
*暗号化を実行する別の方法が使用されている場合は、これを無視できます。それ以外の場合、証明書ベースの認証を選択する仮想マシンの設定を変更します。*  
  


