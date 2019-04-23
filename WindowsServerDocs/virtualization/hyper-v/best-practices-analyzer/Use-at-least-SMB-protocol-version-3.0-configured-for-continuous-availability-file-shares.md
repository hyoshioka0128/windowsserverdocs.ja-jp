---
title: 使用して、少なくとも SMB プロトコルのバージョン 3.0 の継続的な可用性のバーチャル マシンのファイルを保存するファイル共有の構成
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: a1fa5cf9-8a48-4f63-bb57-d81e63e77b30
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 67f41293433bd8d14096688fbaa23eb43334c738
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877873"
---
# <a name="use-at-least-smb-protocol-version-30-configured-for-continuous-availability-on-file-shares-that-store-files-for-virtual-machines"></a>使用して、少なくとも SMB プロトコルのバージョン 3.0 の継続的な可用性のバーチャル マシンのファイルを保存するファイル共有の構成

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
*仮想マシンのファイルまたは仮想ハード ディスク ファイルは、SMB プロトコルのバージョン 3.0 の継続的可用性機能で構成されていないネットワーク ファイル共有に格納されます。*  
  
## <a name="impact"></a>**影響**  
*Microsoft は、サーバーを使用して仮想マシンの可用性に影響を与える可能性があるために、この構成を勧めしません。これには、次の仮想マシンに影響します。*  
  
\<仮想マシンの一覧 >  
  
## <a name="resolution"></a>**解決方法**  
次のいずれかの操作を行います。  
  
-   ファイルを継続的な可用性が構成されている SMB 3.0 ファイル共有に移動します。  
  
-   継続的な可用性を提供する現在のファイル共有を再構成します。  
  


