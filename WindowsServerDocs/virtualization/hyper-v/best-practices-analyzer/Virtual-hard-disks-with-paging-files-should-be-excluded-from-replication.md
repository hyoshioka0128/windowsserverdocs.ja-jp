---
title: 仮想ハード_ディスクのページング ファイルとは、レプリケーションから除外する必要があります。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: c0be8a5f-64a1-488a-944e-bb913bb90517
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 8b6289a82c83f3dcfc0de299250ce19ee3782678
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850123"
---
# <a name="virtual-hard-disks-with-paging-files-should-be-excluded-from-replication"></a>仮想ハード_ディスクのページング ファイルとは、レプリケーションから除外する必要があります。

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、次を参照してください。 [Run Best Practices Analyzer Scans and Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177)します。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|情報|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*ページング ファイルは、レプリケーションに参加しているから除外する必要がありますが、ディスクが除外されません。*  
  
## <a name="impact"></a>影響  
*ページング ファイルには、大量の入力/出力のアクティビティは、レプリケーションに参加する量より多くのリソースが不必要に必要が発生します。これには、次の仮想マシンに影響します。*  
  
\<仮想マシンの一覧 >  
  
## <a name="resolution"></a>解決方法  
*されていない場合は、Windows ページング ファイルの個別の仮想ハード ディスクを作成します。初期レプリケーションは既に完了して場合、は、HYPER-V マネージャーを使用して、レプリケーションを削除します。その後、再度レプリケーションを構成し、レプリケーションからページング ファイルがある仮想ハード ディスクを除外します。*  
  


