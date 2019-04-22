---
title: 仮想 SAN が物理ホスト バス アダプターを関連付ける必要があります。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 14bca69b-e779-4e90-b5c1-1b015625572f
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 3b9ca1e2da1cf9f4410f465fe95c6cc9c0b07ffc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819083"
---
# <a name="a-virtual-san-should-be-associated-with-a-physical-host-bus-adapter"></a>仮想 SAN が物理ホスト バス アダプターを関連付ける必要があります。

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
*仮想記憶域エリア ネットワーク (SAN) は、ホスト バス アダプター (HBA) への関連付けなしに構成されています。*  
  
## <a name="impact"></a>**影響**  
*仮想マシンは、正しく構成されていない仮想 SAN に接続された仮想ファイバー チャネル アダプターで構成されているときの開始は失敗します。次の仮想 San に影響を与えます。*  
  
  
\<仮想 San の一覧 >  
  
  
## <a name="resolution"></a>**解決方法**  
*ホスト バス アダプターに接続して、仮想 SAN を再構成します。*  
  
  
  


