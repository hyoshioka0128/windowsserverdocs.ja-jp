---
title: 親と子の仮想ハード_ディスクが別々 のボリューム上にある場合は、差分仮想ハード_ディスクを使用する場合は、記憶域サービスの品質を有効にしないように
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: aa9ed408-65cf-40dc-aad2-118b54c70179
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 2bdc8462c4d9dc50dbb69792f2f294add0ca3a74
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856203"
---
# <a name="avoid-enabling-storage-quality-of-service-when-using-a-differencing-virtual-hard-disk-when-the-parent-and-child-virtual-hard-disks-are-on-different-volumes"></a>親と子の仮想ハード_ディスクが別々 のボリューム上にある場合は、差分仮想ハード_ディスクを使用する場合は、記憶域サービスの品質を有効にしないように

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
*別のボリュームの親と子の仮想ハード ディスクでは差分仮想ハード_ディスクが、記憶域サービスの品質を有効にします。*  
  
## <a name="impact"></a>**影響**  
*この構成は、予期しないストレージ差分仮想ハード ディスクとその他のバーチャル ハード_ディスク、親と子のボリュームでのサービスの品質の動作があります。これは、次に影響仮想ハード ディスク。*  
  
\<仮想ハード ディスクの一覧 >  
  
## <a name="resolution"></a>**解決方法**  
*参照先の仮想ハード ディスク上の記憶域サービスの品質を無効にするか、または親と子の仮想ハード_ディスクを同じボリュームに移動する記憶域の移行を実行します。*  
  


