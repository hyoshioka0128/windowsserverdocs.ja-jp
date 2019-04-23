---
title: 仮想ハード ディスク ファイルが格納される物理記憶域のセクター サイズ未満のセクター サイズの仮想ハード_ディスクを使用しないでください。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: b7cf994e-bf4b-4b1b-bad6-ecf7d46d105e
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: b6ec2e0995180ecf9ae5986447fdd460a1c7a337
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59846263"
---
# <a name="avoid-using-virtual-hard-disks-with-a-sector-size-less-than-the-sector-size-of-the-physical-storage-that-stores-the-virtual-hard-disk-file"></a>仮想ハード ディスク ファイルが格納される物理記憶域のセクター サイズ未満のセクター サイズの仮想ハード_ディスクを使用しないでください。

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、次を参照してください。 [Run Best Practices Analyzer Scans and Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177)します。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング** <br />**システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|警告|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>**問題**  
*1 つまたは複数の仮想ハード_ディスクがバーチャル ハード ディスク ファイルが配置されている記憶域の物理セクター サイズ未満の物理セクター サイズであること。*  
  
## <a name="impact"></a>**影響**  
*仮想マシンまたはバーチャル ハード_ディスクを使用して、アプリケーションでパフォーマンスの問題があります。これには、次の仮想マシンに影響します。*  
  
\<仮想マシンの一覧 >  
  
## <a name="resolution"></a>**解決方法**  
*次のいずれかの操作を行います。*  
  
-   *新しい物理システムに仮想ハード_ディスクを移動する記憶域の移行を実行します。*  
  
-   *Windows PowerShell または WMI を使用して、特定のセクター サイズを報告する VHDX フォーマットのバーチャル ハード ディスクを有効にするには*  
  
-   *レジストリ設定を使用して、レポートの 4 k 物理セクター サイズを VHD 形式のバーチャル ハード ディスクを有効にするには*  
  


