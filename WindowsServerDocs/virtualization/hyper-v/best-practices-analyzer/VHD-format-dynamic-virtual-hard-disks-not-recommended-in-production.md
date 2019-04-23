---
title: VHD 形式の動的な仮想ハード ディスクは、運用環境でサーバーのワークロードを実行する仮想マシンには推奨されません。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 324a60a0-1d15-4ef2-9f17-23cbd2eb42ce
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 6acd27fa0efa27ba74c28e290c789edca599f66f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849883"
---
# <a name="vhd-format-dynamic-virtual-hard-disks-are-not-recommended-for-virtual-machines-that-run-server-workloads-in-a-production-environment"></a>VHD 形式の動的な仮想ハード ディスクは、運用環境でサーバーのワークロードを実行する仮想マシンには推奨されません。

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
*1 つまたは複数の仮想マシンは、VHD 形式容量可変仮想ハード_ディスクの拡張を使用します。*  
  
## <a name="impact"></a>**影響**  
*VHD 形式の動的な仮想ハード ディスクには、電源障害が発生した場合に一貫性の問題が発生します。一貫性の問題は、物理ディスクは、電源障害が発生したときに変更されている .vhd ファイルに不完全または不正確、セクターに更新プログラムを実行する場合に発生することができます。これには、次の仮想マシンに影響します。*  
  
\<仮想マシンの一覧 >  
  
## <a name="resolution"></a>**解決方法**  
*仮想マシンをシャット ダウンし、VHDX 形式のバーチャル ハード ディスクと固定容量仮想ハード_ディスクを VHD 形式ダイナミック仮想ハード ディスクを変換します。(VHDX 形式とは、システム電源障害による破損からディスクを保護するための信頼性メカニズムのことです)。ただし、変換しないバーチャル ハード ディスクにある時点で Windows の以前のリリースに接続する可能性が高い場合。VHDX 形式をサポートしない Windows Server 2012 より前の Windows リリースします。*  
  


