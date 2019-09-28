---
title: 1つのストレージパスを複数のリソースプールにマップしない
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 24992453-762b-4892-9a50-55d237b9b7f2
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: e89c0382d20d586d8c0b50396ddbd56d6fdadf0b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365258"
---
# <a name="avoid-mapping-one-storage-path-to-multiple-resource-pools"></a>1つのストレージパスを複数のリソースプールにマップしない

>適用先:Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|警告|  
|**カテゴリ**|操作|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。
  
## <a name="issue"></a>**問題**  
*ストレージファイルのパスは、複数のリソースプールにマップされます。*  
  
## <a name="impact"></a>**よる**  
*指定された記憶域プールの種類では、次の親プールと子プールが同じストレージパスを共有します。*  
  
プールの @no__t 0 の一覧 >  
  
## <a name="resolution"></a>**解決方法**  
*複数のプールが同じストレージパスを使用しないように、Windows PowerShell を使用してストレージリソースプールを再構成します。*  
  


