---
title: 複数のリソース プールへの 1 つのストレージ パスのマッピングを避ける
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 24992453-762b-4892-9a50-55d237b9b7f2
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 7c012836309f722e55c28b2ddbe3d54de641b4af
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823963"
---
# <a name="avoid-mapping-one-storage-path-to-multiple-resource-pools"></a>複数のリソース プールへの 1 つのストレージ パスのマッピングを避ける

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、次を参照してください。 [Run Best Practices Analyzer Scans and Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177)します。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|警告|  
|**カテゴリ**|操作|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。
  
## <a name="issue"></a>**問題**  
*ストレージ ファイルのパスは、複数のリソース プールにマップされます。*  
  
## <a name="impact"></a>**影響**  
*指定した記憶域プールの種類には、親と子の次のプールは、同じパスを記憶域を共有します。*  
  
\<プールの一覧 >  
  
## <a name="resolution"></a>**解決方法**  
*Windows PowerShell を使用して、複数のプールが同じ記憶域パスを使用しないように、記憶域のリソース プールを再構成します。*  
  


