---
title: 仮想ハード_ディスクのページング ファイルとは、レプリケーションから除外する必要があります。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: c0be8a5f-64a1-488a-944e-bb913bb90517
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 94e03cf9de3991d003fad9019b9af33fad2f6bae
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855025"
---
# <a name="virtual-hard-disks-with-paging-files-should-be-excluded-from-replication"></a>仮想ハード_ディスクのページング ファイルとは、レプリケーションから除外する必要があります。

>適用対象: Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|情報|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*ページングファイルはレプリケーションに参加しないようにする必要がありますが、ディスクは除外されていません。*  
  
## <a name="impact"></a>影響  
*ページングファイルを使用すると、大量の入出力アクティビティが発生し、レプリケーションに参加するために必要なリソースが不必要に増えることがあります。これは、次の仮想マシンに影響します。*  
  
仮想マシンの一覧を \<>  
  
## <a name="resolution"></a>解決方法  
*Windows のページングファイル用に別の仮想ハードディスクを作成していない場合は、作成します。初期レプリケーションが既に完了している場合は、Hyper-v マネージャーを使用してレプリケーションを削除します。次に、レプリケーションをもう一度構成し、ページングファイルのある仮想ハードディスクをレプリケーションから除外します。*  
  


