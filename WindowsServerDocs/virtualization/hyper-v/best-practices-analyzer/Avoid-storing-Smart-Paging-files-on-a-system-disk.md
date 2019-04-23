---
title: システム ディスクでのスマート ページング ファイルを保存しないように
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 9b57c9b8-76c5-43c7-bfa6-2c95b3cb6510
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 6abc84b406de7e7c33628ccee4e3af706efe5c70
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886173"
---
# <a name="avoid-storing-smart-paging-files-on-a-system-disk"></a>システム ディスクでのスマート ページング ファイルを保存しないように

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、次を参照してください。 [Run Best Practices Analyzer Scans and Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177)します。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|警告|  
|**カテゴリ**|操作|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示されるテキストを示します。  
  
## <a name="issue"></a>問題  
*1 つまたは複数の仮想マシンのメモリ構成は、仮想マシンが再起動され、スマート ページング ファイルの指定した場所は、HYPER-V を実行しているサーバーのシステム ディスクの場合、スマート ページングの使用を必要があります。*  
  
## <a name="impact"></a>影響  
*スマート ページングのシステム ディスクの使用に問題が発生するには、HYPER-V を実行しているサーバーがあります。これには、次の仮想マシンに影響します。*  
  
\<仮想マシンの一覧 >  
  
## <a name="resolution"></a>解決方法  
*非システムのディスク上のスマート ページング ファイルを格納する仮想マシンを再構成します。*  
  


